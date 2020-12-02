---
title: AI-Powered COVID Screening
published: true
---
The healthcare industry has seen a number of innovations which center on using maching learning on audio recordings to triage or diagnose a condition or disease.

My first exposure to this field was [Winterlight Labs](https://winterlightlabs.com/), who developed technology that uses voice recordings to diagnose Alzheimer's. Similar efforts by other organizations have assessed [loneliness, psychosis, PTSD, and depression](https://newatlas.com/health-wellbeing/ai-loneliness-natural-speech-language/).

Recently, news broke of maching learning being used to identify COVID-19 in a subject simply by listening to their cough.
<!--excerpt-->

I first read about this on [Gizmodo](https://gizmodo.com/this-ai-can-tell-if-you-have-covid-19-just-by-listening-1845540851), where they stated that the algorithm was "ridiculously accurate":

> The difference between a healthy person’s cough and the cough of someone infected with the virus is so slight that it’s imperceptible to the human ear. So the team developed an AI to detect these minute differences using tens of thousands of recorded samples of coughs and spoken words. And it’s been ridiculously accurate in early tests, recognizing 98.5% of coughs from people with confirmed covid-19 cases, and 100% of coughs from asymptomatic people.

It also explains in rather plain terms how the model works--it's an ensemble of neural networks:

> One neural network gauges sounds associated with vocal cord strength, while another detects cues related to a person’s emotional state, such as frustration, which can produce a “flat affect.” A third network listens for subtle changes in lung and respiratory performance. The team then combined all three models and overlaid them with an algorithm to detect muscular degradation.

Very cool. 

If it works, this test could triage whether a person is likely to have COVID... almost instantly, at little-to-no cost, without a trip to a testing site. This could have a huge impact in changing the course of the pandemic. 

But the question is whether the algorithm performs as well as the 98.% statistic might lead one to believe. Going back to the two statistics that Gizmodo reported:

*   It recognized 98.5% of coughs from people with confirmed COVID-19
*   It recognized 100% of coughs from asymptomatic people--note that this 100% of people with COVID-19 who were asymptomatic

Digging deeper into the [published paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9208795):

> As shown on the ROC curve, the model discriminates officially tested COVID-19 subjects 97.1% accurately with 98.5% sensitivity and 94.2% specificity, with a 100% asymptomatic detection rate and 88% accuracy on all subjects.

The ROC curve is the Reciever Operating Characteristic curve, which is used to measure the ability of a model to choose between two potential outcomes. In this case, either "Has COVID-19" or "Does not have COVID-19". The curve does this by plotting the true positive rate against the false positive rate.

The true positive rate is also known as sensitivity. In this case, the true positive rate measures how often the model flags people with COVID as having COVID. The false positive rate is the rate at which the model would incorrectly state that a person free of COVID has COVID. If you subtract this rate from 1, you get specificity. Specificity is the true negative rate, or how often the model correctly states that someone with COVID doesn't have COVID.

So parsing the statement above:

*   The model was able to identify as having COVID 98.5% of the people who actually had COVID: 1.5% of the people with COVID would be missed
*   The model was able to identify as not having COVID 94.2% of the people who didn't have COVID--this means that 5.8% of people who did not have COVID would be flagged as having COVID

Now, this does sound pretty impressive--and it is. But we need to consider the implications of this number:

*   A true positive rate of 98.5% means that 1.5% of the people with COVID would be missed
*   A false positive rate of 94.2% means that 5.8% of the people without COVID would be flagged as having COVID

Lets put this into the context of the current pandemic. 

First, we need an estimate of the true prevalence of COVID-19 in a populatio. This is either hard to find, or my Google skills are not as good as I thought. 

I found information on [predicted active cases in California](https://www.cpp.edu/~clange/covid19/Covid19ReportCaliforniaIntAct.html), but this depends on confirmed cases. Estimates of people who are asymptomatic, and therefore might not be tested, range from [20%](https://www.healthline.com/health-news/20-percent-of-people-with-covid-19-are-asymptomatic-but-can-spread-the-disease) to [45%](https://www.acpjournals.org/doi/10.7326/M20-3012). And even those people who are symptomatic might not be tested. So to make things simple, I'll use 1% as the current COVID infection rate. 

Let's assume we randomly test 100,000 people:

*   1,000 people would have COVID-19 (1% of 100,000)
*   985 people would be flagged as having COVID by this test that actully had it (100,000 x 0.01 x 0.985)
*   15 people with COVID would not be detected by this test (100,000 x 0.01 x 0.015)
*   5,742 people would be flagged as having COVID that do not have it (100,000 x 0.99 x 0.058)


![A visual representation of false positives](https://basilhayek.b-cdn.net/01_ai_powered_covid_screening/false_positive_1.png) 

In summary, for every 1 person correctly identified as having COVID, approximately six more would be flagged that don't actually have COVID. Is this a bad thing? I don't know. 

While I don't think everyone should be coughing into their phone to see if they might have COVID-19, it seems the test could be a helpful tool as part of the initial triage done with an HCP. Combined with the HCP's assessment of an individual risk, it could be a way to manage the strain on testing infrastructure, while also ensuring that those who might have it make their way for a test.

I'm excited about the possibility.

