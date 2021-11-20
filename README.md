
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
  - [2.1 Define](#chap2define)


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


### Analyze Results  <a name="analyze-results"></a>

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

### 2.1 Define  <a name="chap2define"></a>
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

#### Gathering Additional Data
* User Experience Research (UER)
  + High depth but on few users
  + Good for brainstorming
  + Can use special equipment
  - Want to validate results
* Focus Groups
  + Medium depth on medium number of participants
  + Get feedback on hypotheticals
  - Run the risk of group think
* Surveys
  + Low depth but high number of participants
  + Useful for metrics you cannot directly measure
  - Can not directly compare with other metrics as population differs, depends on how questions are framed and users might not necessarily tell the truth

#### Metrics Definition and Data Capture
Click-through-probability = total clicks/ total page views <br>
nuanced version: cookie clicked/cookie visited site <br>

Turning high level metric into more defined metric <br>
High-level metric: CTP = #users who click/ #users who visit <br>
```
* Def #1; For each <time interval> = #cookies that click/ #cookies 
* Def #2: #pageviews with click within <time interval>/ #pageviews 
* Def /#3: /#clicks/ #pageviews (click-through-rate)
```

#### Filtering and Segmenting
External reasons: We want to filter on site, abuse or fraud and not want to use that in metric. <br>
What happens if the change affects only a segment of traffic (eg. int vs regional; mobile app vs web app), because you don't want to dilute the results and you can increase the power and sensitivity of the experimenting

Goal of filtering is, to de-bias the data but you want to careful you dont introduce bias when filtering the data. While filtering you need to make sure it is not part of the experiment or logging causing the long/ weird sessions which are being filtered.

##### How to decide a metric to use or not.
* Building baseline.
* Compute metric by different slices of disjoint sets (eg. region, demographic, platform) and want to make sure the metric does not affect any slice disproportionally, if it is then it might be a good thing if it is one slice where all your spam is coming from.
* Week over Week or day-over-day or a single user data can be a good filter to filter out spam. 

<b>Idea is to built a good intution to what changes are expected vs not expected so when you have data from the experiment you can make a call whether if there is problem or metrics are believable </b>

#### Summary Metrics
Per event measurement to one summary metric to combine all the different metrics

* Sums and Counts - eg. #users who visited page
* Means, medians and percentiles - eg. mean age of users who completed a course or mediam latency of page load
* Probabilities and Rates - Probability has 0 or 1 outcome in each case; Rate has 0 or more
* Ratios - eg. P(revenue-generating click)/ P(any click)

##### Characteristics of Metric:
* <b>Sensitivity and Robustness:</b> You want your metric to be sensitive enough that it picks up changes you care about but robust against changes you don't care about.
* <b>Distribution:</b> The most ideal way of doing this is to do a retrospective analysis to compute a histogram.

Sensitivity and Robustness

Latency experiment example.
Mean or median or neither
* Mean is senstiive to outliers.
* Median is roboust to outliers, but if you only affect fraction of users then median might not move at all you might want to use 90th or 99th percentile
* A/A experiment to see if metric where you dont change anything, and pick up metric is not picking up any supurious changes
* Retrospective analysis of logs you can check previous experiments and see of metrics move at all.

##### Absolute or Relative Difference

### Variablity
Affects sizing of experiment and analyzing confidence interval and draw conclusions of the expirement

#### Analytical vs Empirical
<>Analytical</b>
If doing count or probability then you're dealing with variablility of single measurement or constrained in case of probability <br>
Click-through-probability whether the user clicked or not and summary metric was overall click-through-probability we were able to do analytical or theoritical variance we expected from our overall probability
Other types of metric same thing works eg. normally distributed data.
<>Empirical</b>
Ratios, 90th percentile or lumpy distribution data then you want to compute empirical variability


|Type of Metric|Distribution|Estimated Variance|
|:---:|:---:|:---:|
|Probability|Binomial (normal)|<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;{\frac{\hat{p}*(1-\hat{p})}{N}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;{\frac{\hat{p}*(1-\hat{p})}{N}}" title="{\frac{\hat{p}*(1-\hat{p})}{N}}" /></a>|
|Mean|Normal| <a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;\frac{\hat{\sigma}&space;^{2}}{n}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;\frac{\hat{\sigma}&space;^{2}}{n}" title="\frac{\hat{\sigma} ^{2}}{n}" /></a>|
|Median/Percentile|Depends|Depends|
|Count/Difference|Normal|<i>Var(X) + Var(Y)</i>|
|Rates|Poisson|<a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;\hat{X}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;\hat{X}" title="\hat{X}" /></a> (mean)|
|Ratios <a href="https://www.codecogs.com/eqnedit.php?latex=\bg_white&space;(\frac{\hat{p}_{exp}}{\hat{p}_{cont}})" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\bg_white&space;(\frac{\hat{p}_{exp}}{\hat{p}_{cont}})" title="(\frac{\hat{p}_{exp}}{\hat{p}_{cont}})" /></a>|Depends|Depends|



Calculating Variability
Eg. To calculate a confidence interval you need:
* Variance (or standard deviation)
* Distribution

Knowledge of binomial distribution is used for SE formula and margin of error formula depends on the fact that binomial distribution approaches normal distribution as N gets larger
Binomial distribution:
SE = sqrt(p * (1-p)/N) 
width of standard error: m = z * SE

Non-parametric methods, can be measured without making assumptions of the distribution of data
* Sign test - Eg. If expirement ran for 20 days and if 15 of those days exp has higher measurement than control 
 + easy to do and can do under a lot of different circumstances
 - does not help estimate size of the effect




  

References:

https://classroom.udacity.com/courses/ud257

https://www.evanmiller.org/ab-testing/sample-size.html

https://exp-platform.com/hbr-the-surprising-power-of-online-experiments/

https://www.udacity.com/api/nodes/3954679115/supplemental_media/additional-techniquespdf/download
