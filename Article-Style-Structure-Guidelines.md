---
layout: page
title: Article Style and Structure Guidelines
permalink: Article-Style-Structure-Guidelines
---

#Article Style and Structure Guidelines

The Kaltura VPaaS Developer Site is using [Jekyll engine](http://jekyllrb.com/) and markdown syntax as the basis of the articles.
To learn about Markdown basics and how to use the format, please read: [GitHub markdown basics](https://help.github.com/articles/markdown-basics/).

The Kaltura VPaaS Developer Site extends the default markdown with Onebox embeds as follow:

To add Kaltura videos: 
`
{% onebox http://www.kaltura.com/tiny/nex76 %}
`

To add YouTube videos: 
`
{% onebox https://www.youtube.com/watch?v=Owh8nBt4QSs %}
`



For additional reading on the Markdown flavor we use read: [GitHub flavored markdown](https://help.github.com/articles/github-flavored-markdown/).

A nifty tool to help you to see how your markdown looks as you create it: http://dillinger.io/

##Tips for Creating Great Content

* Start with an introduction by answering the question “what will be learned in this document”.
* Think about the steps that will get your reader from A to Z in the fastest way possible while following Kaltura best-practises.
* All sections should be separated by H2 headings (##), subsections by H3 headings (###) and so on.
* **Don’t forget to spell check!**

Remember that your audience is developer-focused, therefore:
* Include code snippets where relevant
* Reference API end-points where applicable
* Reference github/bitbucket repos where applicable
* Clearly explain the required workflows to achieve an end-result


##How to contribute and help improve the documentation

* Every topic category (e.g. Content Ingestion & Acquisition) has a respective directory under this repository.
* All markdown documents should be saved in this repository under the respective topic category directory.
* When naming your files, please use the same convention as the other documents on this repository:
 * Lower case
 * Spaces converted to dash
 * Filename always ends with `.md` as the file extension
 * The filename should always reflect the title of the article (i.e. H1 == filename)
* Follow the guidelines for article header notation as per below


##Article header notation
At the top of every markdown file, you will find the below notation. This designates the type of page and its location in the website menu.

```---
layout: page
title: VPaaS Website Sample Article
permalink: /introduction/vpaas-website-sample-article
type: header
---
```

The fields and options are:  

* `layout:` this is static, and should always be set to `page`
* `title:` this is the title of the page (correlates to `<title></title>` tag in HTML)
* `permalink:` the respective **relative** link to the rendered page on the website (e.g. `/introduction/vpaas-website-sample-article` will be: http://vpaas.com/introduction/vpaas-website-sample-article)
* `type:` this indicates that this page should be included in the website menu. If this page should not be on the menu, this parameter should not be specified at all.