---
title: "Markup: Syntax Highlighting"
excerpt: "Post displaying the various ways of highlighting code in Markdown. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sequi, accusantium sint ullam? Facere, perferendis in ipsa hic explicabo ad vitae sequi soluta eligendi asperiores quod delectus voluptas minus magni officia."
modified: 2016-09-09T09:55:10-04:00
header:
  teaser: "assets/images/markup-syntax-highlighting-teaser.jpg"
categories:
    - Markup
tags: 
  - code
  - syntax highlighting
---

Syntax highlighting is a feature that displays source code, in different colors and fonts according to the category of terms. This feature facilitates writing in a structured language such as a programming language or a markup language as both structures and syntax errors are visually distinct. Highlighting does not affect the meaning of the text itself; it is intended only for human readers.[^1]

[^1]: <http://en.wikipedia.org/wiki/Syntax_highlighting>

### GFM Code Blocks

GitHub Flavored Markdown [fenced code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/) are supported. To modify styling and highlight colors edit `/_sass/syntax.scss`.

```css
#container {
  float: left;
  margin: 0 -240px 0 0;
  width: 100%;
}
```