---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Lightning Development Pro Tips
---
## Handy collection of key pointers from my 2years of experience of developing crazy solutions on top of Lightning Component Development Framework,

**Architeching Components**
1. Communication between components,
  - Using 2 way binding (Pass by Reference) with help of bound expressions {!}
  - If building component to be added via app builder to LeX utilize OOB events handled by one.app
  - Component Event - when a component needs to communicate with components above in containment hierarchy (e.g grandParent, Parent etc.)
  - Application Event - when a component needs to communicate with components not part of containment hierarchy (eg. siblings)
  -
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
1. Functions can be passed as a parameter, In example below the `onNext`, `onPrevious` functions defined in `shellComp` are passed as parameters to the embedded comp `paymentNavigationComp` as attributes,

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
2. Don\`t blindly use aura:If for conditional rendering, do consider just changing the visibility by simply using using css display:none/bloc, review the [Best Practices for Conditional Markup.](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/components_conditional_markup.htm)

3. To set a breakpoint in JavaScript code, use the debugger; statement, This causes your web browser to stop app execution and enables you to start debugging at the line where the statement was called.

4. Use Component Event when a child component needs to communicate  

5. Incases where some data need to be fetched from Database, 1st think of [force:recordData (LDS)](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/aura_compref_force_recordData.htm), only when you you hit any LDS limitations, then only go for Apex, that way you can keep your code minimal and efficient.

6. Cases when building dynamic components leveraging custom metadata you might run want to esacpe html stored in those metadata fields, use `<aura:unescapedHtml value="{!v.note.body}"/>` in such cases.

7. 




