---
title: "Flag Command [Unlocked]"
description: "Writeup for the WEB challenge Flag Command on HackTheBox"
date: 2026-03-12
slug: "htb-flag-command"
image: assets/web.png
categories:
    - HackTheBox
tags:
    - web
draft: false
---

## Introduction

**Challenge Scenario:**
Embark on the "Dimensional Escape Quest" where you wake up in a mysterious forest maze that's not quite of this world. Navigate singing squirrels, mischievous nymphs, and grumpy wizards in a whimsical labyrinth that may lead to otherworldly surprises. Will you conquer the enchanted maze or find yourself lost in a different dimension of magical challenges? The journey unfolds in this mystical escape!

RETIRED Machine

## Solution

The only accepted command to progress is HEAD NORTH. After that, we get 4 choices:
- GO DEEPER INTO THE FOREST
- FOLLOW A MYSTERIOUS PATH
- CLIMB A TREE
- TURN BACK

After choosing the first one, we die.

So we open the browser console and dig into the source code.

We can see in game.js:
![Image 1](assets/image.png)

We filter the results:
![Image 2](assets/image2.png)

Going through all 4 answers leads to a 5th step where the choices aren't displayed. I picked one of the options and searched for it in the Network tab, where I found a file named "option".
![Image 3](assets/secret.png)

We can see a secret choice, so we try it:
![Image 4](assets/image4.png)

`HTB{D3v3l0p3r_t00l5_4r3_b35t__t0015_wh4t_d0_y0u_Th1nk??}`