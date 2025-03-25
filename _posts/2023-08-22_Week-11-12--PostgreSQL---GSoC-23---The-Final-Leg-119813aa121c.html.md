Week 11–12, PostgreSQL @ GSoC’23 — The Final Leg

Week 11–12, PostgreSQL @ GSoC’23 — The Final Leg
================================================

Hello Everyone!

---

### Week 11–12, PostgreSQL @ GSoC’23 — The Final Leg

![](https://cdn-images-1.medium.com/max/800/0*WwyO8vXR8fmjnM2M.jpg)

Hello Everyone!

This is the final installment in my Google Summer of Code 2023 Devlogs as we approach the end of this season. It has been an amazing journey so far, the mentors have been amazing and helped me whenever I got stuck on a problem.

### Quick Recap

Last week, work was done on enhancing the URL tests and submitted the patch which is yet to be reviewed by the community members. Work was also done on validation of multiple URL & markdown fields.

### Accessibility Testing

As we discussed in the last blog, accessibility tests were added to the testing suite. For this we are using a simple to use tool —[Unlighthouse](https://unlighthouse.dev/integrations/ci). This tool using Google Lighthouse to crawl the entire development build to check for accessibility issues. Currently we are generating a csv report but soon we’ll be shifting to a report format which will be able to host itself on the internet for easier accessibility.

### Error Reporting Using Email

As discussed in the last blog, there was no error reporting mechanism as such. So we added a new script which uses [smtplib](https://docs.python.org/3/library/smtplib.html) library available in python. The email template generated consists of all the reports attached and a link to the action run that generated the email. Whenever any tests fail, the script is run. The script is as follows:

### Conclusion

With this the base of the testing suite has been completed!

Now the project is open for contributions and we hope that this tool helps the amazing PostgerSQL-www community in their effort to maintain the official PostgreSQL website.

To checkout the project and raise issues and provide suggestions kindly check it [here](https://github.com/destrex271/pgweb-testing-harness/tree/main).

Thanks for following our journey!

By [Akshat Jaimini](https://medium.com/@destrex271) on [August 22, 2023](https://medium.com/p/119813aa121c).

[Canonical link](https://medium.com/@destrex271/week-11-12-postgresql-gsoc23-the-final-leg-119813aa121c)

Exported from [Medium](https://medium.com) on March 25, 2025.