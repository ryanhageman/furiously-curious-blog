---
layout: post
title: Fundamentals of CSS
categories: CSS
tags:
---
It's the "language" that people love to hate. They struggle with it, fight with it, say it's "not really a programming language". CSS. The web would be stuck in the 1990's without it. 

The thing is, [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) is really important, it's here to stay, and strangely enough, if you lean into its fundamentals instead of ignoring and fighting them, it's pretty great to work with. 

This is the first in a series of posts to make CSS not only workable, but actually a bit fun. Understand a few fundamentals, follow a few rules, and CSS can be your friend. You might even prefer writing CSS to using the frameworks that make it "easier". 

## Before CSS

- show site with styles turned off
- show site with styles back on


## You're styling something else

The styles don't work on their own. You're styling a document. How do you know what part of the document you're styling. If it were only a bunch of words, you wouldn't be able to. Good thing you've got the parts of the document tagged. Remember HTML and it's "tags"? That's what those are for. It creates a heirarchy, sure, but it also tags things as headings, paragraphs, spans that are a smidge different than the text around it, things like that. It even gets a bit better with articles, asides, and other semantic tags. 

With only HTML tags, you can make your document look pretty ok. But if you want more than that, there are a few options. There are a few basic ways to grab specific parts of your document to style them.

- The base elements themselves (the tags)
- Classes
- IDs

### Base HTML Elements

While there are a lot of different HTML tags out there, you don't have to style them all. Most of them either are fine the way they are, or you'll transform into something more in the next layer. You might not need to do anything on this layer. Some very basic things to consider. 

- body
  - set a font
  - set a size
- headings
  - set a font 
  - set sizes for each of them, if you want
  - set weights
  - etc

You might choose to do more, but don't worry too much about these. Most of your styles will be written in the next layer.

### Classes

Use classes to style everything. This is where you can get specific with the things you're building. Cards, navigation dropdowns, layouts, these are the components you use to assemble your document into an app or site. You can use classes to name these different components, then style them and assemble them on the screen.

Only use classes for these. IDs are not your friend for styling. 

### IDs

Only use IDs if it's REALLY unique. Imagine you've got a group of minions. `class="minion"`. Then there's a Harry Styles minion. There's only one Harry Styles. `id="harry-styles" class="minion"` that's it. It builds on the fact that this Harry Styles minion is still a minion, but THIS PARTICULAR ONE is Harry Styles. 

ID's are for TRULY unique things. You 'can' use them for JavaScript hooks, but remember, TRULY unique. `data` attributes are better as JavaScript hooks. 


## Naming Your Classes

Names are important. Those names are how you identify which styles to apply to each element. CSS creates one big list of styles and uses that list to make the document look nice. Thing is, there's only ONE list, and it's used everywhere. AND, if something is set, then changed later in the list, the last set of styles wins. This is the 'cascade'. We'll dive into that a bit later. 

Because there's only ONE list (that means its global), you need to have a strategy to name things. There are a couple basic ways to approach this. Give things unique names, or make a bunch of general utilities and slap them all over the place. Each has its pros and cons. I like a combination of the two, but lean very strongly toward unique names for the components of your site with a few utility classes. 

Talk about how CSS is global. Do a couple things to make your life better:

- Only use classes
  - CSS Math isn't hard if you only style with classes. 1 class, your styles apply. 2 styles beats 1 style. Don't use ids and you don't have to fight with them. 
- [BEM](https://getbem.com/)
  - BEM stands for Block, Element, Modifier. Blocks are like components. They're a thing you're working on, like a card. A card can have a header, a body, a footer, unique card style buttons. They're all part of `.card`. Want to focus on the header? `.card__header` Have primary and secondary buttons? `.card__button--primary`. Why the double dashes? That way dashes still work to separate words. Is it pretty? Not really. Does it work? Yes. Since CSS is global, things like this help keep things namespaced and separate. It's not that crazy after a while, and there's usually only one class on an element instead of lots of utility classes. You also don't have to do CSS math like you do with utility classes. There's only one or two classes, they're namespaced, you know what's styling your element and where to find it. Writing these with Sass makes it easier too.

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


