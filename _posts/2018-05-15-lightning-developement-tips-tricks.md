---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Lightning Developement Tips & Tricks
---
## Handy collection of key pointers from my experience of developing lightning components from past couple of years,

**Architeching Components**
#Reusable
#Scalable
#Modular
#FAST
#Accessible

#Using Helper
#Inheritance
#Returning from Server
#Error Handling
#Comps for App Builder

**Debugging & Prerformance**
#Lightining Linter
#Lightning Inspector & Community something

**Developement Tips**
1. Functions can be passed as a parameter  
  *In example below the onNext, onPrevious functions defined in shellComp are passed as parameters to the embedded comp paymentNavigationComp  
  ---------------shellComp.cmp-------
  
```html
<aura:component>
	<c:paymentNavigationComp onPrevious="{!c.onPrevious}" onNext="{!c.onNext}"/>
</aura:component>
```  
---ShellCompController.js---
```js
{
  onNext : function(component, event, helper) {
    //Logic
  },
  onPrevious : function(component, event, helper) {
    //Logic
  }
}
```  

-------------------------paymentNavigationComp.cmp---------------  
```html
<aura:component>
  <aura:attribute name="onPrevious" type="Aura.Action"/>
  <button class="slds-button slds-button--neutral" onclick="{!v.onPrevious}">Previous</button>
</aura:component>
```