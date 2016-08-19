---
title: "Google Summer of Code’16 with Oppia"
layout: post
date: 2016-08-20 00:30
image: '/assets/images/'
description:
tag: gsoc, oppia
blog: true
jemoji:
author: Avijit Gupta
---

### Introduction:

Every year, Google invites open source projects from various organizations so that students across the globe can contribute to them as a part of Google Summer of Code programme.
I was forunate enough to be a part of GSoC-16 under the organization Oppia. Before I go on and detail my journey, let me tell you something about myself.

I am Avijit Gupta, a Computer Science undegrad who loves to contribute to Open Source. I primarily like to work on Frontend technologies.

My journey with Oppia began as a contributor within the first few weeks after the announcement of selected organizations this year.
The two possibly main parts to backing a GSoC project are: code contributions (in terms of bugfixes, enhancements) and a great project proposal.
Hence, choosing a project and making a good proposal was the foremost step. I worked on the project - Creator Dashboard.


### Detailed Description of Project:

<GSoC and ur own timeline> - contributions, proposal, bonding, project timeline.

Before I begin introducing the project, it's a must to know that Oppia is a community of learners and teachers to help anyone learn anything they want in an effective and enjoyable way.
The project "Creator Dashboard" aimed at implementing a dashboard that allows lesson creators to see common statistics like total plays, average rating, common student misconceptions,
and student-submitted feedback for the lessons they own -- and to make it easy for creators to take action on this information.
Basically, it was a full-stack web project that involved working on AngularJS on the frontend and Python (Google App Engine) on the backend.

##### Week-by-week progress:
#### Week #1:
* Started off work by creating a continuous map-reduce job which will actually calculate the statistics.
* Changes in existing data models to store the computed data.

#### Week #2:
* Write unit tests and integration tests for the map-reduce job.

#### Week #3:
* Write a backend service to fetch data from models and send it to the controllers.
* Unit testing this service.

#### Week #4:
* Implement controller on backend which fetches the data through the service, and sends it to the frontend as a JSON response.
* Improve on the existing code to make it less redundant and use `get_multi` datastore calls as an optimization.

#### Week #5:
* Work on creating a service on frontend and the changes in controller.
* Testing both the service and controller.
* Make changes to the existing view of dashboard according to the latest mocks to mark the completion of MVP.

#### Week #6:
* Additions to frontend view of dashboard in form of creating the card view for the dashboard.

#### Week #7:
* Write a cron job to keep history of stats being recorded for each user. This is It kicks off a one-off map-reduce job to perform calculations.
* Tests for both cron job and one-off job.

#### Week #8:
* Fetch and display open feedback in dashboard - frontend and backend changes along with tests.

#### Week #9:
* Add realtime layer to statistics continuous job (written in the beginning) along with tests.

#### Week #10:
* Calculate and display change in statistics relative to the previous week's data.
* Display new feedback on frontend separately. 

#### Week #11:
* Make creator dashboard UI responsive, so that it looks equally good on mobile devices as on desktops.

#### Week #12:
* (Marked as busy)

#### Week #13:
* Work on adding sorting functionality to the list of explorations according to all the available parameters which are visible to the user, along with tests.
* Implement a dropdown which appears on clicking on each non-private exploration and displays most important statistical data to the user at once (PR for this is still not merged, due to a few failing tests!)

### Conclusions:
Well, during this 3 months of GSoC, I learn it a lot. I did the best that I could do with my knowledge and help from Xinyu, Allan, Sean, Ben and Jacob.

I can say that my work is 95% concluded. There’s still some revision to be made, some code to be clean up. And I’m doing that.
### Useful Links:

##### List of PRs:
1. https://github.com/oppia/oppia/pull/1891
2. https://github.com/oppia/oppia/pull/2082
3. https://github.com/oppia/oppia/pull/2096
4. https://github.com/oppia/oppia/pull/2101
5. https://github.com/oppia/oppia/pull/2126
6. https://github.com/oppia/oppia/pull/2151
7. https://github.com/oppia/oppia/pull/2155
8. https://github.com/oppia/oppia/pull/2170
9. https://github.com/oppia/oppia/pull/2173
10. https://github.com/oppia/oppia/pull/2238
11. https://github.com/oppia/oppia/pull/2239
12. https://github.com/oppia/oppia/pull/2252
13. https://github.com/oppia/oppia/pull/2281
14. https://github.com/oppia/oppia/pull/2291
15. https://github.com/oppia/oppia/pull/2296
16. https://github.com/oppia/oppia/pull/2318

#### Link to commits:
https://github.com/oppia/oppia/commits/develop?author=526avijitgupta
