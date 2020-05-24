---
title: Markdown Notes
date: 2018-07-06 12:28:12 -0500
categories: [Tools]
tags: [markdown]
---

These markdown notes are referenced from [Markdown Basics](https://daringfireball.net/projects/markdown/basics), [Github Guides](https://guides.github.com/features/mastering-markdown/) and [Writing on Github](https://help.github.com/categories/writing-on-github/).

Click here for this [markdown source file](https://raw.githubusercontent.com/yuyang-yy/yuyang-yy.github.io/master/_posts/2018-07-06-Markdown-Notes.markdown)

# HEADERS
There are two styles of headers: Setext and atx.

### Setext (Use = or -)

> A First Level Header
====================

> A Second Level Header
---------------------

### atx (Use 1-6 hash marks(#) at the beginning of the line)

> ### Header 3 

> ##### Header 5

# BLOCKQUOTE

> This is a blockquote.
>
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote.


# PHRASE EMPHASIS
Markdown uses asterisks and underscores to indicate spans of emphasis.

+   Some of these words *are italic*.

+   Some of these words _are italic also_.

+   Use two asterisks for **bold**.

+   Or, if you prefer, __use two underscores instead__.


# LISTS
Unordered lists use asterisks, pluses, and hyphens(**, +, -) as list markers. They are interchangeable.

*	Apple
* 	Orange
* 	Grape

+ 	Banana
+ 	Mango
+ 	Watermelon

- 	Pineapple
- 	Strawberry
- 	Cherry

Ordered lists use regular numbers folllowed by periods as list marker.

1. 	Baby
2. 	Teenager
3. 	Adult
4. 	Oldman

To input multiple lines in one single item: insert blank lines between lines and use 1 tab for each line.
* 	A list item

	with multiple lines.
	
	another line
	
*	Another list item.
*	The third item.

# LINKS

There are two styles for creating links: inline and reference.

Inline style:

*   This is [Bing](https://cn.bing.com)

Reference style:

*   I get 10 times more traffic from [Google][1] than from
    [Yahoo][2] or [MSN][3].

    [1]: http://google.com/        "Google"
    [2]: http://search.yahoo.com/  "Yahoo Search"
    [3]: http://search.msn.com/    "MSN Search"

Or, we can use name as index.
*   I start my morning with a cup of coffee and
    [The New York Times][NY Times]. And I do exercises on [LeetCode][LeetCode].

    [ny times]: http://www.nytimes.com/
    [LeetCode]: https://leetcode.com


# IMAGES

Image syntax is very much like link syntax.

When the image source is a link:
![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

When the image source is one folder:
![Image of bulb](/assets/img/bulb.jpg)

Align two pictures in one row: (use pipe)
![](/assets/img/all-at-once.jpg) | ![A little every day](/assets/img/a-little-every-day.jpg)

# CODE

The following are `code blocks`.

Either simply indent a tab.

	def __init(self):
		self.height = 160

Either use backticks.
```
def __init__(self):
    self.height = 160
```

Either use Syntax highlighting (GFM).

```python
def __init__(self):
	self.width = 20
```

# TASK LISTS (GFM)
- [ ] this is an incomplete iterm
- [x] this is a complete item


# TABLES (GFM)

First Header | Second Header
------| ------
Content from cell 1 | Content from cell 2
First column | Second column


# Tips for Markdown
1. Use Markdown TOC extension in VSCode to insert table of contents automatically.
