Week 9–10, PostgreSQL@GSoC’23

Week 9–10, PostgreSQL@GSoC’23
=============================

Hello everyone!

---

### Week 9–10, PostgreSQL@GSoC’23

![](https://cdn-images-1.medium.com/max/800/0*RU5q387QsOJwSDd7.png)

Hello everyone!

This blog is a part of my ongoing Google Summer of Code 2023 journey, at PostgreSQL where I am developing a Test Harness Suite for the official [PostgreSQL website](https://www.postgresql.org/).

### Quick Recap

As discussed in the previous blog I had fixed some bugs in the url test script earlier that allowed for crawling the entire website and report broken urls. Although some bugs came up this week that would be discussed later. I had also increased the speed at which the documentation load tests were working.

### Enhancing the URL Tests

Last week after deploying the URL test script we realized that there was a really big problem with the flow. Although the crawling approach was able to pickup broken links that had been hard coded in the website, it was not able to pickup any user generated content since the tests were to test the deployment build and to check for valid links in the user generated content we needed the live production data.

Now this is a big problem because one of the main goals of the testing suite was to stay as isolated from the pgweb codebase as possible but this particular problem could not have been ignored.

Therefore with the help of my mentors, we decided to split the functionality into 2 parts. For now the crawler tests have been deactivated on the testing harness and instead of accessing the prod database directly we decided to add the following

1. Add inbuilt validation in the website fields that deal with URLs in any way, be it any markup field or any field specifically accepting URLs.
2. Setup a cronjob on the production server which scans specific tables in the database and check if the url related fields present in them don’t have any broken links

This might seem to be a tangent from the testing suite, I felt the same too, but that is only because the idea looks a little excessive from the surface.

If you think about it as a way to make the development of the PostgreSQL website more test driven, it makes perfect sense.

The brute-force approach might be to scan all the tables(except the auth tables) and guess which field consists a url. This would also mean that if a new table is added, the data in that table would be validated as well without making any changes to the script.

***Sounds good right? Well you are wrong by a long shot!***

That was me a week before from now feeling that this approach would be good and ‘scalable’(I even wen ahead and added some fancy CLI output stuff *T\_T*) but then my mentors pointed out that it might pickup some fields that are not even required to be tested and generate unnecessary logs and overall it was a very bad idea to check the entire database just for the sake of validation. So after a lot of discussion we decided that our approach was going to be similar to what we did in the testing harness. Writing specific ‘tests’ like function that check the required fields in the tables that we know need validation. Also this would make the development more test driven. For example if a new table is added to the website later then a validation function ‘test’ would be added to the script as well!

**Now this sounds much much better in my opinion!**

The script scans these tables and provides the broken urls with all the details of its whereabouts in the database. This script along with the form validation patch would be sent to the mailing list. We’ve tried our best to utilize the tools available without introducing any big changes to the codebase. The patch is currently being tested by us and would be sent for review on the mailing list. Let’s hope this patch makes it to production!

#### Tackling markup validation

While writing the validation patches for existing forms on the website, one of the main problems was to test the links in the markup content. The problems were as follows:

1. Parsing markdown in a format giving a generic representation of a link
2. Extracting links that are meant to route to another page i.e. avoiding links that are just written as plain text
3. Avoiding any unnecessary dependency addition for these validation tests

My first approach was to use the markdown library(which was already a part of the pgweb codebase) to parse the markdown into HTML to get a more generic content representation.

Although parsing the content was not a big thing the next part was extracting the links, which was a little wiered. I could have used Beautiful Soup to parse this HTML, which I had actually done but in latter revisions my mentors suggested to find some other approach that would comply with the 3rd point mentioned above i.e reduce dependecies.

I tried to look for some existing packages that would help validate links in markdown content but the only thing I came close to was the urlify extension which converts text urls to embedded urls(i.e. wrap them within an anchor tag). After studying the code for that extension I figured out that regex might help in extracting URLs, but I was so wrong!

Lets take an example.

```
<a href="htp://kyllex.live"></a>  
<a href="https://kyllex.live"></a>
```

As you can see in the snippet above lets say this was the parsed content. You can clearly see that the first URL won’t work as the schema of the URL is malformed, but will the approach catch this problem? NO!

It will skip this URL therefore defeating the entire purpose of validation. Regex tends to have this problem and therefore the second approach was to pickup the anchor tags instead of links and extract the href part. The main problem was to clean the data due to varying formats but I was able to come up with an approach that utilized regex and cleaned the extracted data properly to provide a list of links to test. If the link is dead a validation warning would be thrown in the form while saving the it.

This patch is also under review for now and lets hope this one makes it to production too!

I’ll also be writing a separate extension to validate links within markup for the markdown library soon!(Yes another blog is coming soon after the GSoC series is completed ;))

### Back to the Harness

Well lets get back to the testing harness. One of the last tests was to check for accessibility guidelines compliance on the main website. I tried to integrate CLI tools instead of writing something myself to check for these issues, specifically checking for compliance with the [W3 accessibility rules](https://www.w3.org/WAI/standards-guidelines/).

These consist of multiple levels of validation therefore its better to use a tool specifically designed for this. I tried using Pa11y but eventually switched to [Google Lighthouse CLI](https://github.com/GoogleChrome/lighthouse) because of the amazing format in which the results were being reported in the form of a beautiful HTML report and even JSON. This would certainly help the users of the testing harness in increasing their productivity while solving these bugs. If you want to explore similar tools you can check of the official list of tools provided by w3c [here](https://www.w3.org/WAI/ER/tools/).

### Road Ahead

Now since only two weeks are left, I’ll be shifting my focus on the testing harness while also reviewing the above mentioned patches. In the upcoming last weeks I’ll be completing the accessibility tests such that it is able to crawl the entire website and generate a single report for all the pages. I am also going to setup a service which sends the logs in case of a failure to the concerned mailing lists(most prolly the pgsql-www mailing list) and a simple web page from where you can go to the GitHub Action run for a specific build of the website.

Thanks for reading!

If you have any suggestions or questions kindly write them in the comments section and do check out the repository of the project [here](https://github.com/destrex271/pgweb-testing-harness/). All contributions in any form, let it be changes to documentation, raising issues to adding more testcases are always welcome!

By [Akshat Jaimini](https://medium.com/@destrex271) on [August 5, 2023](https://medium.com/p/9e3fc29890e9).

[Canonical link](https://medium.com/@destrex271/week-9-10-postgresql-gsoc23-9e3fc29890e9)

Exported from [Medium](https://medium.com) on March 25, 2025.