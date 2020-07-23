---
layout: post
title: The COVID Notebooks
subtitle: Visualizing Local Pandemic Trends
gh-repo: srfinley/MD-covid-viewer
gh-badge: [star]
tags: [long post]
---

Like a lot of people in self-isolation during the pandemic, my dad has become a bit of a news junkie. What's the governor saying about the situation? What are the numbers saying? Staying on top of of the data helps him feel more confident in the decisions he's making to protect his health.

His state dashboard is good; he especially likes the local views, which give him a snapshot of how his county and zip code (and the immediately surrounding counties and zip codes) are doing. But what he really wanted, and couldn't get from the dashboard, were local cases _over time_. Trying to figure out whether the daily new case numbers were going up or down locally wasn't practical.

Enter me!

My task was clear: use my training in data science to build a tool my dad could use to stay informed. First, with a little bit of googling, I found the data APIs that the state dashboard uses to generate each day's view. By hitting the endpoints, I could confirm that they were unprotected and take a look at the structure of the data.

The fact that a RESTful API responds in JSON format tells us very little about how the JSON object itself is structured. My second task was to unpack the response, peeling back its convoluted layers and reshaping it into a table for analysis. This part really hammered home the conventional wisdom that data scientists programming is more about producing the _right_ code than many lines of code; all my exploration resulted in a short, simple script that produced consistent results.

For each locality, I wanted two different views: the first one of cumulative cases and another of average new cases per day. Producing them was step three. The APIs automatically serve the cumulative version, and you can intuitively understand how to turn a table of cumulative values into a table of rolling averages or sums by subtracting earlier values from more recent ones. Fortunately, pandas makes such a calculation trivial. Seven-day averages are popular for coronavirus views, since they smooth out weekend reporting dips.

Once the data science problems were well in hand, I was left with a user interface problem. How could I empower my dad, despite his lack of familiarity with Python, to use this Python tool?

One has certain customizability expectations of a web app that are hard to translate into a notebook. This exercise forced me to zero in on the variables of interest in order to allow them to be easily modified by my lay user:

- regions to visualize
- whether to truncate the early days, and if so, by how much
- for rolling averages, over the past how many days to average

I think this was a valuable exercise in code structure -- and in commenting, since each of those variables, as well as the other code, demanded thorough annotation. Philosophically: either hide it or explain it. In the notebook format, hiding wasn't an option.

My biggest advantage was that my dad was receptive to being trained. As long as I showed him how to get the information he wanted, he was willing to jump through a few hoops to get it.

There were other, subtler quality-of-life improvements to be made. I cut the number of cells to run down to the bare minimum. In the first iteration of the notebooks, I conceptualized the "check whether today's data is present" operation as a matter of printing the last few rows of the table and comparing the most recent date to that day's; but the majority of data revealed in that operation was a waste, and using it was burdensome. Ultimately, I learned a little about the datetime module and implemented an automatic date check.

It's still imperfect. Region names are subject to mistyping; my dad complains that running each cell in turn makes him feel like a trained ape. But what really matters is that it tells him what he needs to feel well-informed.

[Check it out here.](https://github.com/srfinley/MD-covid-viewer)