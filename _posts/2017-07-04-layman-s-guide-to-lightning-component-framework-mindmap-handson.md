---
layout: post
published: true
mathjax: false
featured: true
comments: true
title: Layman`s guide to Lightning Component Framework (Mindmap + Handson)
tags: lightning component guide layman salesforce begineer attributes servercall
categories:
  - lightning
---
## Here\`s a simple laymans guide to learning Salesforce\`s Lightning Component Framework

Best way to learn, is to start building simple components which can help us understand the basics which power the lightning framework, so let\`s straight away dive into code.

### Let\`s start by building a simple wishlist app which will help us list down the items we desire along with the cost to buy.

To start, let\`s build a simple static component named `aWishListItem.cmp` (Go to Developer Console-> File -> New Lightning component -> name it as aWishListItem
```html
<aura:component>
  <h2>Item Name: <ui:outputText value="Fidget Spinner"/></h2>
  <h3>Will cost: <ui:outputCurrency currencySymbol="₹" value="250"/></h3>   
</aura:component>
```
 Now let\`s create new container component which will hold our wishes named `wishlist.cmp`
```html
<aura:component >
    <c:wishlistItem/>
</aura:component>
```
And then inorder to preview our wishlist.cmp let\`s add it to a new application named wishlistApp.app
```html
<aura:application >
    <c:wishList/>
</aura:application>
```
Here\`s the preview of our application built so far.
![staticWishList.gif]({{site.baseurl}}/images/staticWishList.gif)

### Offcourse you would not be creating a component to display one wishlist item and make another coponent when you want to display another fruit, so how you do you make fruit.cmp **dynamic**??

And that brings to our first topic,
## 1. Using Attributes and Expression.
We will leverage aura:attributes which are the properties that we pass in to our component to customize its behaviour (what it renders), let\`s look at updated version of our previous components.
`wishlistItem.cmp`
```html
<aura:component>
    <aura:attribute name="itemName" type="String"/>
    <aura:attribute name="cost" type="String"/>
    <div>
        <h2>Item Name: 
  			<ui:outputText value="{!v.itemName}"/>		  </h2>
    	<h3>Will cost: 
  			<ui:outputCurrency currencySymbol="₹" 	                              value="{!v.cost}"/>
  		</h3> 
        </div>
</aura:component>```
`wishlist.cmp`
```html
<aura:component >
    <c:wishlistItem itemName="Fidget Spinner" cost="250"/>
    <c:wishlistItem itemName="Peace of Mind" cost="0"/>
</aura:component>
```
Observe,
1. {!...} is called expression language syntax in simple words whatever is there inside the curly brace syntax instead of just printing them framework will treat them specially and evaluate them instead, thereby replace it with correponding attributes value.
2. {!v.} here v represt\`s View also called as value provider, holds all the attribute values.

Here\`s the much awaited preview of our awesome `wishlist.app`
![attributeWishList.gif]({{site.baseurl}}/images/attributeWishList.gif)

Now that we understand how to use attributes, let\`s look at few examples of expressions and what they evaluate to,

..........
** Company 'Dreams come true' is planning to expose our wishlist application to their employees so that they can help make them come true, let\`s create custom object named WishList_Item__c with fields Name (Text), Cost__c (Currency) & Dreamer__c (User Lookup) so that employee\`s wishes can be persisted in salesforce database for company to act upon.**

Create few sample wishlist items records for user 'Nikunj',
[Screenshot here]

Now when Nikunj opens up the wishlist.app he should see the couple of items created above, how can we achieve it??
## 2. Communicating with Server

```
`APXWishlistController.apxc`
```java
public List<WishList_Item__c> getMyWishListItems(){
  return [Select Name, Cost__c from WishList_Item__c where Dreamer__c =: UserInfo.getUserId()];
  }
```

`wishlist.cmp` attribute to store array of wishitems returned from server and init handler to perform the logic to call server method to query and get related wishlist items for logged in user and set components attribute with the same 
```html
<aura:component >
    <aura:attribute name="wishlistItems" type="WishList_Item__c[]" default="false"/>
    <h1>My Wish List</h1>
    <aura:handler name="init" value="{!this}" action="{!c.getMyWishes}"/>
    <aura:iteration var="item" items="{!v.wishlistItems}">
        <c:wishlistItem itemName="Fidget Spinner" cost="250"/>
    </aura:iteration>
</aura:component>    
```
`wishlistController.js` -- function getMyWishes to call apex method getMyWishListItems'
```js
({
	getMyWishes : function(component, event, helper) {
		//Call APXWishlistController\`s getMyWishListItems
        //Set wishlistItems
	}
})


### Let\`s add some css to make our wishlist application look as pretty as our wishes.
## 3. Adding CSS

-----------

## 4. Event handlers (Add Edit Remove button code)

## 5. Communicating data between components
- `OpenTheDoor.app` (container for holding the guy & the door)          
```html
	<!-- OpenTheDoor.app (container for holding the guy & the door)-->
```
		- `guy.cmp` (On click of "Knock Knock" fires openDoor Event)        
```html
    	<!--guy.cmp (On click of 'Knock Knock!' fires openDoor Event)-->
```
		- `openDoor.evt` (fired when guy knocks the door)         
```html
        <!--openDoor.evt (fired when guy knocks the door)-->       
```
		- `door.cmp` (Listens(registers) to the openDoor event and accordingly acknowledges)         
```html
        <!--door.cmp (Listens(registers) to the openDoor event and accordingly acknowledges-->
```  
  <!--<embed src="{{site.baseurl}}/images/lightningComponentMindMap.pdf" width="800px" height="800px" />
_Mind Map_-->
