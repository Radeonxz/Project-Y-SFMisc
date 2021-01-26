#### Class Syntax

```
private | public | global
[virtual | abstract | with sharing | without sharing]
class ClassName [implements InterfaceNameList] [extends ClassName]
{
    // The body of the class
}
```

#### Enum

```
public enum myEnums {
    Enum1,
    Enum2,
    Enum3
}
```

```
Integer enumOrd = myEnums.Enum3.ordinal();
```

#### List

```
List<String> myStrings =  new List<String>();

String[] myStrings = new List<String>();

List<String> myStrings =  new List<String> {'String1', 'String2', 'String3' };

List<String> myStrings = new List<String>();
myStrings.add('String1');
myStrings.add('String2');
myStrings.add('String3');

List<Account> myAccounts = [SELECT Id, Name FROM Account];

List<Account> myAccounts = [SELECT Id, Name FROM Account];
String firstAccount = myAccounts[0].Name;
```

#### Set

```
Set<ID> accountIds = new Set<ID>{'001d000000BOaHSAA1','001d000000BOaHTAA1'};  
List<Account> accounts = [SELECT Name FROM Account WHERE Id IN :accountIds];    
```

#### Map

```
Map<Id, Account> accountMap = new Map<Id, Account>([SELECT Id, Name FROM Account]);

Id accId = '001d000000BOaHSAA1';
Account account = accountMap.get(accId);
```

