---
title: "Facebook OG Tags"
date: 2020-08-06T13:05:13-04:00
draft: false
---

![Code 2020](/img/code-202-png) 

Facebook introduced the [https://ogp.me/](Open Graph) format however long ago it was, I am not sure. For me, as a website developer and content creator, the OG format is always one of those things I forget about until I've published the site and go to share the first post (note to self to add that to the check list). When Facebook does not parse my content I get my sad face on because yet again I have forgotten to add the OG tags. 

This site is generated using [https://gohugo.io](Hugo) and I use the [Blackburn](https://github.com/yoshiharuyamashita/blackburn) theme as my base. I like the layout and the code is easy to extend. As a matter of personal preference I've always liked minimalist websites. A minimalist site is about the content and nothing else. 

That being said, there is a lot of room for improvement and one of those improvements is adding the og tags. This is how I did it by adapting this [gist](https://github.com/RickCogley/RCC-Hugo2015/blob/master/layouts/partials/seo-og.html#L6)  by Rick Cogley for this theme; however this method will work for any theme because we use [partials](https://gohugo.io/templates/partials/) to pull this off. So lets get started.

Create a file called seo-og.html in your theme's partial/ directory. 

In the seo-og.html file place this code:

```html
{{ "<!-- ENTERING partial seo-og.html (open graph) -->" | safeHTML }}
{{ $baseurl := $.Site.BaseURL }}
{{ if .IsPage }}
<!-- Required Open Graph Info -->
<meta property="og:title" content="{{ .Title }}{{ if ne .Title .Site.Title }} : {{ .Site.Title }}{{ end }}" />
{{ with .Params.images }}{{ range first 6 . }}<meta property="og:image" content="{{ if in . "http" }}{{ . }}{{ else }}{{ $baseurl }}{{ . }}{{ end }}" />
{{ end }}
{{ end }}
<meta property="og:url" content="{{ .Permalink }}" />
<!-- Optional Open Graph Info -->
<meta property="og:description" content="{{ if .Description }}{{ .Description }}{{ else }}{{if .IsPage}}{{ .Summary }}{{ end }}{{ end }}" />
<meta property="og:locale" content="{{ if .Params.locale }}{{ .Params.locale }}{{ else }}en_US{{ end }}" />
{{ with .Params.audio }}<meta property="og:audio" content="{{ . }}" />{{ end }}
{{ with .Params.videos }}{{ range . }}
<meta property="og:video" content="{{ . }}" />
{{ end }}
{{ end }}
{{ with .Site.Params.title }}<meta property="og:site_name" content="{{ . }}" />{{ end }}
{{ if eq .Type "post" }}
<!-- Required Open Graph Info -->
<meta property="og:type" content="article" />
<!-- ARTICLE Open Graph Info -->
<meta property="article:published_time" content="{{ .PublishDate  }}"/>
<meta property="article:modified_time" content="{{ .Date }}"/>
<meta property="article:author" content="{{ $.Site.Social.twitter }}" />
<meta property="article:publisher" content="{{ $.Site.Social.twitter }}" />
<meta property="article:section" content="{{ .Section }}" />
{{ with .Params.tags }}{{ range first 6 . }}<meta property="article:tag" content="{{ . }}" />
{{ end }}
{{ end }}
<!-- If it is part of a series, link to related articles -->
{{ $permalink := .Permalink }}
{{ $siteSeries := .Site.Taxonomies.series }}
{{ with .Params.series }}{{ range $name := . }}
    {{ $series := index $siteSeries $name }}
    {{ range $page := first 6 $series.Pages }}
        {{ if ne $page.Permalink $permalink }}<meta property="og:see_also" content="{{ $page.Permalink }}" />{{ end }}
    {{ end }}
{{ end }}{{ end }}
{{ else if eq .Type "aboutpage" }}
<!-- PROFILE Open Graph Info -->
<meta property="profile:first_name" content="{{ .Params.og.ogfirstname }}" />
<meta property="profile:last_name" content="{{ .Params.og.oglastname }}" />
<meta property="profile:username" content="{{ .Params.og.ogusername }}" />
<meta property="profile:gender" content="{{ .Params.og.oggender }}" />
{{ end }}
{{ end }}
{{ "<!-- LEAVING partial seo-og.html -->" | safeHTML }}
```

​	

You can save and closet that. You are done with it.

Now open your config.yaml and add this lines to the end. Change the values.

```yaml
[og]
	
    ogfirstname = "Norman"
    oglastname = "Bauer"
    ogusername = "simulacra10"
    oggender = "male"
```



Finally the very last thing you need to do is add this one line to the head of you your index.html



```
{{ partial "seo-og.html" . }}
```



That's it! Now when you render your hugo site you will see the OG meta tags. 