---
layout: post
title: Fundamentals of CSS
categories: CSS
tags:
---
It's the "language" that people love to hate. They struggle with it, fight with it, say it's "not really a programming language". CSS. The web would be stuck in the 1990's without it. 

The thing is, [CSS](https://en.wikipedia.org/wiki/CSS) is really important. And it's here to stay. Strangely enough, if you lean into its fundamentals instead of ignoring and fighting them, it's pretty great to work with. 

This is the first in a series of posts to make CSS not only workable, but actually a bit fun. Understand a few fundamentals, follow a few rules, and CSS can be your new best friend. You might even prefer writing CSS to using the frameworks that make it "easier". 

## Cascading Style Sheets

It's right there in the name. **Cascading** style sheets. The cascade is what makes CSS work,and it's the thing that folks fight with the most. 

Let's say you style your `H2` to be 30 pixels tall:

```css
h2 {
  font-size: 30px;
}
```

Anywhere you use an `H1` the text will be 30 pixels high! pretty straight forward. 

As you keep working, you create a "Card" that has a header section. You need to use an `H2` for proper accessibility, but you want the `H2` on your "Card" to be 26 pixels. 

```css
h2 {
  font-size: 26px;
}
```

If you write this after the first one, ALL your h2's will now be 26 pixels. That's because the last rule you write is the one that applies. The second `font-size` "cascades" over the earlier ones. It's like draping a curtain over the previous rule. The later curtain covers up the style in the earlier curtain. 

This seems frustrating, but only if you don't think first about what order you're writing your styles. 

### Import order

You get to decide what order your style sheets are imported into your page. You can do it in the head of the page, or use something like [Sass](https://sass-lang.com/) to give you more control. Yes, there are other options, [PostCss](https://postcss.org/) is great too. 

There are two basic layers to use when setting up a CSS system.

1. Foundation Layer
2. Style Layer

The Foundation Layer is where you set up your fundamental building blocks. Things like [CSS Variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/--*), [Sass Mixins](https://sass-lang.com/guide/#mixins), or even [CSS Functions](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@function) live here.

These don't actually generate CSS Styles, but they're the building blocks for the styles you're going to write. The need to be available everywhere, so they get pulled in first. 

[Resets and Normalization](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@function) make your page styles act the same no matter which browser the user is using. The goal is to make basic styles and elements look the same across browsers. 


