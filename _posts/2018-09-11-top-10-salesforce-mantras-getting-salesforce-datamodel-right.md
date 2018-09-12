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

Before we hop on to the Top 10 secrets of getting salesforce data model design it right, Let\`s reiterate **WHY** DataModel Design so important ,
1. Data model designing is critical and understanding reporting requirements UP-FRONT is a key success factor.
2. Easy configuration is a double edged sword and Most of the times data models are setup by accidental admins or junior functional consultants who not necessarily understands the impacts of design they take on the end result of salesforce aligning to the overall vision/analytic dreams/security & performance needs.
3. Traditional data model design principles where normalization is the norm doesn\`t work in salesforce as here calculated decisions needs to be made by weighing tradeoff between user-experience (ease of inputting data) vs reporting requirements and deciding whether to normalize or denormalize.
4. Good outcomes and bad outcomes start with the Data Model, Your Physical Data Model in Salesforce directly influences what is possible with Declarative Features vs what requires Custom  Development.


So here are the **Top 10 Secrets to smartly designing in salesforce database**

1. Go top to botton while designing a data model, first understand the Vision/Challenges/Pain Points, then understand Reporting/Integration/Security/Performance Needs and then finally design and build the Data Model.

2. Inorder to understand when to go Flat(DeNormalize) or not to go flat(Normalize), Let\`s consider below user stories,

    ![Datamodel user stories]({{site.baseurl}}/images/Datamodel user stories v2.png)

    Let\`s take the First user story to understand when not to go flat, Here Data can be modelled in     below two ways,

    ![Sales Rep Sales Split]({{site.baseurl}}/images/Sales_Rep_Sales_Split.png)

    Focus of this userstory is on the analytics needs, so here from reporting perspective, here it make sense to store Sales Rep\`s split % into seprate table of it\`s own (normalize/not go falt) because, now we can easily build a report to generate metrics like commision share per rep per quarter in minutes time by using report type Sales with Sales Rep Splits and grouping columns by sales rep and columns by sales date(grouped by quarter).

3. Now let\`s take the second user story to understand when not to go flat, Here also Data can be modelled in below two ways,

    ![Lead Contact Numbers]({{site.baseurl}}/images/Lead_Contact_Numbers.png)

    But here, we don\`t have any specific analytic needs on contact numbers instead here the focus is on the user experience in entering and viewing the data, so here it makes sense to go flat and simply create fields of phone datatype on Lead itself, so that those fields can then be easily added to the list views built on Lead object

4. Understand cardinality in salesforce

5. There are two ways to build relationship between objects, use below table to understand when to use what,

6. Let\`s consider you have built lookup realtionship but still desperately need rollup fields, worry not there are many appexchange packages like [Rollup Helper](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N30000009i3UpEAI) and open sourced code projects like [the one here which I build](https://struckbylightning.github.io/2018/05/apex/freebies/define-rollup-fields-for-lookup-relationships-in-custom-metadata) available for your rescue.

7. Understand when to leverage standard object v/s when to build a custom object, using below pointers

 * Start with, Understanding the Salesforce Standard Objects and fields and their ‘Special Features’
  * If it walks like a duck and talks like a duck, its probably a Duck.
  * If it’s called a Duck but it walks like a chicken and talks like a chicken, its  probably a Chicken.
  * For example,
   * ‘We need to keep quotes, but we won’t be using Opportunities, or  Products or be sending Quote’s out of Salesforce’
    * It’s probably not the Quote object
   * ‘We need to track Jobs, with email interactions and pass it back and forth between people ’
    * I think you mean ‘Case’.

8. Define the user stories in a way that expresses a requirement in a way that provides context and justification
Usually in a standard form:
‘AS A \<Job Role\> I WANT to <some business process> SO THAT I can <achieve  some outcome>’
  For example refer #2
9. Rename [Object, Tab, and Field Labels](https://help.salesforce.com/articleView?id=customize_rename.htm&r=https%3A%2F%2Fwww.google.com.au%2F&type=5) to make your users feel at home 


6. Design for referential integretiy, so data needs to exist only once 
4. Segment object using record type
5. 
7. Understand cardinality 1:1, 1:n & 1:1
8. Get into continuous refactoring mindset, what is right today might not be right tomorrow so don\`t be afraid to refactor/redesinging your datamodel to suit your needs, and use tools like dataloader to massage your existing data to match new data model design
9. Indexes and External Ids
10. Be thoughtful about names & Help out your users using help text and descriptions

Most importantly 

Resources to learn more than just tips and become a Pro at scalable datamodelling.
1. [Data Modelling Basics - Trailhead Module](https://trailhead.salesforce.com/en/modules/data_modeling)
2. [Build a Data Model for a Recruiting App - Trailhead Project](https://trailhead.salesforce.com/en/projects/build-a-data-model-for-a-recruiting-app)
