# Use Asynchronous Apex

## When to Go Asynchronous

The following three reasons are usually behind choosing asynchronous programming.

1. `Processing a very large number of records`. This reason is unique to the multi-tenanted world of the Lightning Platform where limits rule. The limits associated with asynchronous processes are higher than those with synchronous processes. Therefore, if you need to process thousands or even millions of records, asynchronous processing is your best bet.

2. `Making callouts to external web services`. Callouts can take a long time to process, but in the Lightning Platform, triggers can’t make callouts directly.

3. `Creating a better and faster user experience` by offloading some processing to asynchronous calls. Why do everything at once? If it can wait, let it.
