---
layout: post
published: false
mathjax: false
featured: true
comments: true
title: Top 10 Salesforce Mantras - Getting Salesforce DataModel Right
---
## Getting Salesforce DataModel Right

There’s a thin line between having your salesforce end up as a glorified dumb database where data entry is considered as an overhead v/s a smart realtime insight generating database where data entry is considered as worthwhile given the analytics it generates.

If above sounds familiar to you and you are getting anxious to know what’s that secret salesforce sauce that causes all the difference then come aboard this post is just for you,

As someone rightly said, “You Are Only as Strong as Your Foundation”, Inorder to realise your Salesforce investments worth, we need to get our foundation which in Salesforce\`s case is Data Model design RIGHT.

Before we hop on to the Top 10 secrets of getting salesforce data model design it right, Let\`s reiterate why is DataModel Design that important ,

Why,
1. Data model designing is critical and understanding reporting requirements UP-FRONT is a key success factor.
2. Easy configuration is a double edged sword and Most of the times data models are setup by accidental admins or junior functional consultants who not necessarily understands the impacts of design they take on the end result of salesforce aligning to the overall vision/analytic dreams/security & performance needs.
3. Traditional data model design principles where normalization is the norm doesn\`t work in salesforce as here calculated decisions needs to be made by weighing tradeoff between user-experience (ease of inputting data) vs reporting requirements and deciding whether to normalize or denormalize.
4. Salesforce is not a data warehouse (nor do they want to be).  The recommended data strategy is to have the data you need and to remove the data you don’t.  While that sounds like a pretty simple concept it is much more difficult to realise.

So here are the **Top 10 Secrets to smartly designing in salesforce database**

Inorder to understand when to go Flat(DeNormalize) or not to go flat(Normalize), Let\`s consider below user stories,
![Datamodel user stories.png]({{site.baseurl}}/images/Datamodel user stories.png)

1. Let\`s take the First user story to understand when not to go flat,

Here Data can be modelled in below two ways,

![Sales Rep Sales Split]({{site.baseurl}}/images/Screen%20Shot%202018-09-12%20at%2011.06.06%20am.png)

Focus of this userstory is on the analytics needs, so here from reporting perspective, here it make sense to store Sales Rep\`s split % into seprate table of it\`s own (normalize/not go falt) because, now we can easily build a report to generate metrics like commision share per rep per quarter in minutes time by using report type Sales with Sales Rep Splits and grouping columns by sales rep and columns by sales date(grouped by quarter).

2. Now let\`s take the second user story to understand when not to go flat,

Here also Data can be modelled in below two ways,

![Lead Contact Numbers]({{site.baseurl}}/images/Screen%20Shot%202018-09-12%20at%2011.14.42%20am.png)![Screen Shot 2018-09-12 at 11.14.42 am.png]({{site.baseurl}}/images/Screen Shot 2018-09-12 at 11.14.42 am.png)

But here, we don\`t have any specific analytic needs on contact numbers instead here the focus is on the user experience in entering and viewing the data, so here it makes sense to go flat and simply create fields of phone datatype on Lead itself, so that those fields can then be easily added to the list views built on Lead object


1. Go top to botton Vision/Pain Points - Reporting/Integration Needs - Data Model
2. Go Flat but just not to flat, do a smart tradeoff between 
3. Design for referential integretiy, so data needs to exist only once 
4. Segment object using record type
5. [Rename Object, Tab, and Field Labels] to make your users feel at home 
6. Lookup vs master detail
7. Understand cardinality 1:1, 1:n & 1:1
8. Get into continuous refactoring mindset, what is right today might not be right tomorrow so don\`t be afraid to refactor/redesinging your datamodel to suit your needs, and use tools like dataloader to massage your existing data to match new data model design
9. Indexes and External Ids
10. Be thoughtful about names & Help out your users using help text and descriptions

Most importantly 

Resources to learn more than just tips and become a Pro at scalable datamodelling.
1. [Data Modelling Basics - Trailhead Module](https://trailhead.salesforce.com/en/modules/data_modeling)
2. [Build a Data Model for a Recruiting App - Trailhead Project](https://trailhead.salesforce.com/en/projects/build-a-data-model-for-a-recruiting-app)
