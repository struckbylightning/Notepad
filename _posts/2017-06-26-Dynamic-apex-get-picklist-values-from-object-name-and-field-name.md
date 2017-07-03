---
layout: post
published: true
title: Get picklist field values from a given object and field name using Dynamic Apex
mathjax: false
featured: true
comments: true
headline: Dynamic Apex Snippet
description: Dynamic Apex Snippet to get picklist values
categories: Apex
tags:   
  - dynamic apex
  - reusable code
---
```java
public static List<String> getPicklistFieldValues
							(String objectName, String pickListFieldName){
        List<String> picklistValues = new List<String>();
        SObjectType objectType = Schema.getGlobalDescribe().get(objectName);
        List<Schema.PicklistEntry> pick_list_values = objectType.getDescribe()
                                                       .fields.getMap()
                                                       .get(pickListFieldName)
                                                       .getDescribe().getPickListValues();
        for (Schema.PicklistEntry aPickListValue : pick_list_values) {                   
            picklistValues.add(aPickListValue.getValue()); 
        }
        return picklistValues;
    }
```