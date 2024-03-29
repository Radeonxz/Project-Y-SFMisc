# Use Asynchronous Apex

## When to Go Asynchronous

The following three reasons are usually behind choosing asynchronous programming.

1. **Processing a very large number of records**. This reason is unique to the multi-tenanted world of the Lightning Platform where limits rule. The limits associated with asynchronous processes are higher than those with synchronous processes. Therefore, if you need to process thousands or even millions of records, asynchronous processing is your best bet.

2. **Making callouts to external web services**. Callouts can take a long time to process, but in the Lightning Platform, triggers can’t make callouts directly.

3. **Creating a better and faster user experience** by offloading some processing to asynchronous calls. Why do everything at once? If it can wait, let it.

## Future Methods

In situations where you need to make a callout to a web service or want to offload simple processing to an asynchronous task, creating a future method could be the way to go.

Changing a method from synchronous to asynchronous processing is amazingly easy. Essentially, you just add the @future annotation to your method. Other than that, just make sure that the method is static and returns only a void type. For example, to create a method for performing a web service callout, we could do something like this:

```
public class MyFutureClass {
    // Include callout=true when making callouts
    @future(callout=true)
    static void myFutureMethod(Set<Id> ids) {
        // Get the list of contacts in the future method since
        // you cannot pass objects as arguments to future methods
        List<Contact> contacts = [SELECT Id, LastName, FirstName, Email
            FROM Contact WHERE Id IN :ids];
        // Loop through the results and call a method
        // which contains the code to do the actual callout
        for (Contact con: contacts) {
            String response = anotherClass.calloutMethod(con.Id,
                con.FirstName,
                con.LastName,
                con.Email);
            // May want to add some code here to log
            // the response to a custom object
        }
    }
}
```

### Future Limitations

Here are some limitations to consider before using a future method.

- You can’t track execution because no **Apex job ID** is returned.
- Parameters must be **primitive data types**, arrays of primitive data types, or collections of primitive data types. Future methods **can’t take objects as arguments**.
- You can’t chain future methods and have one call another.

## Batch or Scheduled Apex

Another long-used asynchronous tool is the **batchable interface**. The No. 1 reason to use it is if you need to process a large number of records. For example, if you want to clean up or archive **up to 50 million records**, the batchable interface is your answer. You can even schedule your batches to run at a particular time.

To use it, your class implements the **Database.Batchable interface**. You also define **start()**, **execute()**, and **finish()** methods. You can then invoke a batch class using the **Database.executeBatch** method. For example, the following code creates a batchable class that processes all accounts in an org and then sends an email when it is done.

```
global class MyBatchableClass implements
            Database.Batchable<sObject>,
            Database.Stateful {
    // Used to record the total number of Accounts processed
    global Integer numOfRecs = 0;
    // Used to gather the records that will be passed to the interface method
    // This method will only be called once and will return either a
    // Database.QueryLocator object or an Iterable that contains the records
    // or objects passed to the job.
    global Database.QueryLocator start(Database.BatchableContext bc) {
        return Database.getQueryLocator('SELECT Id, Name FROM Account');
    }
    // This is where the actual processing occurs as data is chunked into
    // batches and the default batch size is 200.
    global void execute(Database.BatchableContext bc, List<Account> scope) {
        for (Account acc : scope) {
            // Do some processing here
            // and then increment the counter variable
            numOfRecs = numOfRecs + 1;
        }
    }
    // Used to execute any post-processing that may need to happen. This
    // is called only once and after all the batches have finished.
    global void finish(Database.BatchableContext bc) {
        EmailManager.sendMail('someAddress@somewhere.com',
                              numOfRecs + ' Accounts were processed!',
                              'Meet me at the bar for drinks to celebrate');
    }
}
```

You could then invoke the batch class using anonymous code such as this:

```
MyBatchableClass myBatchObject = new MyBatchableClass();
Database.executeBatch(myBatchObject);
```

### Batchable Limitations

The batchable interface is great, but as with just about everything, consider its limitations.

- Troubleshooting can be troublesome.
- Jobs are queued and subject to server availability, which can sometimes take longer than anticipated.

## And Then There Was Queueable Apex

Queueable Apex provides the following benefits to future methods.

- **Non-primitive types** - Classes can accept parameter variables of non-primitive data types, such as sObjects or custom Apex types.
- **Monitoring** - When you submit your job, a jobId is returned that you can use to identify the job and monitor its progress.
- **Chaining jobs** - You can chain one job to another job by starting a second job from a running job. Chaining jobs is useful for sequential processing.

Because **Queueable Apex** includes the best of future methods, it’s much easier to implement than Batch Apex. It just doesn’t have those pesky limitations we talked about. To demonstrate how it works, let’s take the sample code that used a future method to do a web callout and implement it using Queueable Apex.

```
public class MyQueueableClass implements Queueable {
    private List<Contact> contacts;
    // Constructor for the class, where we pass
    // in the list of contacts that we want to process
    public MyQueueableClass(List<Contact> myContacts) {
        contacts = myContacts;
    }
    public void execute(QueueableContext context) {
        // Loop through the contacts passed in through
        // the constructor and call a method
        // which contains the code to do the actual callout
        for (Contact con: contacts) {
            String response = anotherClass.calloutMethod(con.Id,
                    con.FirstName,
                    con.LastName,
                    con.Email);
            // May still want to add some code here to log
            // the response to a custom object
        }
    }
}
```

To invoke Queueable Apex, you need something like the following:

```
List<Contact> contacts = [SELECT Id, LastName, FirstName, Email
    FROM Contact WHERE Is_Active__c = true];
Id jobId = System.enqueueJob(new MyQueueableClass(contacts));
```
