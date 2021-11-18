
# AB Testing
AB Testing Notes from Udacity course https://classroom.udacity.com/courses/ud257

## Contents
- [1. Overview](#overview)
  - [1.1 Metric Choice](#metric-choice) 
  - [1.2 Distribution](#distribution) 
  - [1.3 Confidence Interval](#confidence-interval) 
  - [1.4 Hypothesis Testing](#hypothesis-testing) 
  - [1.5 Standard Error](#standard-error) 
  - [1.6 Size vs Power Trade off](#size-power) 
  - [1.7 Analyze Results](#analyze-results)
- [2. Choosing and Characterizing Metric](#lesson2)



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


```
phat = X / N (# users who clicked/ # users)

Lets say; X = 100 and N = 1000 
phat = 0.1

To use normal distribution check N * phat > 5 and N * (1-phat) > 5 

margin of error m = z * SE
m = z * sqrt( (phat * (1 - phat))/ N ) 
m = 1.96 * sqrt( (0.1 * 0.9) / 1000) 
m = 0.01859 
so confidence interval @95% is (phat - m, phat + m)
(0.1 - 0.019, 0.1 + 0.019) 
so we would see between 81 ~ 119 click
```
### 1.4 Hypothesis testing <a name="hypothesis-testing"></a>
We want to calculate what is the probability that the results are due to a chance <br>
H<sub>o</sub>: <i>P</i><sub>exp</sub> -  <i>P</i><sub>cont</sub> = 0 <br>
H<sub>A</sub>: <i>P</i><sub>exp</sub> -  <i>P</i><sub>cont</sub> ≠ 0

### 1.5 Standard Error   <a name="standard-error"></a>
 <a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;{\hat{P}&space;=&space;\frac{X_{cont}&plus;&space;X_{exp}}{N_{cont}&plus;&space;N_{exp}}}" title="{\hat{P} = \frac{X_{cont}+ X_{exp}}{N_{cont}+ N_{exp}}}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;SE_{pool}&space;=&space;\sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}&plus;\frac{1}{N_{exp}})}" target="_blank"><img style="background: white;" src="https://latex.codecogs.com/svg.latex?\bg_white&space;SE_{pool}&space;=&space;\sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}&plus;\frac{1}{N_{exp}})}" title="SE_{pool} = \sqrt{\hat{P_{pool}}*(1-\hat{P_{pool})}*(\frac{1}{N_{cont}}+\frac{1}{N_{exp}})}" /></a> </p>

<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;\hat{d}&space;=&space;\hat{p_{exp}}&space;-&space;\hat{p_{cont}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;\hat{d}&space;=&space;\hat{p_{exp}}&space;-&space;\hat{p_{cont}}" title="\hat{d} = \hat{p_{exp}} - \hat{p_{cont}}" /></a>


H<sub>0</sub>: d = 0 where d<sub>hat</sub> ~ N(0, SE<sub>pool</sub>) <br>
If d<sub>hat</sub>  > 1.96 * SE<sub>pool</sub> or  d<sub>hat</sub> < -1.96 * SE<sub>pool</sub>, reject null hypothesis


#### Practical or Substantive Significance
Practical significance is the level of change that you would expect to see from a business standpoint for the change to be valuable.

The differences in the magnitudes for what's consider practically significant can be quite different. What you really want to observe is repeatability.

Statistical significance is about repeatability. And you want to make sure when you setup your experiment that you get that guarantee that yes, these results are repeatable so it's statistically significant.

The statistical significance bar is often lower than the practical significance bar, so that if the outcome is practically significance, it is also statistically significant.

### Size vs Power trade off.  <a name="size-power"></a>
Given that we have control over how many page views go into our control and expirement group, we need to decide how many page views we need in order to get a statistical significance result, this is called <b>statistical power</b>. Key thing is if we see something interesting we want to have enough power to conclude with high probability that the interesting result is in fact statistically significant. <br>
Power has an inverse trade-off with size, the smaller the change you want to detect or increase confidence you want to have in the result means you have to run a larger experiment, that is more page views. <br>
α = P(reject null | null true) -- False positive<br>
β = P(fail to reject null | null false) -- False negative<br>

As sample size increases, distribution become tighter around the mean, bring confidence interval closer.

|α /β |Small Sample|Large Sample|
|:---:|:---:|:---:|
|α | α is low, unlikely to launch bad experiment | α remains the same|
|β| β is high, more probably to not lauch an exp that made a difference| β is lower|

Online sample size calculator
https://www.evanmiller.org/ab-testing/sample-size.html


#### As you change one of the parameters, your sample size will change as well.

1. Higher click-through-probability in control but still less than 0.5 -> standard error increases -> more samples required. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;SE&space;=&space;\sqrt{\frac{p*(1-p)}{N}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;SE&space;=&space;\sqrt{\frac{p*(1-p)}{N}}" title="SE = \sqrt{\frac{p*(1-p)}{N}}" /></a>                   

<i>SE = √0.5 * 0.5 = 0.5  <br>
SE = √0.1 * 0.9 = 0.3 <br></i>
as <i>p</i> gets closer to 0.5 <i>SE</i> increases

2. As practical significance level (𝑑𝑚𝑖𝑛) increases, fewer samples are required since large changes are easier to detect
3. With increase in confidence level (1−𝛼), you want to be more certain that you are rejecting the null. At the same sensivitiy, this would require increasing the number of samples
4. If you want to increase the sensitivity (1−𝛽), you need to collect more samples


### Analyze results  <a name="analyze-results"></a>

N<sub>cont</sub> = 10072  ;Control samples (pageviews) <br>
N<sub>exp</sub> = 9886  ;Test samples (pageviews) <br>
X<sub>cont</sub> = 974  ;Control clicks <br>
X<sub>exp</sub> = 1242  ;Exp. clicks <br>

p<sub>pool</sub> = (X<sub>cont</sub> + X<sub>exp</sub>)/(N<sub>cont</sub>+N<sub>exp</sub>) <br>
SE<sub>pool</sub> = sqrt(p<sub>pool</sub> * (1-p<sub>pool</sub>) * (1/N<sub>cont</sub>+ 1/N<sub>exp</sub>)) <br>

p<sub>cont</sub> = X<sub>cont</sub>/N<sub>cont</sub> <br>
p<sub>exp</sub> = X<sub>exp</sub>/N<sub>exp</sub> <br>
d<sub>hat</sub> = p<sub>exp</sub> - p<sub>cont</sub> <br>
d<sub>hat</sub> = 0.02892847 <br>

m = 1.96*SE<sub>pool</sub> <br>
cf<sub>min</sub> = d<sub>hat</sub>-m <br>
cf<sub>max</sub> = d<sub>hat</sub>+m <br>
d<sub>min</sub> = 0.02 ; Minimum practical significance value for difference <br>
cf<sub>min</sub> = 0.0202105 <br>
cf<sub>max</sub> = 0.03764645 <br>

Since the minimum confidence limit is greater than 0 and the practical significance level of 0.02, we conclude that it is highly probable that click through probability is higher than 0.02 and is significant. Based on this, one would launch the new version.


## 2. Choosing and Characterizing Metric <a name="lesson2"></a>
Define Metric
Build Intution
Characterize

<b>Define</b>
* <b>Invariate metric:</b> Metrics that shouldn’t change between your test and control, used as a <b>sanity check</b>
  * Do you have the same number of users across the two?
  * Is the distribution the same?

* <b>Evaluation metric:</b>  
  * High level business metrics; how much revenue you make, what your market share is, how many users you have
  * Detailed metrics: user experience with the product

High level concept of metric, active users, ctp; more granular details, for eg. one time active user, new active uses, auto assigned active.
You can pick 1 metric or entire suite of metric.

OEC Overal Evaluation Criterion, weighted function the combines all different metrics.
Issues with OEC
a. Deciding on a definition, hard to define
b. If over-optimize on 1 thing and not take into consideration other
c. If metric not moving, you need to break the composite metric back to individual components



References:

https://classroom.udacity.com/courses/ud257

https://www.evanmiller.org/ab-testing/sample-size.html

https://exp-platform.com/hbr-the-surprising-power-of-online-experiments/

https://www.udacity.com/api/nodes/3954679115/supplemental_media/additional-techniquespdf/download
