---
title: "Social Media Investigation Hub [Locked]"
description: "Writeup du challenge OSINT Social Media Investigation Hub sur HackTheBox"
date: 2026-03-12
slug: "htb-social-media-investigation-hub"
image: images/osint.png
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
**Question 1:** What is the real name of the person behind the TechReviewer2024 account? **Alex Morgan** (ConnectPro profile reveals the real name in the professional headline).  

**Question 2:** Which company did Alex Morgan previously work for? **RivalTech Inc.** (Marketing Specialist from Jan 2021 - Dec 2023 according to ConnectPro).  

**Question 3:** What is the operation codename mentioned in the ForumHub coordination post? **operation_social_storm_2024** (Mentioned in 'XyloPhone Pro Campaign Coordination' post).  

**Question 4:** In which month and year were most of the suspicious reviewer accounts created? **February 2024** (Indicated by the ChirpNet following list timestamps).  

**Question 5:** What product is being specifically targeted in the negative review campaign? **XyloPhone Pro** (Specifically outlined in the ForumHub coordination post). 

**Question 6:** What role does TechReviewer2024 have in the TechReviews subreddit? **moderator** (Shown on the ForumHub profile with 24 posts this month).  

**Question 7:** What is Alex Morgan's educational background? **University of California, Berkeley** (Bachelor of Science in Marketing, 2017-2021).  

**Question 8:** How many connections does Alex Morgan have on ConnectPro? **89** (The profile shows exactly 89 connections).  

**Question 9:** What is the total post karma that u/TechReviewer2024 has accumulated? **1247** (The ForumHub profile shows 1,247 post karma).


`HTB{alexmorgan_operationsocialstorm2024_february2024}`
{{< /flag >}}
