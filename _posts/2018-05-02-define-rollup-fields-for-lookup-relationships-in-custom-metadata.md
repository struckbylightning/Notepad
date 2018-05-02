---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Define Rollup Fields for Lookup Relationships in Custom Metadata
---
## Declarative Metadata base Rollup Summaries,

This code leverages an excellent open source library by [Abhinav Gupta](https://twitter.com/abhinavguptas) and is a Metadata variant of [Andrew Fawcett\`s](https://twitter.com/andyinthecloud) [DLRS](https://github.com/afawcett/declarative-lookup-rollup-summaries) 

Problem that we are solving,

- 25 rollup summary fields allowed per object on master detail relationships
- Rollup child sobject records part of a lookup relationship. Native rollup summary fields are not available on LOOKUP relationships.
- Deploying the metadata configs with ease without use of data loader.

As always first thing first, here\`s the link to Unmanage Package ()