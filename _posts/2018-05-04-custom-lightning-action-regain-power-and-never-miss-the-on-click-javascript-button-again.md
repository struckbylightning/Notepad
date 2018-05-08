---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: >-
  Custom Lightning Action, Regain Power and never miss the On-Click JavaScript
  button again!!!
---
## Cheers to the Future - Custom Lightning Action

I know despite of what Salesforce says [here](https://developer.salesforce.com/blogs/developer-relations/2016/10/your-new-life-with-lightning-actions-smart-fast-and-mobile.html) to [Break Up with JavaScript Buttons and Embrace Lightning](https://developer.salesforce.com/blogs/developer-relations/?p=157981&preview=true) and suggests the [First Steps: to replace JavaScript Buttons](https://developer.salesforce.com/blogs/developer-relations/2016/09/take-the-first-steps-ways-you-can-replace-javascript-buttons.html)
-[with Lightning Actions( because they are Smart, Fast, and Mobile](https://developer.salesforce.com/blogs/developer-relations/2016/10/your-new-life-with-lightning-actions-smart-fast-and-mobile.html), we all still continue to miss our mighty old friends(On-Click Javascript buttons) when we run into situations highlted below when despite of all suggested we are still unsure of the way out,

#### Needing to do following currently hurts as there\`s no straight forward to perform the below listed seemingly simple tasks,

- Button with simple 'Are you sure?' confirm box.
- Button with conditional 'Are you sure?' confirm box.
- Button which does conditional redirection.
- Button that simply does API callouts to external system (no UI required!)
- Button which opens up a prefilled form.
- Button which just calls an Apex method to do the needfull.
- Button that can leverage the power of OOB [events that are handled in the Salesforce mobile app and Lightning Experience](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/events_one.htm) 
- Button that can redirect to another Lightning Component or open up the component inside a modal.

What if I tell you can do all mentioned above with all pointNclicks and very minimal code, Sounds Magical Right!!

All you need to do is dragNdrop \'customLightningAction.cmp\' to record detail page and configure few design parameters(ref table at end for details) and woof you are all set :)

### Let\`s straight away jump and see the component in action, with help of below scenarios,

**1. Always Confirm box + redirect to component example**
- Let\`s say on click of 'Create Sales Order' button on Account Record we want always show a confirm box with 'Are you Sure?' message with Yes/No buttons, and then,
-- If user clicks Yes, redirect them to 'newSalesOrderWizard.cmp'(1a) or open the component in modal(1b).
-- If clicks No then close the confirm modal.

**1a. Redirect to Component on confirm**
![ConfirmBoxAlwaysCmpRedirect.gif]({{site.baseurl}}/images/ConfirmBoxAlwaysCmpRedirect.gif)
**1b. Open Component in a Modal on confirm**
![ConfirmBoxAlwaysCmpModal.gif]({{site.baseurl}}/images/ConfirmBoxAlwaysCmpModal.gif)

**2. Conditional Confirm box + call Apex example**
- Now Let\`s say on click of 'Create Sales Order' button on Account Record we want to first do a Credit Status check and accordingly show a Confirm Box on basis of the results,
-- If Account.Credit_Status__c == 'Red' we want to show a message 'This account has been marked Red are you sure you want to create a new Sales order?', and then,
--- If user clicks Yes then call 'createSalesOrder' apex method.
--- If clicks No then close the confirm modal.
-- Else call 'createSalesOrder' apex method

![ConditionalConfirmApexCall.gif]({{site.baseurl}}/images/ConditionalConfirmApexCall.gif)

3. Validate Prior Redirecting + Fire Event example
- Let\`s say on click of 'Create Sales Order' button on Account Record we want to first do a Credit Status check and accordingly stop user from proceeding on basis of the result, 
-- If Account.Credit_Status__c == 'Red' we want to show a message 'You cannot place new Sales order as Finance has marked this account Red, Check with Finance team for more info'. and block the user from proceding.
-- Else Fire force:createRecord event

![validateEvent.gif]({{site.baseurl}}/images/validateEvent.gif)

## This package comes with other reusable freebies which are ingrained into this component but can be easily decoupled and utilized.
- loadingSpinnerComp - Simple component to show a centered spinner on basis of a boolean attribute
- genericUtilities.cmp, GenericDataSaverApxCtrl.apxc, APXFieldValidationError
- To simplify performing DMLs from LC and also support a better error handling mechanism which helps with finite details around failing validation rules in a consumable way 
- LightningServerResponse - Any call to Apex will always return LightningServerResponse (in component I build, Why?- probably will write another post explaining all these antics)

| S.no | Design Attribute Label                                                                          | Attribute Type | Options                                                         | Additional Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Required? |
|------|-------------------------------------------------------------------------------------------------|----------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| 1    | Button Label                                                                                    | String         |                                                                 | The text to be displayed inside   the button.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Yes       |
| 2    | Show Confirm Box?                                                                               | Picklist       | Always     Conditional     Never     ValidatePriorToRedirecting | 1. Always - \'Confirm box will   be shown always\'     2. Conditional - \'Apex method defined in attribute 3 will be called and on basis of   showConfirmMessage retured(as a part of returned LightningServerResponse\`s   objectData) confirm box will be shown accordingly.     3. Never - \'No Confirm box will be shown\'     4. ValidatePriorToRedirecting - \'No Confirm box will be shown, however   apex method defined in attribute 3 will be called and on basis of redirect   param returned (as a part of returned LightningServerResponse\`s objectData)   following logic will be executed or error message will be shown | Yes       |
| 3    | If Conditional, Enter the name   of the Method in CustomLightningActionApxCtrl.cls to be called | String         |                                                                 | Will be called as per #2, and   will need to return showConfirmMessage/redirect param accordingly.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |           |
| 4    | Enter Confirmation Message                                                                      | String         |                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 5    | Call apex or load component or   fire an event                                                  | Picklist       | Apex     Component     Event                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 6    | If Apex, Enter the name of the   Method in CustomLightningActionApxCtrl.cls to be called        |                |                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 7    | If Event, Enter the name of the   Event                                                         | String         |                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 8    | If Component, Enter the Name                                                                    | String         |                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 9    | Component Load Type                                                                             | Picklist       | Modal     Redirect                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
| 10   | Record Id Holder Attribute                                                                      | String         |                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |           |
