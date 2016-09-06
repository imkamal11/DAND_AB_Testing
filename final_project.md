# A/B Testing
## Experiment Summary
At the time of this experiment, Udacity courses currently have two options on the home page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. This screenshot shows what the experiment looks like.

![alt final screenshot](./Final Project_ Experiment Screenshot.png)

The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.


## Experiment Design
### Metric Choice
#### Invariant Metrics
Invariant metrics should not change across experimental or control groups. 

And with this definition in mind, the metrics below were choosen (Number of cookies, Number of clicks and Click-through probability) because the intervention occurs after the point where the metrics are measured, therefore, the experiment will have no direct effect on any of the metrics, i.e the metrics should not change, making them a good choice as in invariant metric

**Number of cookies**: The number of unique cookies to view the course overview page. This is a population sizing metric to be split evenly between the control and the experiment group. 

**Number of clicks**: The number of unique users/students (unique cookies) that click on the "start free trial" button. Here the button is clicked prior to the free trial screen appearing.

**Click-through-probability**: The number of unique cookies to click on the "start free trail" button divided by the number of unique cookies to view the course overview page.

**Number of User-Ids**: (Not Used) The number of users who enrolled in the free trial. Since we're interested in the proportion of unique cookies that click on the "start free trial" button, i.e the probability of enrolling, this metric would not give us any useful information and therefore it was not used as an invariant metric. 

#### Evaluation Metrics
Evaluation metrics are expected to change over the experiment with differences observed between the experimental and control groups. If the hypothesis is true, the number of user-ids to enroll would be reduced, eliminating the unprepared students, with payments/checkouts not decreasing. 

In order to launch the experiment, we want to decrease the enrollment of unprepared students, i.e the gross conversion should decrease, while not reducing the number of students who complete the free trial and make a payment, i.e the net converion should either stay the same or go up.

**Gross conversion**: The number of user-ids that enroll in the free trial divided by the number of unique cookies to click on the "start free trial" button. The number of enrollments can be affected by the experiment and as a result the gross conversion; therefore this will be used as an evaluation metric. There should be a statisticial significant reduction in enrollment.

**Retention**: The number of user-ids that stayed enrolled past the 14 day free trial (made a payment) divided by the number of unique cookies that clicked on the "start free trial" button. The number of payments can be affected the experiement and retention values; therefore this will be used as an evaluation metric.

**Net conversion**: The number of user-ids to remain enrolled past the 14 day free trial (made a payment) divided by the number of unique cookies that clicked on the "start free trial" button. The number of payments can be affected by the experiment and as a result the net conversion, this will be used as an evaluation metric. There should be a statisticial significant increase in payment/continued enrollment after the free trial.

### Measuring Standard Deviation
Evaluation Metric | Standard Deviation
--- | ---
Gross Conversion | .0202
Retention | .0549
Net Conversion | .0156

The number of clicks and enrollments both follow a binomial distribution. The standard deviation is computed with - sqrt(p(1-p)/n)

