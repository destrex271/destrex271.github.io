Week 5–6 @ PostgreSQL, Google Summer Of Code’23

Week 5–6 @ PostgreSQL, Google Summer Of Code’23
===============================================

Hello There!

---

### Week 5–6 @ PostgreSQL, Google Summer Of Code’23

![](https://cdn-images-1.medium.com/max/1200/0*qnI7YBhC8Tnk5t3n.png)

Hello There!

This is the 4th installment in my biweekly series for the duration of GSoC’23 @ PostgreSQL. For a quick recap, the project that I have been working on is to develop a testing suit for the official PostgreSQL website. You can read more about this [here](https://github.com/destrex271/pgweb-testing-harness/).

### Progress Made In This Week

This week almost all the tests related to form data submissions were completed. I also realized that although I was checking that the data was being stored correctly I was not checking if it was being rendered as intended on the respective pages.

Well you might say that this isn’t that much of a problem, but there have been some rendering related issues earlier with the website and therefore I think it would be in the best interest to cover as many features as I can in this project to ensure that the testing suit is actually useful for the website developers.

The second feature that I worked on was to render the logs as an artifact after each run so that the developers can easily identify what all tests passed and which ones failed. But there is a problem with this approach, GitHub only allows artifacts to persist for a duration of 90 days but if any of the logs are required later they won’t be archived, therefore I need to store them using a database or some cloud storage.

### Documentation Rendering

After all these tests were completed I shifted my focus to another problem that was pointed out early on in the community bonding period. If you have ever visited the PostgreSQL website, you might have noticed the amazing documentation that seems to be integrated into the website so beautifully making you think that this might have been a webpage written manually by a person. Well guess what, its all automated!

I was shocked myself! The entire process is really beautiful. For each release a tarball file is prepared which contains all the required content for the documentation. A custom script in the pgweb repository, named [docload.py](https://github.com/postgres/pgweb/blob/master/tools/docs/docload.py) is responsible for this magic. It inserts the documentation of each minor release into its Version Tree.

To test this rendering process I needed to use this script with some changes that worked with my [setup script](https://github.com/destrex271/pgweb-testing-harness/blob/main/src/workflow_utils/setup.sh). But there was no way I was going to manually download and place all the files in repository.

Therefore I used another approach. I wrote a script which scraped the ftp server of PostgreSQL(where all the docs are available) and downloaded the documentation of some of the version. I even wrote the functionality to form a fixture using the data obtained and inserting it into the database using the *loaddata* command. This would populate the version table so that the corresponding documentation can be loaded easily. The script is as follows:

This script fits into the setup.sh script and introduces the Docloading process in the normal flow of the test setup.

### Conclusion

So that was it for this week. This project has evolved in a much different way that I had imagined in the beginning. Almost one half of the project has been completed before the Mid Term Evaluations and I could not have been more grateful for the amazing guidance provided by my mentors [Stephen Frost](https://www.linkedin.com/in/stephen-frost/) and [Ilaria Battiston](https://www.linkedin.com/in/ilaria-b-a53014175/).

The project has come to a stage where every new module can be easily inserted in the normal workflow, just like Legos and I could not have been happier with this outcome. I hope this project evolves in the journey left.

You can checkout the repository [here](https://github.com/destrex271/pgweb-testing-harness). As usual, if you have any suggestion, kindly drop them in the comments section or you can send a mail to me at [*destres271@gmail.com*](mailto:destrex271@gmail.com) or you can raise an issue on the [project repository](https://github.com/destrex271/pgweb-testing-harness) as well!

By [Akshat Jaimini](https://medium.com/@destrex271) on [July 10, 2023](https://medium.com/p/d74ec1dff8f8).

[Canonical link](https://medium.com/@destrex271/week-5-6-postgresql-google-summer-of-code23-d74ec1dff8f8)

Exported from [Medium](https://medium.com) on March 25, 2025.