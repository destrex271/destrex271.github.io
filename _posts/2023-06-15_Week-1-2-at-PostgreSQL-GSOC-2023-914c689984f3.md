Week 1–2 at PostgreSQL@GSOC 2023

Week 1–2 at PostgreSQL@GSOC 2023
================================

As I documented in my previous blog which you can find here, the official coding period for GSOC 2023 began on 29th May. Here I will share…

---

### Week 1–2 at PostgreSQL@GSOC 2023

![](https://cdn-images-1.medium.com/max/800/1*Dvigwgu1tXFqhBAiLKID4A.png)

As I documented in my previous blog which you can find [here](https://blog.devgenius.io/beginning-google-summer-of-code-2023-postgresql-a4cc6f350c23), the official coding period for GSOC 2023 began on 29th May. Here I will share all the tasks that I accomplished in the 1st week.

### Work Done Till Now

The primary focus of the Pgweb Testing Harness is to check the functionality of the latest build of the website, so to facilitate that as mentioned in the previous blog, I had setup a Github Action to check for updates to the main repo and another action to execute the tests as soon as new tests are pushed.

Although report generation is still left to be added to the testing suite.

In the first week most of my work involved setting up the above mentioned actions and adding the following functionality tests for the codebase.

### Link Tests

These functional tests include checking all the links on the website and ensuring that none of them are broken, both internal and external.

One approach would have been to go through each and every page of the website manually to check for links but instead I followed an approach that adds a program similar to a crawler for the codebase.

As soon as these set of tests are fired, the program starts from the Home page of the website and opens each and every page aka *internal links* in terms of the testing suite. This crawler then segregates all the links as internal and external and runs tests to ensure that they return a valid GET response. This ensures that the website has no broken links.

Although these tests are failing for content like news and lists which utilizes other codebases like [*pgarchive*](https://git.postgresql.org/gitweb/?p=pgarchives.git;a=summary)*.*

Therefore there are some changes to be made to the existing setup to ensure that these services are also running, but since it is separate from the pgweb codebase, I am going to tackle that later as the project mainly focuses on the pgweb codebase.

Selenium has been used in combination with the Django Test Client to execute these tests.

### Form Tests

These tests involve checking all the forms on the website and ensuring that they work properly. Since each form is unique this requires me to add different tests for different forms unlike the link tests where I was able to figure out a generalized approach.

As of now I have completed the tests for Authentication and Registration forms as well as the form which allows Organization members to inform the PostgreSQL community about their upcoming events.

Although these tests differ a lot in terms of the fields and the data to be entered, they do follow the following steps:

1. Check if input data is ***valid***
2. Check if a subsequent confirmation message has been displayed on submitting the form
3. Check if the data has been ***added to the database*** in case of a *positive response*.

### Bug Fixes

Well as I started to add more tests to the codebase I realized there was a major bug in the Monitoring Action Script.

My previous approach relied on the fact that the container has a clone of the pgweb repository and if I check against that repository I might be able to check for changes but in github actions the containers created neither persist their data nor their state, therefor it was impossible for the script to run as a cronjob in the container as the container only started when the actions were triggered.

Therefore I changed the entire approach. First of all I modified the monitoring script and broke it into two parts -

1. Commit Checker
2. Commit Value Updater

The first script would pull the repository and check the commit ID of the last commit, if it matched the commit id stored in the file commit\_id.txt on the testing suite repository, it meant that there were no updates and vice versa. In case there is an update the pipeline is triggered and the Commit Value Updater Script updates the value in the commit\_id.txt file and pushes the changes via Github Dependabot to the repository.

Both the scripts are as follows:

And the modified action which enables these scripts to run as a cron job is:

### Conclusion

Apart from this bug fix, most of my time also went in going through the official documentation of the pgweb repository as i found out that the main PostgreSQL website has multiple modules backing it up. It is truly an amazing piece of software. The content management system enforced on this website is really cool and even the process to load documentation etc.

So for the next week I would be adding more tests to the codebase! If you have any suggestions do leave them in the comments sections and checkout the repository [here](https://github.com/destrex271/pgweb-testing-harness).

By [Akshat Jaimini](https://medium.com/@destrex271) on [June 15, 2023](https://medium.com/p/914c689984f3).

[Canonical link](https://medium.com/@destrex271/week-1-2-at-postgresql-gsoc-2023-914c689984f3)

Exported from [Medium](https://medium.com) on March 25, 2025.