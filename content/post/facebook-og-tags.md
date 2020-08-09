---
title: "Facebook Og Tags"
date: 2020-08-06T13:05:13-04:00
draft: true
---

Facebook introduced the [https://ogp.me/](Open Graph) format however long ago I am not sure. For me, a website developer and content creator, the OG format is always one of those things I forget about until I've published the site and go to share the first post (note to self to add that to the check list). When Facebook does not parse my content I get my sad face on because yet again I have forgotten to add the OG tags. 

This site is generated using [https://gohugo.io](Hugo) and I use the [Blackburn](https://github.com/yoshiharuyamashita/blackburn) theme as my base. I like the layout and the code is easy to extend. As a matter of personal preference I've always liked minimalist websites. A minimalist site is about the content and nothing else. 

That being said, there is a lot of room for improvement and one of those improvements is adding the og tags. This is how I did it for this theme but this method will work for any theme because we use [partials](https://gohugo.io/templates/partials/) to pull this off. So lets get started.

Create a file called seo-og.html in your theme's partial/ directory. 

