Week 3–4, PostgreSQL@GSoC’23

Week 3–4, PostgreSQL@GSoC’23
============================

Hello everyone!

---

### Week 3–4, PostgreSQL@GSoC’23

![](https://cdn-images-1.medium.com/max/800/0*AYysGVsaEK3obr5X.jpg)

Hello everyone!

Welcome to the latest addition to my PostgreSQL@GSoC’23 series. You can checkout the previous blog [here](https://medium.com/dev-genius/week-1-2-at-postgresql-gsoc-2023-914c689984f3). For those who are new here you can checkout the details of the project [here](https://wiki.postgresql.org/wiki/GSoC_2023#Creating_a_pgweb_testing_harness_.282023.29) and checkout the project [repository](http://github.com/destrex271/pgweb-testing-harness/).

So, lets get on with this weeks changes.

### More Debugging!

Well this isn’t anything surprising but I quickly realized that some of the tests that I had written earlier would eventually break in future builds, for example, when I am checking the title of the webpages to check for redirection to the correct page, the test needs to check against a lower case version of that title because it is very much possible that a change might be introduced later.

I soon realized that some other small changes that might seem not worth caring about earlier do become important when preparing a test case. We also need to setup our tests for each edge case.

### Report Generation

One of the major problems as of now was that the tests were running but the output was not being stored in some form of report. Also when a test fails, GitHub actions does not indicate the run as failed which will be fixed later on.

For now one of the possible approaches is to get the output of stdout and stderr in a log file and represent that log file in a much better way.

Development on a portal to view tests for each build has been started as well and hopefully it will be completed.

### Road Ahead

As of now I am lacking behind a lot in the process of completing this project. Functional tests are still left to be completed and other tests are yet to be started but it will be completed within these upcoming weeks before the midterm evaluation.

Most of the functional tests are related to the various forms on the website and checking data integrity on submitting these forms, once these are completed we’ll move on to accessibility and security tests for the website. As usual if you have any suggestions kindly drop them in the comments section below or you can raise an issue on the [GitHub Repo](http://github.com/destrex271/pgweb-testing-harness/) as well or you can [email](mailto:destrex271@gmail.com) me as well.

By [Akshat Jaimini](https://medium.com/@destrex271) on [June 27, 2023](https://medium.com/p/13b4bbb4c54a).

[Canonical link](https://medium.com/@destrex271/week-3-4-postgresql-gsoc23-13b4bbb4c54a)

Exported from [Medium](https://medium.com) on March 25, 2025.