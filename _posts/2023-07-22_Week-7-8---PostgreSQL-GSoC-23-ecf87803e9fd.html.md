Week 7–8 , PostgreSQL@GSoC’23

Week 7–8 , PostgreSQL@GSoC’23
=============================

Hello there!

---

### Week 7–8 , PostgreSQL@GSoC’23

![](https://cdn-images-1.medium.com/max/800/0*cbK7YH1ILCPFMZsg.png)

Hello there!

This blog is a part of my ongoing Google Summer of Code 2023 journey, at PostgreSQL where I am developing a Test Harness Suite for the official [PostgreSQL website](https://www.postgresql.org/).

### Quick Recap

Last week the mid term evaluation for the project took place and I was able to clear it with the guidance of my mentors. The project is now almost in its final stages with most of the functional tests completed as we speak as of now. There were some bugs that would be discussed later. For now the CI/CD pipeline is active, and the monitoring utility for the main website is also running successfully. For now we are using the log files (stored as artifacts) of the test run.

### Bugs, Bugs, Bugs

It happens so often that we write a piece of code to discover that it isn’t working as intended. The same happened with me in this project.

#### #1

One of the functional tests in the suite crawls the development build of the website to check if the links present are working or not. This had been one of the common issues on the website so this test was very crucial for the success of this testing harness but for some reason the test was only crawling the homepage.

Fixed the recursive calling issue by implementing a mixture of a queue and a set. It also records the root page for each link and prepares a log report with the status code and the root url which is now uploaded as a artifact. Also limited the use of selenium and replaced most of its sections with Beautiful Soup 4.

#### #2

The second issue was related to the documentation test implemented in the last blog. One of the major problems that I came across were related to the slow speeds at which the documentation testing was taking place. Earlier I was using selenium which was almost taking indefinite time to finish the tests. To minimize this time I switched over to Beautiful Soup library since it was much faster at processing static content.

But the problem was not solved completely as the tests were taking about 5–6 hours which is still too much. To fix this I studied about the concurrent library in python which allows for the creation of a ThreadPool, you can check the implementation here:

As you can see the ThreadPoolExecutor allows us to create a dynamic number of threads and execute the same function with different arguments simultaneously. This sped up the process a lot and allowed the doc tests to finish within 5 minutes! This was eureka method for me, as the time taken was changed from indefinite -> 5–7 hours -> 5mins

### Other Tests

Added new tests for the profile section of the website, testing the update and delete features with respect to the secondary email address. These tests were pretty small.

### The Road Ahead

So after this some other tests like the accessibility tests also are left to be added. We are also going to develop a notification system to warn the members if there have been any bugs detected by our Testing Harness Suite. Now we have finally entered into the second half of the project and I hope my work did contribute something to the community.

If you have any doubts or suggestions, kindly drop them in the comment section bellow and Thanks for Reading!

By [Akshat Jaimini](https://medium.com/@destrex271) on [July 22, 2023](https://medium.com/p/ecf87803e9fd).

[Canonical link](https://medium.com/@destrex271/week-7-8-postgresql-gsoc23-ecf87803e9fd)

Exported from [Medium](https://medium.com) on March 25, 2025.