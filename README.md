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

Metrics:
1. Click through rate = Number of Clicks / Number of page vists
2. Click through probability = unique vistors who clicked / unique visitors to page
3. Distribution is binomial as 2 outcomes 

![\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}](https://latex.codecogs.com/svg.latex?x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D)



<b>Confidence Interval</b>
phat = X / N (# users who clicked/ # users)

Lets say; X = 100 and N = 1000 <br>
phat = 0.1

To use normal check N * phat > 5 and N * (1-phat) > 5

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
