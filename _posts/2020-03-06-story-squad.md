---
layout: post
title: Story Squad
subtitle: Story Matchmaking for Kids
gh-repo: Lambda-School-Labs/story-squad-ds
gh-badge: [star]
tags: [long post]
---

Story Squad is a platform for weekly storytelling and art contests among kids in grades three through six. As a member of the three-person "Labs 20" team, I was tasked with building the foundation of the data science component of the application over eight weeks. Our work was all about making a high-performing algorithm to match participants with their peers.

The Story Squad game involves two rounds of assessment. On each team of two, kids rate their own and their partner's creative submissions on a relative basis, betting points on which story or illustration is most likely to win the head-to-head matchups against an unknown opposing team's stories and illustrations. In the second phase, independent evaluators pick their favorites between the stories and illustrations matched across different teams.

This means that kids have a lot of chances to win each week. Either their story or their illustration might be assigned more points than their teammate's; either one might win its head-to-head with the opponents' submissions; and even if none of those happen, their team could still collectively get more points and carry the day.

These chances can only manifest meaningfully for a kid if their group of four -- them, their teammate, and a pair of opponents -- are all performing on roughly the same level. A weak teammate is a liability; a weak opponent is hardly a pleasure to defeat. Likewise, there's no fun in being steamrolled by an obviously more advanced opponent or carried by a hugely superior ally. Bad matchups not only make the game less fun, but also send a signal to a participant that they're in the wrong place.

Given all that and the huge developmental gaps among the target audience, creating better-than-random matchups is critical.

Getting from a full cohort of creative submissions to a set of teams and matchups was a three-part process:

1. Transform the photographed stories and drawings into machine-readable content
2. Score the content along relevant axes 
3. Group kids creating at similar levels of sophistication

A pretty tall order!

We focused on processing written story submissions during our time on the project. That meant that step one was perfectly clear; we needed to incorporate optical character recognition into the data pipeline so that the text of each handwritten story could be processed later. We used Google Cloud's Vision API, which provided a high degree of accuracy quickly and with a low cost. During this phase, I wrote a Python script that inserted both automatic and manual transcriptions of each of the 167 stories from our sample dataset into a convenient csv file. I also devised a metric that would provide insight into the quality of the automatic transcription.

Step two was more open-ended. We ended up drawing on the rich tradition of "reading scores" like the Flesch Reading Ease score and the Coleman-Liau Index for this part, as well as taking cues from our client, the Story Squad founder, on story elements he associated with storytelling competence. During this phase, I updated our csv to include the scores we were considering to allow for easy data exploration.

In step three we could finally start creating matchups using clustering algorithms, but had to balance our desire to iterate, iterate, iterate against the reality of testing each iteration. There was simply no substitute for having a human evaluator judge the quality of the matchups. Fortunately, our client was happy to pitch in and work with us to develop and use a system of match evaluation, and we tested three different versions of the matchmaking algorithm before settling on the one that produced the best score. I took the lead on interfacing with the client during this time, as well as implementing the logic that translated clusters of players into teams and matches.

I'll let our client's words speak for themselves:

> Samanatha, Bhavani and Clay absolutely crushed Labs 20.  The work they did on handwriting recognition allowed us to weaponize the time kids spend scribbling and drawing — this is the killer feature that makes Story Squad so impactful for kids: unlike YouTube, Fortnite, Snapchat et al, we don’t maximize for passive Time-on-Device, but for Time-in-Creative-Mode.  Their work allows us to deliver this fundamental value prop to kids and parents. It’s a game changer in terms of product differentiation!  Additionally, the team’s work on clustering matchups drives unprecedented value to users in terms of retention.  The importance of their work in Labs 20 cannot be overstated!  Story Squad would be a watered down derivative idea without their contributions, and they have brought this cutting edge technological ooomph that will makes an enormous difference in kids’ lives.  Brava, bravo and thank you!!

-Story Squad Founder Graig Peterson

[Check it out here.](https://www.storysquad.education/)