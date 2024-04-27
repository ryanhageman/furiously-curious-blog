---
layout: post
title: Understanding Binary, With Tacos
categories:
tags:
date: 2024-04-27 10:52 -0500
image: /assets/images/binary-tacos-hero-image.webp
---
Everything you're looking at here is 1's and 0's. When you scroll around on the screen, the movement is created by 1's and 0's. All the different colors, the shows we stream, everything digital comes down to 1's and 0's.

Even weirder, it's not even a number, it's a microscopic switch, that's either on or off. That state, on or off, represents either a 1 or a 0.

How?

## Numbers Represent Everything On Your Device

> Tacos are delicious.
{: .prompt-tip }

The sentence above is a list of letters and spaces. Each of the characters in the sentence has a number to represent it. There's more than one way to [convert a character to a number](https://en.wikipedia.org/wiki/Character_encoding#Character_sets,_character_maps_and_code_pages). The one we use with all of our emojis is [UTF-8](https://en.wikipedia.org/wiki/UTF-8). [ASCII](https://en.wikipedia.org/wiki/ASCII), and [Unicode](https://en.wikipedia.org/wiki/Unicode) are a couple of others. Each of these is a little bit different, but in general, each character has a number equivalent.

Let's start with a letter, how about X. The number code for capital X is 88. Lowercase x is a different letter, its code is 120. Even a space has a code, it's 32.

There are different ways to represent the number 32. It could be 32, or thirty two, or '0x20'. Ultimately, though, all of these are different ways to represent the 32 items we're talking about.

## Base 10
{: #base-10 }

The numeric version, 32, is encoded. We use this encoding so much that our brains automatically translate it. The position of the number matters a LOT. 32 is a [Base 10](https://en.wikipedia.org/wiki/Decimal) number. Each position represents an amount of 10's. Since our everyday number system has only 10 characters, 0 - 9, this is a good way to count.

If we start at 0 and count up, we run out of numbers after 9. How do we represent the next item? We add a column and put a one there. Then, we reset the 9 to 0. 10 means 1 group of ten and 0 ones. 11 is 1 group of ten and 1 one. 12 is 1 group of ten and 2 ones.

To visualize, we'll need something to look at. Like most folks, I like tacos. They're honestly one of the most versatile and delicious foods to ever exist. I could really use 12 tacos, you in?

For the number 12, there are two columns. Each one has a certain number of tacos.

| 1 (Tens)             | 2 (Ones) |
| -------------------- | -------- |
| 🌮🌮🌮🌮🌮🌮🌮🌮🌮🌮 | 🌮🌮     |

There are ten tacos in our tens column and two tacos in the ones column. Our brain does the addition automatically, so we intuitively understand it.

Binary "numbers" are not different numbers. Binary is a different way to represent the number of items we're referring to, like our twelve tacos above. We don't have to stick with twelve. We could say 12 or even a dozen.

## Binary
{: #binary }

Binary is another way to say [Base 2](https://en.wikipedia.org/wiki/Binary_number). Base 2 means that each column is a multiple of 2. It's a lot like [Base 10](#base-10). Each column represents a number of items, then we add up all the columns to know how many items we have.

In Base 10, we added a new column for ten, 100, 1000, because we ran out of numbers. Same with binary. Here, we have 0 and 1. Let's start counting.

0 in binary, is 0.

1 in binary, is 1.

Now you're counting in binary. Where we get tripped up is trying to convert binary representations to Base 10 in our heads. It's an addition problem, like Base 10, but we haven't used it so much that it's automatic.

After one comes two. We don't have a number for it, though, so we'll add a column.

10

Yeah, it looks like ten, but it's two.

| (1) Two | (0) One |
| ------- | ------- |
| 🌮🌮    |

Moving on to three (11):

| (1) Two | (1) One |
| ------- | ------- |
| 🌮🌮    | 🌮      |

Above, there is one "two" and one "one", add it up and it's three. No matter if you write it as 3, three, or 11, it refers to the same number of tacos, 🌮🌮🌮.

Each new column doubles the last one.

Four is 100.

| (1) Four | (0) Two | (0) One |
| -------- | ------- | ------- |
| 🌮🌮🌮🌮 |         |

Five is 101

| (1) Four | (0) Two | (1) One |
| -------- | ------- | ------- |
| 🌮🌮🌮🌮 |         | 🌮      |

Six is 110

| (1) Four | (1) Two | (0) One |
| -------- | ------- | ------- |
| 🌮🌮🌮🌮 | 🌮🌮    |

Seven is 111

| (1) Four | (1) Two | (1) One |
| -------- | ------- | ------- |
| 🌮🌮🌮🌮 | 🌮🌮    | 🌮      |

We need a new column.

Eight is 1000

| (1) Eight             | (0) Four | (0) Two | (0) One |
| --------------------- | -------- | ------- | ------- |
| 🌮🌮🌮🌮<br/>🌮🌮🌮🌮 |          |         |         |

We've got a lot of tacos.

## Back to UTF-8

The code for a space is thirty two. In [Base 10](#base-10), that's 32. In [Binary](#binary) it's 100000.

| (1) Thirty Two                                                                    | (0) Sixteen | (0) Eight | (0) Four | (0) Two | (0) One |
| --------------------------------------------------------------------------------- | ----------- | --------- | -------- | ------- | ------- |
| 🌮🌮🌮🌮🌮🌮🌮🌮<br />🌮🌮🌮🌮🌮🌮🌮🌮<br/>🌮🌮🌮🌮🌮🌮🌮🌮<br />🌮🌮🌮🌮🌮🌮🌮🌮 |             |           |          |         |         |

That's a lot of tacos in the "Thirty Two" column, but none in the rest. Without any kind of delimiter to group things, like a comma, it's hard to see how many columns there are. In writing, I'll stick with Base 10.

To represent our space character, though, we can only use 0 and 1, so 100000 will have to do. We can't use a comma either, because a comma is neither a 0 nor a 1. That comma is 44.

Our 🌮 emoji takes up 4 bytes, so it would be represented by 4 Base 10 numbers, 240, 159, 140, 174. In Binary (Base 2) it's 11110000 10011111 10001100 10101110.

## Bits and Bytes

Each 1 takes up a 'bit' of memory. Bit is a unit of measurement. 8 bits equals 1 'Byte'. All the basic letters in our alphabet can be represented in one Byte of memory. Memory is chunked into Bytes for [a reason someone decided long long ago](https://en.wikipedia.org/wiki/Byte).

One byte can represent any number from 0 to 255.

## Converting To Binary

> Tacos are delicious.
{: .prompt-tip }

Our sentence is still a list of characters. The letters and spaces are converted, using UTF-8, to numbers. The numbers are represented in binary. The binary representation is saved in 'Byte' sized chunks of memory by flipping those switches on and off.

> 01010100 01100001 01100011 01101111 01110011 00100000 01100001 01110010 01100101 00100000 01100100 01100101 01101100 01101001 01100011 01101001 01101111 01110101 01110011 00101110
{: .prompt-info }

I think almost all of us can agree with that sentence.
