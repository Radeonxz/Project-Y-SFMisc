# Code with Salesforce Languages

## Options

Three core programmatic technologies to learn about:

1. `Lightning Component Framework`: A UI development framework similar to AngularJS or React.
2. `Apex`: Salesforce’s proprietary programming language with Java-like syntax.
3. `Visualforce`: A markup language that lets you create custom Salesforce pages with code that looks a lot like HTML, and optionally can use a powerful combination of Apex and JavaScript.

## Lightning Components

The `Lightning Component framework` is a user interface development framework for `desktop` and `mobile`. As its name suggests, it’s a component-based approach to UI development. Using prebuilt and custom Lightning components, you can quickly develop sleek and consistent UIs for your apps.

### Create Map Lightning Components

1. Navigate to Setup by clicking the gear menu and then clicking `Setup`.
2. In the Quick Find bar, search for and click `Lightning Components`.
3. Click `Map` and then click `Developer Console`.

The `Developer Console` is the Salesforce integrated development environment (IDE) that you can use to develop, debug, and test code in your org. Right now, it contains the code for the property map you just saw. It’s XML markup. It contains both Aura-specific and static HTML tags. It uses a `<namespace:tagName>` convention for its tags, each represents a smaller, or child, component.

## Apex

1. From Setup, search Quick Find for Process Builder and open the Process Builder page.
2. Click `Price Change Push Notification`.
3. Under Immediate Actions, click `Push Notification`.
4. Notice the value in the Apex Class field. From the gear menu up top, open the Developer Console.
5. Click `File` | `Open` and use the Filter bar to find PushPriceChangeNotification. Double-click to open it in the Developer Console.

## Visualforce

Visualforce lets you create and customize pages in Salesforce as well as integrate with other standard web technologies, including HTML, CSS, and JavaScript.
