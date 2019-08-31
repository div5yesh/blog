---
layout: post
logo: "🎒"
title:  "Well, the road to Javascript Documentation"
date:   2018-03-31
categories: Web
permalink: /web/well-the-road-to-javascript-documentation
description: Javascript | Documentation | YUI Doc | JS Doc
---

![](https://miro.medium.com/max/5472/0*68QxeRbiR49St37b.)

This article is to make you feel comfortable about documenting the code. But you still might not do it.

> Generating the documentation by parsing the code is more harmful than not having a documentation at all. It’s like having a dream and then slowly killing the hope.

---

In a world where “*Functionality comes first!*”, It’s tough to convince someone to spend the time to document the code. It requires the right tools for creation, regular maintenance and a pinch of motivation to achieve the documentation that is accurate and helpful.

Well to the shock of developers, “**the code itself is not the documentation**”, which they always fail to understand.

![](https://miro.medium.com/max/323/1*VkcaRCz759FCP9pFd9otuA.gif)

There are various tools available for document generation, JSDoc, ESDoc, YUI, Doxx to name a few. Pick one and get right to it. For it to be more practical and maintainable, documentation must always be a part of the build process. The choice of tools for documentation plays an important role in driving the motivation for writing it. So choose wisely.

Most of us developers are not great writers and usually go with the tools that generate documents by parsing the source code. This helps them to focus on the coding, and they don’t have to worry about the documentation. Just having a small description over every function or class, does the trick. To be honest that works pretty well.

> BUT…

At first, you start with enthusiasm and promise yourself to always document the code. As new and advanced features like ES6 are introduced in the language, you start experiencing FOMO, so what do you do? You incorporate these into your code but wait what about documentation. Oh! We have an automated tool, so relax. However, if the tool is not up to date with the language specifications, it fails to produce the sweet output that you love. Coz, who doesn’t like to document code. So you find a new tool that has the support of ES6, but now you are working on React, and the tool does not support JSX and just vomits errors. You will eventually become lazy and quit documenting.

Tools like JSDoc or ESDoc runs through your source code and generates the documentation based on the code it can parse. With javascript and its thousands of frameworks/libraries, and a number of coding patterns, running through source code is not a good idea. They will fail to recognize the syntaxes like JSX, arrow functions or you might get mysterious global properties that are actually not global since you have used module pattern.

Well, now you think of creating your own document generation tool and try to keep it up to date. But in a dark corner of your mind, you know what javascript is capable of. It’s always more. It’s always weird. And it always sucks. Not for me, of course.

> Your code might not compile or run, but you can still produce the documentation you need.

![That’s right.](https://miro.medium.com/max/600/1*6kDP3XCczkg3709ab4H8fg.gif)

Say hello to YUI, and it is language neutral. Just follow the YUI syntax for comments in any of your Javascript, Java, C# or whatever files and it will generate the lovely document. You can write the comment blocks in the way you want your code to make sense. YUI reads just the comment blocks and ignores the rest which makes the output of YUI predictable and reliable.

It’s easy to learn too, just look at the [YUIDoc Syntax Reference](http://yui.github.io/yuidoc/syntax/index.html). It acknowledges HTML, Markdown, cross-referencing and custom themes/templates, to supports all your documentation needs. This is what a complete documented code would look like and is written in a way to reflect the code structure.

<script src="https://gist.github.com/div5yesh/2d88e13dea3a13a7f2e3d790c054f6fa.js"></script>

---

If you are looking for other opinions, here they are:

[Choosing a JavaScript Documentation Generator – JSDoc vs YUIDoc vs Doxx vs Docco](https://www.fusioncharts.com/blog/jsdoc-vs-yuidoc-vs-doxx-vs-docco-choosing-a-javascript-documentation-generator/?source=post_page-----fe332f9f4766----------------------)

and there are points you would like me to argue, but if you try YUI, I won’t have to.

Originally posted: [medium.com/@div5yesh](https://medium.com/@div5yesh/well-the-road-to-javascript-documentation-fe332f9f4766)