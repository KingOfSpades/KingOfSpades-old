---
title:  "Using inline dataview query's in markdown tables"
date: 2022-03-10
toc: true
mermaid: true
categories: [Obsidian]
tags: [productivity, dataview,] # TAG names should always be lowercase
---

# Inline dataview query's for Markdown tables
One of the best (in my opinion) plug-ins if you're using [Obsidian](https://obsidian.md) is [Dataview](https://github.com/blacksmithgu/obsidian-dataview). Dataview enables you to query your markdown files based on links, tags and custom Fontmatter atributes. For example, to create a list in Obsidian from all pages containting the tag `#Tag1` you could use:

```yaml
list from #Tag1
```

More examples can be found in the official documentation: [https://blacksmithgu.github.io/obsidian-dataview/](https://blacksmithgu.github.io/obsidian-dataview/).

# Background, PARA and my vault
I've been using the PARA method for almost a year now in Obsidian, Things3 and in my File Storage. I love the ease of PARA and how easily I can organize and retrive data using this system. I also added the concept of a Inbox to the system where notes, tasks and files can be stored before being procesed in to the PARA system.

## PARA in Obsidian
I use a series of backlinks to link all my notes and resources to a PARA Area. I use a index page to navigate to Projects, Areas and Resources. To add more imerssion to my flow I wanted to create counters that show how many Inbox notes I have that need processing and how many links there are to my different PARA Indexes.

# Using inline querys
To create a dataview view you use a code fence. But you can also create *inline* querys to render content in a sentence or in a table. In my example I will do the later. Please make sure you have updated to a relevant version of Dataview. In my case I couldn't get inline querys to work because I was stuck on an old version.

## Enabeling inline querys
After installaing Dataview you will need to enable inline querys in the settings. You can find this under `Plugin options > Dataview > Enable Inline JavaScript Queries`:

![](../assets/images/screen-20220407114006.png | =250x)

## Setting up frontmatter
To make my querys work I will query on 3 attributes:
- A backlink, to link to a MOC
- A tag, to indicate the Type of de note
- A custom frontmatter attribute called `status` to set a MOC as `Active` or `Archived`

I use the following frontmatter:

```yaml
---
status: Active
tags:
- Type/MOC 
- Evergreen/Seedling 
- PARA/Area
---
```

For the inbox counter we don't need any frontmatter code because we will count the files in a folder.

## Building a query
Let's start with an easy one, the Inbox folder count. I use the following query:
```dataview
`$= dv.pages('"0 INBOX"').length`
```

This will count all files in the folder `0 INBOX`.

To count the links to my different MOC's (Map Of Content) I use the following 4 querys:

- All active Projects
  ```dataview
  `$= dv.pages("[[MOC-PROJECT]] and #Type/MOC").where(p => p.status == "Active").length`
  ```
- All active Area's
  ```dataview
  `$= dv.pages("[[MOC-AREA]] and #Type/MOC").where(p => p.status == "Active").length`
  ```
- All active Resources
  ```dataview
  `$= dv.pages("[[MOC-RESOURCE]] and #Type/MOC").where(p => p.status == "Active").length`
  ```

  ```dataview
  `$= dv.pages("[[MOC-ARCHIVE]] and #Type/MOC").where(p => p.status == "Archive").length`
  ```

## Using it in a table