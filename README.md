# AB Testing
AB Testing Notes from Udacity course https://classroom.udacity.com/courses/ud257

## Contents
1. Overview


## 1. Overview
A/B testing is a general methodology used to test a new product or a feature. Users are split in two groups, control set exposed to exsisting version of product of feature and a new group, experiment set exposed to new version of the feature and measure how do these users behave differently in order understand which feature is better. <br>

A/B testing is useful for <br>
* New feature <br>
* Personalized recommendation <br>
* Ranking changes<br>
* Latency changes<br>

A/B testing is not useful for new experience/ change of version, due to 2 major issues.<br>
* It may result in <i>change aversion</i> (where users don’t like changes to the norm), or<br>
* a <i> novelty effect </i> (where users see something new and test out everything).<br>

what happens is: <br>
* what is  baseline for comparison? <br>
* how much time you need for user to adapt to new experience, so you can say what is going to be the plateaud experience and make a robust decision <br>

<b> A/B testing cannot tell you if you are missing something. </b> <br>
eg. let's say youre one a digital camera review site, A/B testing can tell you if you should x camera review above y camera review, but what it can not tell is if you are missing a z camera that you should be reviewing and you are not doing at all.


#### Other techniques.
Complimentary Analyze users logs retrospectively or observationally and see if a hypothesis can be developed of whats causing changes in their behaviour, using this you can randomize and design an experiment and do a perspective analysis.
User experiment research, surveys, human focus groups give deep quanlitative data whereas A/B testing gives broad quantitative data.



Example Audacity learning website wants to test a change on Audacity page. <br>
<b>Experiment:</b> <br>
Hypothesis: Changing the "Start Now" button from orange to pink will increase how many students explore Audacity course
#### Metric choice:
1. Click through rate = Number of Clicks / Number of page vists (Measure usability)
2. Click through probability = unique vistors who clicked / unique visitors to page (Measure total impact)

In our case we will use click-through probability as we want to measure the impact

<b> How to compute rate & probability? </b> </br>
<b> Rate: </b> on every page view you capture the event, and then whenever a user clicks you also capture that click event <br>
Sum(Page views)/ sum(clicks) <br>
<b> Probability: </b> match each page view with all of the child clicks, so that you count, at most, one child click per page view.

#### Distribution
We have exactly 2 different outcomes, click and no click.
#### Binomial Distribution

For a binomial distribution with probability 𝑝 , the mean is given by 𝑝 and the standard deviation is sqrt(𝑝×(1−𝑝)/𝑁) where 𝑁 is the number of trials.

A binomial distribution can be used when <br>
* The outcomes are of 2 types 
* Each event is independent of the other 
* Each event has an identical distribution (i.e. 𝑝 is the same for all)

We expect click-through probability to follow a binomial distribution


<b>Confidence Interval</b> <br>
Benefit of knowing binomial distribution is we can use the formula for sample standard error for binomial distribution to measure how variable we expect our overall probability of click to be. For 95% confidence interval, if we repeat our experiment over and over again we can expect the interval we construct around our sample mean to cover the true value of our population 95% of the time.


phat = X / N (# users who clicked/ # users)

Lets say; X = 100 and N = 1000 <br>
phat = 0.1

To use normal distribution check N * phat > 5 and N * (1-phat) > 5 

margin of error m = z * SE
m = z * sqrt( (phat * (1 - phat))/ N ) <br>
m = 1.96 * sqrt( (0.1 * 0.9) / 1000) <br>
m = 0.01859 <br>
so confidence interval @95% is (phat - m, phat + m)

(0.1 - 0.019, 0.1 + 0.019) <br>
so we would see between 81 ~ 119 click


Refrences:

https://classroom.udacity.com/courses/ud257

https://www.evanmiller.org/ab-testing/sample-size.html

https://exp-platform.com/hbr-the-surprising-power-of-online-experiments/

https://www.udacity.com/api/nodes/3954679115/supplemental_media/additional-techniquespdf/download
