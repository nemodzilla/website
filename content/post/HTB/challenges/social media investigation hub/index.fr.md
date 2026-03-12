---
title: "Social Media Investigation Hub"
description: "Writeup du challenge OSINT Social Media Investigation Hub sur HackTheBox"
date: 2026-03-12
slug: "htb-social-media-investigation-hub"
image: /images/osint.png
categories:
    - HackTheBox
tags:
    - osint
draft: false
---

## Introduction

**Challenge Scenario:**
You've discovered Alex Morgan is connected to RivalTech and has been conducting fake review campaigns against TechFlow. Now you need to map Alex's complete digital footprint across social media platforms to understand the full scope of this operation and find evidence of coordination with other actors.

## Solution
{{< flag "3ddbc1fb4fb9bb0af6c95d6fc3ac64c49c70caddf39c417c088a970e1a9846ee" "1" >}}
**Question 1:** Quel est le vrai nom de la personne derrière le compte TechReviewer2024 ? **Alex Morgan** (Le profil ConnectPro révèle le nom réel dans le titre professionnel).

**Question 2:** Pour quelle entreprise Alex Morgan travaillait-il précédemment ? **RivalTech Inc.** (Marketing Specialist de janv. 2021 à déc. 2023 selon ConnectPro).

**Question 3:** Quel est le nom de code de l'opération mentionné sur ForumHub ? **operation_social_storm_2024** (Cité dans le post 'XyloPhone Pro Campaign Coordination').

**Question 4:** En quel mois et année la plupart des comptes suspects ont-ils été créés ? **February 2024** (Visible via la liste d'abonnements ChirpNet).

**Question 5:** Quel produit est spécifiquement ciblé par la campagne de dénigrement ? **XyloPhone Pro** (Confirmé par les points d'attaque détaillés sur ForumHub).

**Question 6:** Quel rôle TechReviewer2024 a-t-il dans le subreddit TechReviews ? **moderator** (Indiqué sur son profil ForumHub).

**Question 7:** Quel est le parcours scolaire d'Alex Morgan ? **University of California, Berkeley** (Bachelor of Science en Marketing, 2017-2021).

**Question 8:** Combien de relations Alex Morgan a-t-il sur ConnectPro ? **89** (Chiffre visible sur son profil professionnel).

**Question 9:** Quel est le karma total de u/TechReviewer2024 sur ForumHub ? **1247** (Karma accumulé via ses nombreux posts récents).


`HTB{alexmorgan_operationsocialstorm2024_february2024}`
{{< /flag >}}