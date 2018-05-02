---
layout: post
published: true
title: 'Reusable InputPicklist Lightning-Component for free :)'
mathjax: false
featured: false
comments: true
headline: Reusable InputPicklist Lightning-Component
description: Reusable InputPicklist Lightning-Component
categories:
  - Lightning components
tags: 'lightning component,dynamic apex,reusable code, Freebies'
---
Do you love lightning way of componentizing things, but miss good\`ol Visualforce out of box way of handling picklist input field just by using **<apex:inputField/>**, worry no more, will show you how to create a reusable lightning component named *c:inputPicklist* to achieve the same.


Example usage:
```html
<c:LIInputPicklist 
	class="form-control slds-input"
    required="false" object="Contact"
    label="{!$Label.c.Contact_Salutation}"
    value="{!v.Contact.Salutation}"
    field="Salutation"/>
```
Important Attributes
- value(String)     : Variable to store/pass the inout selected
- label(String)     : Label to be displayed for the picklist field
- field(String)     : Api name of the picklist field
- object(String)    : Name of the object
- labelClass(String): List of classes to be applied on label separated by .space.
- Class(String)     : List of classes to be applied on picklist dropdown separated by space.
