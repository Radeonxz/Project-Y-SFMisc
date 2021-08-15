# Use Asynchronous Apex

## When to Go Asynchronous

The following three reasons are usually behind choosing asynchronous programming.

1. `Processing a very large number of records`. This reason is unique to the multi-tenanted world of the Lightning Platform where limits rule. The limits associated with asynchronous processes are higher than those with synchronous processes. Therefore, if you need to process thousands or even millions of records, asynchronous processing is your best bet.

2. `Making callouts to external web services`. Callouts can take a long time to process, but in the Lightning Platform, triggers can’t make callouts directly.

3. `Creating a better and faster user experience` by offloading some processing to asynchronous calls. Why do everything at once? If it can wait, let it.

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
