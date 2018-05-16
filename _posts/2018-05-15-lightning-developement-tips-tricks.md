---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Lightning Developement Tips & Tricks
---
Test
```html
<!-- shellComp.cmp  -->
<aura:component>
	<c:paymentNavigationComp onPrevious="{!c.onPrevious}" onNext="{!c.onNext}"/>
</aura:component>
```

```js
/* ShellCompController.js */
{
  onNext : function(component, event, helper) {
    //Logic
  },
  onPrevious : function(component, event, helper) {
    //Logic
  }
}
```

```html
<!-- paymentNavigationComp.cmp  -->
<aura:component>
  <aura:attribute name="onPrevious" type="Aura.Action"/>
  <button class="slds-button slds-button--neutral" onclick="{!v.onPrevious}">Previous</button>
</aura:component>
```

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