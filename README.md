Stats19 quality assessment
================

The data
--------

We're looking at Stats19 data, police records of road-traffic collisions (RTCs) that occur on roads in the UK. Of the many variables recorded in this dataset, we consider the following:

-   years 2005 to 2017
-   78 local authorities (LAs), which belong to one of nine city regions in England
-   collisions that involve at least two parties
-   collisions in which at least one person was slightly, seriously, or fatally injured.

The question
------------

Specifically, we're looking at the recorded age and gender information of people involved in an RTC in which at least one other person was injured. (This person may or may not have been injured themselves.) We use these data to try to address the following questions:

-   can we assess the quality of the Stats19 dataset?
-   does the quality differ between different city regions?

Descriptive
-----------

Here is the distribution of ages for those people, for the nine city regions:

![](README_files/figure-markdown_github/plot%20ages-1.png)

London has the most events (as it's the biggest city), followed by Leeds, the West Midlands, and Greater Manchester, followed by Sheffield, Liverpool, the North East, Nottingham and Bristol.

There are some spikes in the data, most noticeable for Greater Manchester at age 30, where the spike exceeds the count for London. The spikes are present for some cities but not all, and are most prominent at ages that are multiples of ten, followed by ages that are multiples of 5.

Quantifying quality
-------------------

In an attempt to quantify the spikiness, we normalise each city's trajectory, and take the sum of the absolute differences from point to point. These are the statistics for the city regions:

![](README_files/figure-markdown_github/plot%20city%20variability-1.png)

As expected, Greater Manchester has the most spikiness, followed by Bristol, then Liverpool, then the other six, which are similar to each other.

We can calculate the same statistic for each LA:

![](README_files/figure-markdown_github/plot%20la%20variability-1.png)

which shows a systematic difference between LAs in terms of how spiky the age trajectories are.

Correlates: missing information, and gender
-------------------------------------------

Most ages are recorded as a number between 0 and 103. Some ages are recorded as 'NA', meaning no value was given. Assuming that no value was given in cases where the age was unknown, we speculate that city regions with spikier trajectories have fewer cases of unknown age, as the spike in values at age 30 might reflect a combination of cases where the age was actually 30, and cases where the age was unknown and 30 was guessed. We define 'completeness' as the fraction of values that are not NA, and its counterpart (1-completeness) as missingness.

![](README_files/figure-markdown_github/plot%20age%20completeness-1.png)

There is some correlation and, again, there is some consistency between the LAs within a city region, with the Greater Manchester LAs having the highest spikiness and the highest rate of age entry completeness. London occupies the other end of the spectrum, with some of the lowest-variability LAs and the lowest rates of age completion. Liverpool and Bristol LAs lie between London and Greater Manchester, while Leeds, Sheffield and the North East have low age variability but higher completion, suggesting perhaps a systematic difference in recording. There is a distinct gap in the bottom-right corner, in that no LAs have high variability and low completion rate in age, as we might expect.

Another item of information recorded in Stats19 is gender. We might expect completeness of gender to correlate with that of age. However, we can't spot patterns like spikiness, as there are only three categories available: male, female, and NA.

![](README_files/figure-markdown_github/plot%20gender%20completeness-1.png)

As expected, there is some correlation between gender completeness and age completeness and, again, a separation is suggested between city regions who follow a similar gradient but with a different intercept. West Midlands and London seem to be on the same line, with Liverpool a step up, and the others following a similar pattern with a higher base level of age completeness.

Finally, plotting gender completeness against age variability highlights an outlier, the City of Bristol, which has high age variability but low gender completion, and is far from the other three LAs from its city region.

![](README_files/figure-markdown_github/plot%20var%20and%20gender%20completeness-1.png)

The outlier
-----------

It's not clear what is different about the City of Bristol. There is nothing that stands out about its other covariates.

The Bristol city region as a whole is distinct from the other city regions in the ratio of age missingness to gender missingness to overall missingness (both). All other city regions have lowest age completion, higher gender completion, and similar completion of 'both' to 'gender'. It fits with intuition that it's possible to know, or guess, gender and not age, and unlikely to know, or guess, age and not gender. Greater Manchester differs slightly, in that there is less overlap in missingness between age and gender. (So there are many cases where age is known and gender isn't, but more vice versa.)

Bristol city region, on the other hand, has similar levels for age and gender missingness, which both exceed combined missingness. This suggests there are similar numbers of cases where age is known and gender unknown, and age unknown and gender known.

![](README_files/figure-markdown_github/plot%20city%20completeness-1.png)

This pattern is seen in all the LAs that make up that city region. Likewise, the pattern for Greater Manchester is evident in all its LAs.

![](README_files/figure-markdown_github/plot%20la%20completeness-1.png)

In conclusion?
--------------

There are some curiosities in RTC recording by different city regions, and we don't know why.
