---
layout: post
published: true
title: 'Reusable, Configurable Lightning input/output form component.'
mathjax: false
featured: true
comments: true
headline: >-
  Reusable, Apexless, Fieldset-driven, Configurable Lightning input/output form
  component.
description: >-
  Reusable, Apexless, Fieldset-driven, Configurable Lightning input/output form
  component.
tags: LightningComponent Freebies FieldSet Appbuilder
categories:
  - LightningComponent
  - Freebies
---
Few questions for you,

- Are you using Salesforce Lightning Experience?
- Do you need to show few input fields only on basis of certain filter criteria (can\`t create new recordtype)?
- Want to have flexibility to add/remove/reorder the displayed fields?
- Also need flexibility to change the title/icon of the form component?
- Added flexibility of having the form support both output (read-only)  input(Create / Update) will not hurt?
- [Update]Added support for inline editing in output mode

### If answer to above question is yes look no further, below component is match made in heaven, as it will let you to do the following,

1. Declare the fields for component in fieldset
   ![fieldset.PNG]({{site.baseurl}}/images/fieldset.PNG)

2. Leaverage appbuilder to drag and drop it onto record pages of your choice.
   - Configure the components attributes(object, title, icon, mode(Input/Output) ) 
   - Filter conditions when the component need to be shown.
   ![appbuilder config.PNG]({{site.baseurl}}/images/appbuilder%20config.PNG)
   
3. And here\`s how it looks,
	  * Input Mode  
      ![inputMode.PNG]({{site.baseurl}}/images/inputMode.PNG)
      * Output Mode  
      ![outputMode.PNG]({{site.baseurl}}/images/outputMode.PNG)  
      * Output Mode- Pencil Clicked  
      ![outputMode Edit Pencil Clicked.png]({{site.baseurl}}/images/outputMode%20Edit%20Pencil%20Clicked.png)
    
*Github Repo Link:*  
https://github.com/struckbylightning/FieldsetLightningCompForm  
*Unmanaged Package Link (free, free, free!):*  
https://login.salesforce.com/packaging/installPackage.apexp?p0=04t7F0000051DNd
 [V1.1 with Inline editing support]

**Demo:**
![fieldsetFormLC.gif]({{site.baseurl}}/images/fieldsetFormLC.gif){:height="80%" width="80%"}  

**Code Snippets:**

```html
<aura:component implements="flexipage:availableForRecordHome,force:hasRecordId" access="global" controller="FieldSetController">
    <aura:attribute name="recordTypeId" type="String"/> 
    <aura:attribute name="objectApiName" type="String"/> 
    <aura:attribute name="fields" type="FieldSetMember[]"/>  
    <aura:attribute name="fieldSetName" type="String"/> 
    <aura:attribute name="iconName" type="String"/>
    <aura:attribute name="title" type="String"/> 
    <aura:attribute name="mode" type="String"/> 
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <lightning:card title="{!v.title}" iconName="{!v.iconName}" class="slds-p-around--small">
        <lightning:recordEditForm aura:id="recordViewForm" 
                                  recordId="{!v.recordId}"
                                  objectApiName="{!v.objectApiName}"
                                  onsubmit="{!c.fireRefreshView}">
            <!-- recordTypeId="{!v.recordTypeId}" -->
            <lightning:messages />
            <aura:iteration items="{!v.fields}" var="field">
                <aura:if isTrue="{!v.mode=='Input'? true: false}">
                    <lightning:inputField fieldName="{!field.fieldPath}"/>
                </aura:if>
                <aura:if isTrue="{!v.mode=='Output'? true: false}">
                    <lightning:outputField fieldName="{!field.fieldPath}"/>
                </aura:if>
            </aura:iteration>
            <aura:if isTrue="{!v.mode=='Input'? true: false}">
                <lightning:button class="slds-m-top_small" variant="brand"
                                  type="submit" name="update" 
                                  label="{!empty(v.recordId)?'Create':'Update'}" />
            </aura:if>
        </lightning:recordEditForm>
    </lightning:card>
</aura:component>
```

```js
({
    doInit : function(component, event, helper) {
        var action = component.get("c.getFields");
        var objectApiName = component.get("v.objectApiName");
        var fsName = component.get("v.fieldSetName");
        action.setParams({typeName: objectApiName, fsName: fsName});
        action.setCallback(this, function(a) {
            var fields = a.getReturnValue();
            component.set("v.fields", fields);
        });
        $A.enqueueAction(action);        
    },
    fireRefreshView : function(component, event, helper) {
         $A.get('e.force:refreshView').fire();
    }
})
```

```html
<design:component >
    <design:attribute name="objectApiName" label="Object API Name" 
                      description="objectApiName" 
                      default="Contact"
                      required="true"/>
    <design:attribute name="fieldSetName" label="Fieldset Name" 
                      description="Fieldset Name" 
                      default="lightningFormContactFields"
                      required="true"/>
    <design:attribute name="iconName" 
                      label="Card icon Name" 
                      description="Icon Name" 
                      default="standard:contact"/>
    <design:attribute name="title" label="Title" 
                      description="Component Title" 
                      required="true"
                      default="Update Information"/>
    <design:attribute name="mode" label="Mode" datasource="Input,Output" required="true"/>
</design:component>
```
