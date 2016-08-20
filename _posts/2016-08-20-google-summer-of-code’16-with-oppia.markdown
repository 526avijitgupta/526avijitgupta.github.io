---
title: "Google Summer of Code’16 with Oppia"
layout: post
date: 2016-08-20 00:30
image: '/assets/images/'
description:
tag: gsoc
blog: true
jemoji:
author: Avijit Gupta
---

Every year, Google invites open source projects from various organizations so that students across the globe can contribute to them as a part of [Google Summer of Code](https://developers.google.com/open-source/gsoc/timeline) program.
I was fortunate enough to be a part of GSoC-16 under the organization Oppia. Before I go on and detail my journey, let me tell you something about myself: I am Avijit Gupta, a Computer Science undergraduate who loves to contribute to Open Source. I primarily like to work on Frontend related technologies.

My journey with Oppia began as a contributor within the first few days after the announcement of selected organizations in GSoC this year.


## About the Project:

[Oppia](http://oppia.org/) is a community of learners and teachers to help anyone learn anything they want in an effective and enjoyable way.
The project "Creator Dashboard" aimed at implementing a dashboard that allows lesson creators to see common statistics like total plays, average rating, common student misconceptions, and student-submitted feedback for the lessons they own -- and to make it easy for creators to take action on this information.

Basically, it was a full-stack web project that involved working on AngularJS on the frontend and Python (Google App Engine) on the backend.


### Final work:
![Markdowm Image][1]{: class="bigger-image" }


The screenshot of the page shown above is the current home page of all logged in users at [Oppia.org](https://oppia.org). The most of the statistics currently visible are updated in real time. The users have options to view the dashboard in 2 different formats - list view and card view. The list view is focussed more on power users, or the ones who like to see all their data at once. Card view is a more simplified and beautified format of displaying the explorations as tiles.

The statistics visible in the top white row are aggregated figures as a whole. Clicking on any exploration in the card view opens up a dropdown which provides with the exploration-specific data. The list of explorations can be sorted easily by either using the select dropdown or by clicking on the table headers in list view as well - thus making it easy for users to view their explorations based on different parameters quickly and easily.

The project also involved taking feedback from actual creators after the creation of a Minimum Viable Product(MVP) to ensure that the development is being done keeping the true needs of creators at highest priority.


### Weekly progress logs:

#### Week #1:
* Started off work by creating a continuous map-reduce job which will actually calculate the statistics.
* Changes in existing data models to store the computed data.

#### Week #2:
* Write unit tests and integration tests for the map-reduce job.
* Pull Request: [https://github.com/oppia/oppia/pull/1891](https://github.com/oppia/oppia/pull/1891)

#### Week #3:
* Write a backend service to fetch data from models and send it to the controllers, along with unit tests.
* Pull Request: [https://github.com/oppia/oppia/pull/2082](https://github.com/oppia/oppia/pull/2082)

#### Week #4:
* Implement controller on backend which fetches the data through the service, and sends it to the frontend as a JSON response.
* Improve on the existing code to make it less redundant and use `get_multi` datastore calls as an optimization.
* Pull Requests: [https://github.com/oppia/oppia/pull/2096](https://github.com/oppia/oppia/pull/2096), [https://github.com/oppia/oppia/pull/2101](https://github.com/oppia/oppia/pull/2101)

#### Week #5:
* Work on creating a service on frontend and the changes in controller.
* Testing both the service and controller.
* Make changes to the existing view of dashboard according to the latest mocks to mark the completion of MVP.
* Pull Requests: [https://github.com/oppia/oppia/pull/2126](https://github.com/oppia/oppia/pull/2126), [https://github.com/oppia/oppia/pull/2151](https://github.com/oppia/oppia/pull/2151)

#### Week #6:
* Additions to frontend view of dashboard in form of creating the card view for the dashboard.
* Pull Requests: [https://github.com/oppia/oppia/pull/2155](https://github.com/oppia/oppia/pull/2155), [https://github.com/oppia/oppia/pull/2170](https://github.com/oppia/oppia/pull/2170)

#### Week #7:
* Write a cron job to keep history of stats being recorded for each user. This kicks off a one-off map-reduce job to perform actual calculations.
* Tests for both cron job and one-off job.
* Pull Request: [https://github.com/oppia/oppia/pull/2173](https://github.com/oppia/oppia/pull/2173)

#### Week #8:
* Fetch and display open feedback in dashboard - frontend and backend changes along with tests.
* Pull Request: [https://github.com/oppia/oppia/pull/2239](https://github.com/oppia/oppia/pull/2239)

#### Week #9:
* Add realtime layer to statistics continuous job (written in the beginning) along with tests.
* Pull Request: [https://github.com/oppia/oppia/pull/2238](https://github.com/oppia/oppia/pull/2238)

#### Week #10:
* Calculate and display change in statistics relative to the previous week's data.
* Display new feedback on frontend separately.
* Pull Requests: [https://github.com/oppia/oppia/pull/2252](https://github.com/oppia/oppia/pull/2252), [https://github.com/oppia/oppia/pull/2281](https://github.com/oppia/oppia/pull/2281)

#### Week #11:
* Make creator dashboard UI responsive, so that it looks equally good on mobile devices as on desktops.
* Pull Request: [https://github.com/oppia/oppia/pull/2291](https://github.com/oppia/oppia/pull/2291)

#### Week #12:
* (Marked as busy)

#### Week #13:
* Work on adding sorting functionality to the list of explorations according to all the available parameters which are visible to the user, along with tests.
* Implement a dropdown which appears on clicking on each non-private exploration and displays most important statistical data to the user at once (PR for this is still not merged, due to a few failing tests!)
* Pull Requests: [https://github.com/oppia/oppia/pull/2296](https://github.com/oppia/oppia/pull/2296), [https://github.com/oppia/oppia/pull/2318](https://github.com/oppia/oppia/pull/2318)


### Future of the Project:

* Write end-to-end tests for the creator dashboard ([issue #2403](https://github.com/oppia/oppia/issues/2403)).
* Add support for pagination of content in dashboard (was partially implemented in [pull request #2265](https://github.com/oppia/oppia/pull/2265) before deciding to discontinue it for the time being).
* Collect and display statistics for collections as well, and not just individual explorations.


## Conclusions:

Firstly, I would like to thank Google for enabling students to participate in open source development through GSoC, the whole of Oppia community for accepting my project proposal and letting me embark on this fantastic adventure, and most importantly my mentors - [Sean Lip](https://github.com/seanlip), .[Xinyu Wu](https://github.com/wxyxinyu) and [Allan Zhou](https://github.com/AllanYangZhou) for being there to help me.

Well, during this 3 months of GSoC, I learn a lot. I did the best that I could do with my knowledge and help from the community. And though I can say that most of my work is concluded, there’s still a PR left unmerged, a few ongoing PRs involving work unrelated to GSoC and some more code I've promised to write. And I’m happy to do that!


## Useful Links:

#### All commits to Oppia:

[https://github.com/oppia/oppia/commits/develop?author=526avijitgupta](https://github.com/oppia/oppia/commits/develop?author=526avijitgupta)

#### GSoC Project:

[https://summerofcode.withgoogle.com/projects/#5419488019218432](https://summerofcode.withgoogle.com/projects/#5419488019218432)

#### Accepted proposal:

[https://github.com/oppia/oppia/wiki/pdfs/GSoC2016AvijitGupta.pdf](https://github.com/oppia/oppia/wiki/pdfs/GSoC2016AvijitGupta.pdf)



[1]: https://github.com/526avijitgupta/526avijitgupta.github.io/raw/master/assets/images/dashboard.png