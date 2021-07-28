# Understand Execution Context

## Execution Context

For ASP.NET applications, code is executed in the context of an application domain.
In the Lightning Platform world, code executes within an execution context.

![image](./02-methods-of-invoking-apex.png)

Besides invoking Apex code, `actions`, such as `creating a new task`, `sending an email`, `performing a field update`, or `sending an outbound message`, can all be triggered by one of the declarative platform features. These actions also run within an execution context.

Another important consideration is the context of the user executing the Apex code. `By default, Apex executes in system context.` Apex code has access to all `objects` and `fields`. Object permissions, field-level security, and sharing rules aren’t applied for the current user.
