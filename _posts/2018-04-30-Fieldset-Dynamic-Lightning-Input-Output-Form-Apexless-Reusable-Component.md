---
layout: post
published: true
title: >-
  Reusable, Apexless, Fieldset-driven, Configurable Lightning input/output form
  component.
mathjax: false
featured: true
comments: true
headline: >-
  Reusable, Apexless, Fieldset-driven, Configurable Lightning input/output form
  component.
description: >-
  Reusable, Apexless, Fieldset-driven, Configurable Lightning input/output form
  component.
categories:
  - LightningComponent
tags: 'LightningComponent,reusable component,AdminsFavorite'
---

Are you using LeX?
Do you need to show few input fields only on basis of certain filter criteria (can\`t create new recordtype)?
Want to  have flexibility to add/remove/reorder the displayed fields?
Also need flexibility to change the title/icon of the form component?
Added flexibility of having the form support both output(read-only) / input(Create / Update) will not hurt?

If answer to above question is yes look no further, below component is match made in heaven.

You\`ll be able to declare fields in fieldset and leaverage appbuilder to drag and configure the components onto the record pages you wish, just that simple!

Unmanaged Package Link - https://login.salesforce.com/packaging/installPackage.apexp?p0=04t7F0000051Ca0


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
