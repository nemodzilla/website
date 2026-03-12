---
title: "Flag Command [Unlocked]"
description: "Writeup du challenge WEB Flag Command sur HackTheBox"
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

On peut juste choisir HEAD NORTH pour avancer le reste n'est pas accepté. Ensuite on a 4 choix :
- GO DEEPER INTO THE FOREST
- FOLLOW A MYSTERIOUS PATH
- CLIMB A TREE
- TURN BACK

Après avoir choisi le premier on est mort.

Alors on lance la console et on va fouiller dans le code.

On voit dans game.js :
![Image 1](assets/image.png)

On filtre :
![Image 2](assets/image2.png)

En allant jusqu'au bout avec ces 4 réponses il y avait une 5ème étape où les choix ne sont pas montrés ici. J'ai donc pris un des choix pour faire une recherche et voir où il est marqué et je vois dans l'onglet réseau un fichier nommé "option".
![Image 3](assets/secret.png)

On voit un choix secret alors on le teste :
![Image 4](assets/image4.png)

`HTB{D3v3l0p3r_t00l5_4r3_b35t__t0015_wh4t_d0_y0u_Th1nk??}`