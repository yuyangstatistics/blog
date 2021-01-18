---
title: html and css
date: 2018-12-23 12:28:12 -0500
categories: [Programming]
tags: [html]
---

## HTML Notes
The notes for the edX course: Programming for the Web with Javascript can be found in the following links.
- [Week1 html]({{site.baseurl}}/assets/files/html-learning.html). Or you could directly view the [Week1 source code](https://raw.githubusercontent.com/yuyang-yy/materials/master/html/index.html). 
- [Week2 DOM html]({{site.baseurl}}/assets/files/week2-dom.html) and [Week2 jQuery html]({{site.baseurl}}/assets/files/week2-jquery.html).



## JavaScript Notes
The notes of a YouTube online course [Learn JavaScript - Full Course for Beginners](https://www.youtube.com/watch?v=PkZNo7MFNFg&t=11105s) is [here]({{site.baseurl}}/assets/files/jquery.js).

## HTML
``` html
<!DOCTYPE html>
<html>
    <head>
        <title>Title</title>
        <link href=" " type="text/css" rel="stylesheet">
    </head>
    <body>
        <h1>Head 1</h1>
        <h2>Head 2</h2>
        <p>This is a paragraph.<span>a part in the paragragh.</span> Inside this paragragh, we could use <em>italics</em> and <strong>bold</strong> to emphasize words.</p>
        <a href="">a link</a>

        <!-- image -->
        <img src="" alt=""/>

        <!-- video -->
        <video src="" controls></video>

        <!-- tables -->
        <table>
            <thead>
                <th scope="col"></th>
            </thead>
            <tbody>
                <th>a</th>
                <td>1</td>
            </tbody>
            <tfoot>
                <th>total</th>
                <td>4</td>
            </tfoot>
        </table>
    </body>
</html>
```

## CSS
```css
h1 {
}
.class {
    color: blue;
    background-color: azure;
    background-image: url("https://www.example.com/image.jpg");
    /* Or use the local directory */
    background-image: url("local directory");
    font-size: 2em; /* 18px */
    font-family: Georgia;
    font-weight: bold; /* normal */
    width: 100px; /* 100% */
    height: 200px;
    text-align: center; /* left, right */
    opacity: 0.5;   /* 0-1 */
}
#id {
    width: 100px;
    height: 200px;
    /* border, padding, margin */
    
    border: 1px solid red; /* width style color*/
    border-radius: 5px;

    padding: 10px;
    padding: 2px 4px 2px 4px; /*clockwise rotation*/
    padding: 2px 4px; /* vertical: 2, horizontal: 4 */

    margin: 5px;
    margin: 2px 4px 2px 4px;
    margin: 2px 4px;
    margin: 0 auto; /*horizontally centered */
    margin-right: 3px; 
}
p.class {
    min-width: 300px;
    max-width: 400px;
    min-height: 300px;
    max-height: 400px;

    overflow: auto; /* scroll, hidden, visible */
}
.class li {
    box-sizing: content-box; /* border-box */
}
/* resetting defaults */
* {
    margin: 0;
    padding: 0;
}
```
<img src="/assets/img/box_model.png" alt="Box Model" width="400" height="300"/>
<img src="/assets/img/margin_collapse.png" alt="Magin collapse" width="400" height="300"/>

## Google Dev Tools
Use `Command + Shift + c` to open Chrome Dev Tools
