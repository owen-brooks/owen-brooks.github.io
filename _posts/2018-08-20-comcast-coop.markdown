---
layout: post
title: "What It Was Like To Co-op at Comcast"
date: 2018-08-20 08:34:25
categories: Comcast Co-op
tags: featured
image: /assets/article_images/comcast.jpg
---

This summer I worked as a Data Engineering Co-op for Comcast. During the 6-month cycle I learned a lot about programming, data, and what its like to work for a massive corporation like Comcast. Looking back, my position was kind of unique. Unlike the other co-ops I did not participate in the Agile development process. Instead I worked closely with a Senior Engineer on different projects that him and management came up with. I will go more in-depth into this below.

# What I Did

- **Metadata Search App:** This was the first project I worked on. Someone had previously created a company data search – allowing teams to quickly asses the content of different data sets. Using ElasticSearch as a foundation, I rebuilt this in Python, fixing UI bugs from the predecessor. Because the ElasticSearch data did not have a uniform schema, it made creating the queries complicated. It was not a priority to re-load the database, and I was given a different project.

- **Dev-Ops REST-API:** I built a REST API to allow other employees manipulate the properties of ETL workflows. Coming in I had no experience with Java so I first built a POC in Python. I then created the final version in Java. I learned a ton about application design using the MVC model. After it was deployed, I made a couple revisions to fix bugs and add additional features. Additionally, I got experience with continuous deployment using Jenkins and Cloud Foundry.

- **Workflow Dashboard:** Created a dashboard allowing engineers to monitor their ETL workflows. This gave me good experience in frontend development and design. The biggest challenge of this project was working with a badly supported 3rd party API.

- **Data Ingestion Automation:** Converted huge shell scripts to Python. I ran out of time on this project as my 6-month co-op came to an end. I started playing around with ways to automate the process.

# Thoughts About Comcast

It was very interesting time period for the company while I was there. During the 6-month period they acquired Sky Cable and then lost a bidding war for FOX News. While I was obviously not involved in any of this it was exciting to read the headlines while working for them. The size of Comcast did make some things harder. Many of the developers I worked with were located in either India or Colorado. While the time difference with the later is less significant, it did effect my work schedule. Additionally, not all teams were cooperative in the sharing of knowledge, code, time etc. Not sure if this had something to do with the company size. At some scale, this is probably true of all companies.

# Going Forward

I am currently considering going back to Comcast for my final co-op. The experience was challenging and because of this I learned a ton. I thoroughly enjoyed my time there and would recommend it to anyone looking for a software / data focused job.
