# AB Testing
AB Testing Notes from Udacity course

Example Audacity learning website wants to test a change on Audacity page. <br>
<b>Experiment:</b> <br>
Hypothesis: Changing the "Start Now" button from orange to pink will increase how many students explore Audacity course
1. Metric: Click through rate
2. Distribution is binomial as 2 outcomes 

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
