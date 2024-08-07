---
layout: post
title: Instruction Set Architectures
categories:
tags:
date: 2024-08-05 17:32 -0500
image: /assets/images/instruction-set-architectures-hero-image.webp
---
Instruction Set Architectures are the very basic instructions a processor can execute. These are simple things, like: 

- Add these numbers
- Merge these strings

## What's the difference between ARM and Intel? 

There are different types, and brands, of processors. Each type of processor is built with different sets of instructions to be used. Two of the main types are *ARM* and *Intel*.

### Intel

Intel processors use the x86 ISA. That's a "Complex Instruction Set Computing" (CISC) architecture. Some of the commands they can execute with a single instruction are pretty complex. This ability makes them powerful, but those complicated instructions use a lot of electricity and generate more heat. If your task has a lot of complex instructions, an x86 processor might be a good choice.

### ARM

ARM processors use "Reduced Instruction Set Computing" (RISC). These processors can ultimately do all the same things as any other processor, but you might have to string commands together to get the same result as a single command on an CISC processor. Ultimately, though, they use less power and generate less heat.

## How would it look on each processor to add two numbers?

### ARM Processor

> Move the number 5 into register R0  
> `mov r0, #5`     
> 
> Add 3 to the value in R0, storing the result in R0  
> `add r0, r0, #3` 
{: .prompt-info }

### Intel Processor

> Move the number 5 into the EAX register  
> `mov eax, 5`     
> 
> Add 3 to the value in the EAX register  
> `add eax, 3`     
{: .prompt-info }

## Why are they different with different processors?

The instruction sets are different, so the commands need to be set up differently.

Even when the instruction would be the same, the [binary]({% link _posts/2024-04-27-understanding-binary-with-tacos.md %}) code for each instruction is different. For example `mov`. For an ARM processor, `mov` might be `001110`, while for Intel it might be `1011`.

## How it might look in binary

These are oversimplified examples. In real life they get very complex, quickly.

### ARM

> Move the number 5 into register R0  
> `mov r0, #5`     
> 
> This command in [binary]({% link _posts/2024-04-27-understanding-binary-with-tacos.md %})  
> `1110 0011 1010 0000 0000000000000101`
{: .prompt-info }

In the beginning you have `1110`, the opcode for `mov`. `0000` is the `r0` register. The end is the number 5.

### Intel

> Move the number 5 into the EAX register  
> `mov eax, 5`     
> 
> This command in [binary]({% link _posts/2024-04-27-understanding-binary-with-tacos.md %})  
> `1011 0000 00000000 00000000 00000101`  
{: .prompt-info }

`1011` is the opcode for `mov` to the `eax` register. The last byte is the number 5.
