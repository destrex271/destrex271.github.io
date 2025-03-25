Beginning Google Summer Of Code 2023 @ PostgreSQL

Beginning Google Summer Of Code 2023 @ PostgreSQL
=================================================

---

### Beginning Google Summer Of Code 2023 @ PostgreSQL

![](https://cdn-images-1.medium.com/max/800/0*4UyilswL0EG8RDfS.png)

I am excited to announce that I have been offered the opportunity to work as a contributor at PostgreSQL under Google Summer Of Code 2023. I would like to thank my mentors [Stephen Frost](https://www.linkedin.com/in/stephen-frost/) and [Ilaria Battiston](https://www.linkedin.com/in/ilaria-b-a53014175/) for providing me with this amazing opportunity.

This blog contains all the information about the project that I would be working on this summer. You can post any suggestions related to what can be improved in this project in the comment section.

### The Project

PostgreSQL had a lot of amazing and exciting projects for this summer, ranging from fixes on their official website to adding new features to the main PostgreSQL codebase. You can check out these amazing project ideas [here](https://wiki.postgresql.org/wiki/GSoC_2023).

I decided to go with [Creating a PGWeb Testing Harness(2023)](https://wiki.postgresql.org/wiki/GSoC_2023#Creating_a_pgweb_testing_harness_.282023.29). This project is concerned with our official [PostgreSQL website.](https://www.postgresql.org/) This website has been built using the Django Framework available in python. Although the changes to this website are not that frequent but when there are any changes introduced, some bugs eventually were introduced in the codebase and since there was no system in place to detect these bugs, they eventually persisted until the developers had to spend hours to fix them.

Therefore in order to reduce this workload of checking manually for bugs in the website, a Testing Harness Suite was proposed for the website. This suite should integrate with a CI/CD pipeline and should help in generating Bug Reports for the website.

### Proposed Solution

I had worked on a similar project called WebActuary with [Arav Jain](https://github.com/DarthBoson) back in 2021. To know more about it you can check it out [here](https://github.com/destrex271/WebActuary). Naturally, My interest was piqued.

The current solution proposes the use of [Django Test Client](https://docs.djangoproject.com/en/4.2/topics/testing/tools/) to develop this suite(earlier it was going to be selenium with a bunch of other tools, thanks to Jonathan S. Katz from the psql-www community for proposing Django Test Client as a much more viable solution). The Django Test Client provides a lot of ways to test almost each and every functionality of the website. It is also very easy to run as well. Especially the [LiveServerTestCase](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.LiveServerTestCase) class provides us with the functionality to use Selenium for our tests.

The core tests include Functionality tests. These involve checking if all the links within the website are working, whether or not the forms are working and is the data actually being stored in the database, cookies etc. These tests also check for bugs in rendering of dynamically generated pages, which have been very problematic for the website developers of PostgreSQL, and some security vulnerabilities as well.

### Where are we as of now?

![](https://cdn-images-1.medium.com/max/800/1*AgLRYIbiQkyZ85usKbfRPw.png)

**Proposed Solution Flow**

Lets dive into the exact solution then!

According to the flowchart above our CI/CD pipeline triggers all these tests, although it does miss some crucial components that I figured out with the help of my mentors and the amazing psql-www community.

For our CI/CD pipeline, we are using Github Actions as they are pretty easy to use and they also reduce the work that goes into setting up a pipeline a lot. The workflow goes as follows:

Here you can see that the CI/CD pipeline fires up whenever there is a change in the main branch. This CI/CD pipeline fires up a bash script which basically sets up the entire container to run the main PGWeb repository.

It clones the main repository for [PGweb](https://github.com/postgres/pgweb) and the [tests repository](https://github.com/destrex271/pgweb-testing-harness) as well, installs all the required dependencies and copies all the test files to the pgweb directory and then runs the tests using the command

As you can see the naming convention for the tests goes as `tests_*.py` . Therefore in the future if anyone wants to add any tests for the website, they can easily do so by just adding a file with the similar naming convention to the respective folder in the repository.

### Conclusion

So for now the CI/CD pipeline has been setup successfully, thanks to the support of the psql-www community and my mentors [Stephen Frost](https://www.linkedin.com/in/stephen-frost/) and [Ilaria Battistion](https://www.linkedin.com/in/ilaria-b-a53014175/).

The next stages of the project in the **Coding Period** that begins from May 29th will include addition of various functional tests, especially this week I aim to implement the form and link functionality tests.

If you have any suggestions regarding the project or any changes you would like to propose kindly mention them in the comments or email me at [destrex271@gmail.com](mailto:destrex271@gmail.com). You can even raise an issue on the main Github repository of the project (link given below)!

Github Repository: <https://github.com/destrex271/pgweb-testing-harness>

Thanks a lot for reading! I hope you enjoyed it and would continue to follow this project to the end.

By [Akshat Jaimini](https://medium.com/@destrex271) on [May 29, 2023](https://medium.com/p/a4cc6f350c23).

[Canonical link](https://medium.com/@destrex271/beginning-google-summer-of-code-2023-postgresql-a4cc6f350c23)

Exported from [Medium](https://medium.com) on March 25, 2025.