The standard deviation calculated for each sample has a size of 5000 unique cookies visiting the course overview page. Please see [Baseline Values](https://docs.google.com/spreadsheets/d/1MYNUtC47Pg8hdoCjOXaHqF-thheGpUshrFA21BAJnNc/edit#gid=0) - the standard deviations are calcuated using these baseline values.

Based on the 3 evaluation metrics, the analytical standard deviation will likely match the empirical standard deviation as the units of diversion for the experiment and analysis is cookies. While for the metric retention, given that the units of diversion and analysis are different (user-id vs cookies), it is likely that the analytical standard deivation and the emperical standard deviation will not match.

### Sizing
#### Number of Samples vs. Power
The Bonferroni Correction was not used during the analysis phase. The number of page views required (largest sample size) to conduct this experiment is: 4,741,212

Metric | Pageviews
--- | ---
Gross Conversion | 646,450
Retention | 4,741,212
Net Conversion | 685,325

**alpha value of 0.05 and beta value of 0.2 is used**

#### Duration vs. Exposure
Given the low risk and lack of sensitive data being collected, I would divert 100% of the traffic. With approx. 40,000 page views per day, the experiment would take roughly 119 days. However, this time period is too long to conduct an experiment for Udacity. Revising my previous decision, retention will no longer be used as an evaluation metric. 

New evaluation metrics are Gross Conversion and Net Conversion. The new number of page views required is 685,325 and the experiment will now require 18 days to complete. Note that if other experiments need to be conducted simutaneously, the percentage diversion can be reduced.

Metric | Duration
--- | ---
Gross Conversion | 17
Retention | 119
Net Conversion | 18


## Experiment Analysis
[Control and Experiment data](https://docs.google.com/spreadsheets/d/1Mu5u9GrybDdska-ljPXyBjTpdZIUev_6i7t4LRDfXM8/edit#gid=0) provided by Udacity and used throughout this section.
### Sanity Checks
Below is the computed 95% confidence inteval for the listed invariant metrics

Invariant Metric | Lower Bound | Upper Bound | Observed | Pass/Fail
--- | --- | --- | --- | ---
Number of Cookies | .4988 | .5012 | .5006 | Pass
Number of Clicks | .4959 | .5041 | .5005 | Pass
Click-through Probability | .0812 | .0830 | .0822 | Pass

### Result Analysis
#### Effect Size Tests
Below is the computed 95% confidence interval around the difference between the experiment and control groups. 

Evaluation Metric | Lower Bound | Upper Bound | Statisticially or Practically Significant
--- | --- | --- | ---
Gross Conversion | -0.0291 | -0.012 | Yes (statisticially and Practically)
Net Conversion | -0.0116 | .0019 | No (statistically and Practically)

#### Sign Tests
Below is the computed sign test using the day-by-day data.

Evaluation Metric | p-value | Statistically Significant
--- | --- | ---
Gross Conversion | 0.0026 | Yes
Net Conversion | 0.6776 | No

#### Summary
The Bonferonni correction was not used in my analysis. The Bonefonni correction is a method to limit / control the risk of Type 1 errors in multiple independent metrics comparisons. If one metric was used to base our decision then the Bonferonni correction would have been appropriate; however, two affects were considered, gross conversion and net conversion 

The sign and effect size test both showed gross conversion to be statistically significant, while net conversion is not. 

### Recommendation
Analysis of the screener provided by gross conversion indicates that the experiment was successful at reducing the number of unprepared students who enrolled in the free trial. However, net conversion showed that the screener negatively affected the number students that would continue past the free trial, reducing the number of students making a payment. 

Based on these results, I would recommend against launching the change.


## Follow-Up Experiment
During the 14 day trial students are left alone to complete the videos and project work without direct interaction from Udacity. As a follow-up experiment I would capture, via user-id, the number of hours each student has spent watching videos and going over quizes with some type of approximation reviewing reading material. If a student's time is lacking behind the pace of the recommended commitment hours by Udacity, then a pop up message for the student informing them they're tracking a bit behind and providing recommendations on how to catch up.

The hypothesis is that a kind reminder early on in the process will help the student in two ways 1) give students a reference check on their progress and 2) provide students with resources allowing them to pick up the path. In turn, this will either "weed out" more students who just can't dedicate the time while also encouraging other students to work harder to make the deadlines. Students on pace or ahead of schedule would not see the pop up message.

I would use the user-id as the unit of diversion, enrolled students only, with the number of user-ids as an invariant metric and number of payments divided by the number of unique user-id's as an evaluation metric.

The number of students who enroll should not change across experimental or control groups so it's a good candidate for an invariant metric, while the number of payments / completed free trials divided by the number of user-ids should change over experimental and the control group and can therefore be used as an evaluation metric.

## Reference
* https://en.wikipedia.org/wiki/Sign_test
* https://en.wikipedia.org/wiki/Effect_size
* http://docs.statwing.com/examples-and-definitions/t-test/effect-size/
* http://graphpad.com/quickcalcs/binomial1/
