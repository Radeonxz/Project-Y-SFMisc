# Debug and Run Diagnostics

## Debug Log

In the world of the Lightning Platform, the debug log is where you find most of what you need to debug and analyze your code. You’ve already seen how you can write to the debug log. That is done with something like the following.

```
System.debug('My Debug Message');
```

Specify one of the following logging levels.

- NONE
- ERROR
- WARN
- INFO
- DEBUG
- FINE
- FINER
- FINEST

These levels run from lowest to highest and are cumulative. So if you pick the finest level, you get all messages that are logged as error, warn, info, and so on. There are also several debug log categories, and the amount of information logged depends on the log level.

Each debug log must be **20 MB** or **smaller**. If it exceeds this amount, you won’t see everything you need. Additionally, each org can retain up to **1,000 MB** of debug logs. The oldest logs are overwritten.

## Use the Log Inspector

Developer Console has grown quite a bit in the past few releases. One of its more useful features is the Log Inspector. To see how it works, let’s walk through running some anonymous code and viewing the results.

1. From Setup, select **Your Name** > **Developer Console** to open Developer Console.
2. Select **Debug** > **Change Log Levels**.
3. Click the **Add/Change** link in General Trace Setting for You.
4. Select **INFO** as the debug level for all columns.
5. Click **Done**.
6. Click **Done**.
7. Select **Debug** > **Perspective Manager**.
8. Select **All (Predefined)** and click **Set Default**.
9. Click **Yes** to change this to your default perspective.
10. Close the Developer Console Perspective window.
11. Select **Debug** > **Open Execute Anonymous Window**.
12. Delete the existing code, and insert the following snippet:

```
System.debug(LoggingLevel.INFO, 'My Info Debug Message');
System.debug(LoggingLevel.FINE, 'My Fine Debug Message');
List<Account> accts = [SELECT Id, Name FROM Account];
for(Account a : accts) {
    System.debug('Account Name: ' + a.name);
    System.debug('Account Id: ' + a.Id);
}
```

13. Make sure that Open Log is selected, and click **Execute**.
14. Select Debug > Switch Perspective > All (Predefined).
15. Examine the results in the Timeline and Executed Units tabs.
16. Under Execution Log, select the Filter option, and enter FINE. Because we set the debug level t INFO for Apex Code, no results appear.
17. Select Debug > Change Log Levels.
18. Click the Add/Change link in General Trace Setting for You.
19. Change the DebugLevel for ApexCode and Profiling to FINEST.
20. Click Done.
21. Click Done.
22. Select Debug > Open Execute Anonymous Window.
23. Leave the code that is currently there, and click Execute.
24. Under Execution Log, select the Filter option, and enter FINE. The filter search is case sensitive. You now see "My Fine Debug Message" displayed. You should also notice a size difference between the two latest logs in the Logs tab.

### Set Checkpoints

Checkpoints are similar to breakpoints in that they reveal a lot of detailed execution information about a line of code. They just don’t stop execution on that line.

1. From Setup, select **Your Name** > **Developer Console** to open Developer Console.
2. Select **File** > **Open**.
3. Select **Classes** as the entity type, and **AccountHandler** as the entity.
4. Click **Open**.
5. Position your cursor over line 10 in the left margin and click once. A red dot appears next to the line number.
6. Click .
7. Double-click the latest entry in the Logs panel to open the debug log.
8. Select **Debug** > **Open Execute Anonymous Window**.
9. Delete the existing code, and insert the following snippet:

```
Account acct = new Account(
    Name='Test Account 3',
    Phone='(415)555-8989',
    NumberOfEmployees=30,
    BillingCity='San Francisco');
insert acct;
```

10. Make sure that Open Log is selected, and click **Execute**.
11. Click the **Checkpoints** tab, and double-click the first entry that appears. The Checkpoint Inspector appears.
12. On the Symbols tab, expand the nodes within the execution tree. Notice the Key and Value columns.
13. Click the **Heap** tab. Notice the Count and Total Size columns.
