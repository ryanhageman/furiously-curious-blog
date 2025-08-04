---
layout: post
title: Completions in Neovim
categories: [ Neovim ]
tags: [ neovim, completions ]
---
Type things, that little window pops up and suggests ways to complete the word you're typing. How does that work?

Whether the suggestions are other words in the file you're working on, file paths, or a module from the other side of your project, they come from somewhere. It's a list of things that might fit given the context of what you're typing right now. 

## It's a list

There are a lot of places to get a list of completion suggestions. To keep things straightforward, lets start with the place we are, this post. From beginning to end, this is a list of words. 

We could ask the computer to go through each word in this post and add it to a `[list, of, words, in, this, post]`. Next, we should toss out duplicates. 

It's time to use the list. Hit a key and a letter appears on the screen. "a". Hey, computer, get all the words in the list that start with "a". Or, get all the words that have an "a". Add another letter and the list gets shorter, "al", not as many words have both of those letters in that order. "all", that's the word. Choose it and "poof", it's there. 

## But Other Info

There are all kinds of other info that can help with finding the right completion. Each system structures the data so it can find what it's looking for. Our list of words from this post is "Text". A list of files and paths in the project are "Files". 

## How Does It Know What To Return

In a simple world, it looks at the current file and the keystrokes you've typed since the last space. 

## Completion Sources

Each source sets up its own specifics. 

## Wikilinks Completion

This seemed like a super complicated web of wizardry. The I broke it down and it's not too much. Using something fast, like ripgrep, this can be set up in around 100 lines of code. 

- Get the names of all the files
- Set up "[[" as the trigger
- After the trigger and however many extra characters you choose, show the matches from the filename list

The index is made and held in memory, the list is filtered as you type. Unless you've got thousands and thousands of large files, ripgrep handles the initial index pretty much instantly. The list can be filtered lickety split. 

## Unresolved Links

The obsidian.nvim plugin is fantastic and has wikilink completion built in. Unfortunately, it only suggests existing files. There's a lot built in here, handling aliases and all kinds of stuff, but what about "unresolved links".

Unresolved links are the `[[wikilinks]]` you've added to your notes, but didn't create the files yet. These are great, when you pair them with backlinks, to keep your notes organized and linked without needing to create and fill out notes right until you have info you want to save in that note. 

Adding a completion source for unresolved links takes around 100-200 lines of code. The details are coming soon in another post. The steps are:

- Get the names of all the files
- Scan through the files and make a list of all the `[[wikilinks]]`
- Parse the list of wikilinks and sort them
  - files
  - unresolved links
- Set up "[[" as the trigger
- After the trigger, return the list of appropriate unresolved links
- Keep filtering the list as more characters are typed

All the popups and filtering are handled by your completion plugin. Make a list, format it for the completion plugin to use, hook it up, complete away!




