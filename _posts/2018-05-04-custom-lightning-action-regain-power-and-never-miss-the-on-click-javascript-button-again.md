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

Yes I know it hurts and that\`s why 'customLightningAction.cmp' is created, which allows you to drag and drop it onto any record detail page and then configure the following design parameters to suit your need.

#### Diclaimer - Before I begin explainig how to utilize this comp, please be aware that this is going to be a bit long post, given that component does a lot (I should have simply done a video but still a bit too lazy for that)

1. Once you drag and drop below are the attributes that needs to be configured,

|    Design   Attribute Label                                                                       | Attribute Type | Options                                                         | Additional   Description                                                                                                         | Required?    |
|---------------------------------------------------------------------------------------------------|----------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|--------------|
| Button   Label                                                                                    | String         |                                                                 | The text to be displayed inside the button.                                                                                      | Yes          |
| Show   Confirm Box?                                                                               | Picklist       | Always     Conditional     Never     ValidatePriorToRedirecting | Always - 'Confirm box will be   shown always'     Conditional - 'Apex method defined in '      Never, ValidatePriorToRedirecting | Yes          |
| If   Conditional, Enter the name of the Method in CustomLightningActionApxCtrl.cls   to be called | String         |                                                                 |                                                                                                                                  |              |
| Enter   Confirmation Message                                                                      | String         |                                                                 |                                                                                                                                  |              |
| Call   apex or load component or fire an event                                                    | Picklist       | Apex     Component     Event                                    |                                                                                                                                  |              |
| If Apex,   Enter the name of the Method in CustomLightningActionApxCtrl.cls to be called          |                |                                                                 |                                                                                                                                  |              |
| If   Event, Enter the name of the Event                                                           | String         |                                                                 |                                                                                                                                  |              |
| If   Component, Enter the Name                                                                    | String         |                                                                 |                                                                                                                                  |              |
| Component   Load Type                                                                             | Picklist       | Modal     Redirect                                              |                                                                                                                                  |              |
| Record   Id Holder Attribute                                                                      | String         |                                                                 |                                                                                                                                  |              |

1. Always Confirm box example + redirect to component 
- Let\`s say on click of 'Create Sales Order' button on Account Record we want always show a confirm box with 'Are you Sure you want to really place new sales order?' message with Yes/No buttons,
   -- If user clicks Yes then redirect to 'newSalesOrderWizard.cmp'.
   -- If clicks No then close the confirm modal.
2. Conditional Confirm box example + call Apex
- Now Let\`s say on click of 'Create Sales Order' button on Account Record we want to first do a Credit Status check and accordingly show a Confirm Box on basis of the results,
-- If Account.Credit_Status__c == 'Red' we want to show a message 'This account has been marked Red are you sure you want to create a new Sales order?'.
   --- If user clicks Yes then call 'createSalesOrder' apex method.
   --- If clicks No then close the confirm modal.
-- Else call 'createSalesOrder' apex method
3. Validate Prior Redirecting + Fire Event
- Let\`s say on click of 'Create Sales Order' button on Account Record we want to first do a Credit Status check and accordingly stop user from proceeding on basis of the result, 
-- If Account.Credit_Status__c == 'Red' we want to show a message 'You cannot place new Sales order as Finance has marked this account Red, Check with Finance team for more info'. and block the user from proceding.
-- Else Fire force:createRecord event


## This package comes with other reusable freebies which are ingrained into this component but can be easily decoupled and utilized.
- loadingSpinnerComp - Simple component to show a centered spinner on basis of a boolean attribute
- genericUtilities.cmp, GenericDataSaverApxCtrl.apxc, APXFieldValidationError
- To simplify performing DMLs from LC and also support a better error handling mechanism which helps with finite details around failing validation rules in a consumable way 
- LightningServerResponse - Any call to Apex will always return LightningServerResponse (in component I build, Why?- probably will write another post explaining all these antics)
