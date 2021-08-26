# Get Started with Aura Components

## Lightning Component Framework

**The Lightning Component framework** is a **UI framework** for developing **web apps** for **mobile** and **desktop** devices. It’s a modern framework for building **single-page applications** with dynamic, responsive user interfaces for Lightning Platform apps. It uses JavaScript on the client side and Apex on the server side.

## An Example Aura Component

![image](./02-aura-component-example.png)

Code:

```
<aura:component>
    <aura:attribute name="expense" type="Expense__c"/>
    <aura:registerEvent name="updateExpense" type="c:expensesItemUpdate"/>
    <!-- Color the item green if the expense is reimbursed -->
    <lightning:card title="{!v.expense.Name}" iconName="standard:scan_card"
                    class="{!v.expense.Reimbursed__c ?
                           'slds-theme_success' : ''}">
        <aura:set attribute="footer">
            <p>Date: <lightning:formattedDateTime value="{!v.formatdate}"/></p>
            <p class="slds-text-title"><lightning:relativeDateTime value="{!v.formatdate}"/></p>
        </aura:set>
        <p class="slds-text-heading_medium slds-p-horizontal_small">
            Amount: <lightning:formattedNumber value="{!v.expense.Amount__c}" style="currency"/>
        </p>
        <p class="slds-p-horizontal_small">
           Client: {!v.expense.Client__c}
        </p>
        <p>
            <lightning:input type="toggle"
                             label="Reimbursed?"
                             name="reimbursed"
                             class="slds-p-around_small"
                             checked="{!v.expense.Reimbursed__c}"
                             messageToggleActive="Yes"
                             messageToggleInactive="No"
                             onchange="{!c.clickReimbursed}"/>
        </p>
    </lightning:card>
</aura:component>
```

First of all, it’s XML markup, and mixes both static HTML tags with custom Aura component tags, such as the `<aura:component>` tag that leads off the sample. If you’ve worked with Visualforce, the format of that tag is familiar: ` namespace``: ` `tagName` . As you’ll see later, built-in components can come from a variety of different namespaces, such as `aura:` (as here), or `force:`, `lightning:`, or `ui:`.
