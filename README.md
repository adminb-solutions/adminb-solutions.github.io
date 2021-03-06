# AdminB solutions blog

The blog uses [Jekyll](https://jekyllrb.com/) for static page generation and gets published through [Git Hub Pages](https://pages.github.com/). Only changes made to the **master** branch are published. 

## Running locally

You can view a local copy of the blog, useful to view other branches, make changes, test things. 
You could install your own copy of Jekyll but it is easier to just use Docker. The repository is already set up to use a Linux Docker container. 

Simply run ```docker-compose up -d``` (or use the commands from the [Docker extension in Visual Studio Code](https://code.visualstudio.com/docs/languages/dockerfile#_docker-commands)) from the root of the project. The site will be available in ```localhost``` on your host machine.

Changes to the source files (new posts, pages, changes, etc.) are automatically picked up. You will have to reload the page in the browser though. (Unfortunately LiveReload requires more extensive configuration using a Windows host).

When you have finished simply ```docker-compose down``` to tear everything down.

## Creating content

You can add new content either as markdown (MD) files or HTML. 

**Important:** all files need to be in UTF-8 with no BOM.

Files require some *Front Matter* (i.e. some YML formatted header). Front matter is marked by three hyphens. So at a minimum any file that needs to be processed by Jekyll should start:

``` html
---
---
rest of your HTML or MD file
```

Between the hyphens you can add extra properties for the document. For example when creating a blog post:

``` html
---
author: John Writer
title: An awesoem post
category: sitecore
tags: demo adminb test
---
```

Post should be placed in the *_posts* folder and named with the format ```yyyy-mm-dd-title.ext```. They should include a title property.

## Optional attributes

The blog posts Front Matter can include extra optional properties:

- Author
- Category: a post can only be assigned a single category. It will affect the url: /
- Tags: supports multiple values

In order to support lists with all the posts included in a particular tag or category a page must exist in the corresponding location. For categories: ```/category/<name-of-category>``` and for tags ```/tag/<name-of-tag>```. Those files as a minimum must contain an empty front matter.

``` frontmatter
---
---
```

## Adding code snippets

In order to insert code snippets with nice syntax colouring use the following tags:

``` liquid
{% highlight csharp linenos %}
public class Test
{
    public Test() {}
    public void DoesNothing()
    {
        var i = 0;
    }
}
{% endhighlight %}
```

There are over [70 languages](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers) available. You can add the `linenos` directive to show line numbers.

Alternatively you can also use the usual markdown syntax of three back-ticks:

    ```csharp
    public void static Main()
    {
    }
    ```

## Modification flow

Since only changes made to the master branch are published in GitHub Pages, you could create your new blogpost in a separate branch and test it locally. When it is ready to be published, simply do a PR (or simply a merge) against master.

Alternatively you could also create draft post in a _drafts folder. These won't be picked up by Jekyll in production, but they will be published by the local instance inside the Docker container.