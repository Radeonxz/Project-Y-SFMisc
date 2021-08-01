# Understand Execution Context

## Execution Context

For ASP.NET applications, code is executed in the context of an application domain.
In the Lightning Platform world, code executes within an execution context.

![image](./02-methods-of-invoking-apex.png)

Besides invoking Apex code, `actions`, such as `creating a new task`, `sending an email`, `performing a field update`, or `sending an outbound message`, can all be triggered by one of the declarative platform features. These actions also run within an execution context.

Another important consideration is the context of the user executing the Apex code. `By default, Apex executes in system context.` Apex code has access to all `objects` and `fields`. Object permissions, field-level security, and sharing rules aren’t applied for the current user.

## Trigger Essentials

Similar to triggers in SQL Server, Apex database triggers execute programming logic before or after events to records in Salesforce. When defining the trigger, you can specify more than one of the following events:

- before insert
- before update
- before delete
- after insert
- after update
- after delete
- after undelete

The basic syntax for a trigger looks like the following:

```
trigger TriggerName on ObjectName (trigger_events) {
   // code_block
}
```

You only want to resort to using a trigger when you are absolutely sure that the same thing cannot be accomplished with one of our point-and-click automation tools.

## Mark Execution Context

An Apex database trigger that creates an opportunity when a new account is entered. This trigger calls a method from a handler class, so we first need to create that.

1. From Setup, select Your Name > `Developer Console` to open Developer Console.
2. In Developer Console, select `File` > `New` > `Apex Class`.
3. Enter AccountHandler for the class name and click OK.
4. Delete the existing code, and insert the following snippet:

```
public with sharing class AccountHandler {
    public static void CreateNewOpportunity(List<Account> accts) {
        for (Account a : accts) {
            Opportunity opp = new Opportunity();
            opp.Name = a.Name + ' Opportunity';
            opp.AccountId = a.Id;
            opp.StageName = 'Prospecting';
            opp.CloseDate = System.Today().addMonths(1);
            insert opp;
        }
    }
}
```

5. Press `Ctrl + S` to save your class.
