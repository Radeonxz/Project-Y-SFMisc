# Develop Without Code

## The Power of Metadata

In this abstraction, objects are our database tables. The fields on those objects are columns, and records are rows in the database. This analogy is true both for `standard objects` that come with Salesforce by default and `custom objects` that you build yourself.

In short, metadata forms the structure of your org. Whether you’re defining fields, business processes, or something more complex, metadata holds your configuration. The platform then renders your app’s metadata in the user interface along with its associated data.

This `metadata-driven development model` is one of the key differences between developing on the platform and developing outside of Salesforce. Because the platform is metadata-aware, it can auto-generate a significant part of your user experience for you. Things like dialogs, record lists, detail views, and forms that you’d normally have to develop by yourself come for free. You even get all the functionality to create, read, update, and delete (affectionately referred to as CRUD) custom object records in the database.

The platform provides a handy tool called Schema Builder so you can see your entity relationship model in action.

1. Navigate to Setup by clicking the gear menu and then clicking `Setup`.
2. Search for Schema Builder in the Quick Find box. When you initially open Schema Builder, you see all the custom and standard objects in your org.
3. Clear all current selections. From the Select from menu, choose Custom Objects and then select all.

## No-Code and Low-Code Development

Salesforce offers a host of tools for point-and-click—or `declarative`—development. Most of these tools require little to no understanding of development principles: no code. Someone who thinks JSON is just missing a letter can construct a robust and complex data model. A person who hears Cron and thinks it’s some kind of sci-fi film can schedule batch jobs.
