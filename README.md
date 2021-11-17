# AB Testing
AB Testing Notes from Udacity course https://classroom.udacity.com/courses/ud257

## Contents
- [1. Overview](#overview)
  - [1.1 Metric Choice](#metric-choice) 
  - [1.2 Distribution](#distribution) 
  - [1.3 Confidence Interval](#confidence-interval) 
  - [1.4 Hypothesis Testing](#hypothesis-testing) 
  - [1.5 Standard Error](#standard-error) 
  - [1.6 Calculating Results](#calculating-results) 
  - [1.7 Conclusion](#conclusion) 


## 1. Overview  <a name="overview"></a>
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
### 1.1 Metric choice <a name="metric-choice"></a>
1. Click through rate = Number of Clicks / Number of page vists (Measure usability)
2. Click through probability = unique vistors who clicked / unique visitors to page (Measure total impact)

In our case we will use click-through probability as we want to measure the impact

<b> How to compute rate & probability? </b> </br>
<b> Rate: </b> on every page view you capture the event, and then whenever a user clicks you also capture that click event <br>
Sum(Page views)/ sum(clicks) <br>
<b> Probability: </b> match each page view with all of the child clicks, so that you count, at most, one child click per page view.

### 1.2 Distribution <a name="distribution"></a>
We have exactly 2 different outcomes, click and no click.
#### Binomial Distribution

For a binomial distribution with probability 𝑝 , the mean is given by 𝑝 and the standard deviation is sqrt(𝑝×(1−𝑝)/𝑁) where 𝑁 is the number of trials.

A binomial distribution can be used when <br>
* The outcomes are of 2 types 
* Each event is independent of the other 
* Each event has an identical distribution (i.e. 𝑝 is the same for all)

We expect click-through probability to follow a binomial distribution


### 1.3 Confidence Interval <a name="confidence-interval"></a>
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

### 1.4 Hypothesis testing <a name="hypothesis-testing"></a>
We want to calculate what is the probability that the results are due to a chance <br>
H<sub>o</sub>: <i>P</i><sub>exp</sub> -  <i>P</i><sub>cont</sub> = 0 <br>
H<sub>A</sub>: <i>P</i><sub>exp</sub> -  <i>P</i><sub>cont</sub> ≠ 0

### 1.5 Standard Error   <a name="standard-error"></a>
 <a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" title="{\hat{P} = \frac{X_{cont}+ X_{exp}}{N_{cont}+ N_{exp}}}" /></a>


<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" title="{\hat{P} = \frac{X_{cont}+ X_{exp}}{N_{cont}+ N_{exp}}}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;SE_{pool}&space;=&space;\sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}&plus;\frac{1}{N_{exp}})}" target="_blank"><img style="background: white;" src="https://latex.codecogs.com/svg.latex?\bg_white&space;SE_{pool}&space;=&space;\sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}&plus;\frac{1}{N_{exp}})}" title="SE_{pool} = \sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}+\frac{1}{N_{exp}})}" /></a>


References:

https://classroom.udacity.com/courses/ud257

https://www.evanmiller.org/ab-testing/sample-size.html

https://exp-platform.com/hbr-the-surprising-power-of-online-experiments/

https://www.udacity.com/api/nodes/3954679115/supplemental_media/additional-techniquespdf/download
