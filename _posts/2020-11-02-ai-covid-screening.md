---
title: AI COVID Screening
published: false
---
The healthcare field has seen a lot of innovations in which machine learning is applied to audio recordings to triage or diagnose a condition or disease. A few years back, I learned of Winterlight, who is using voice recordings to diagnose Alzheimer's. What immediately comes to mind is the potential to monitor the progression of Alzhemier's through a smart speaker while at the same time giving them a companion who can assist them with day-to-day activities and bring them back to the moments and music of their earlier days. <Other examples> Of course now, in the midst of a pandemic, it's not unexpected that we learn of a machine learning algorithm that can identify COVID19 in a cough with stunning accuracy. The ability to quickly triage whether a person might have COVID, and do so without a trip to a testing site, and with a turnaround measured in seconds could have a huge impact in changing the course of the pandemic. But the question is whether the algorithm performs as well as it is supposed to. Gizmodo says this:

> The difference between a healthy person’s cough and the cough of someone infected with the virus is so slight that it’s imperceptible to the human ear. So the team developed an AI to detect these minute differences using tens of thousands of recorded samples of coughs and spoken words. And it’s been ridiculously accurate in early tests, recognizing 98.5% of coughs from people with confirmed covid-19 cases, and 100% of coughs from asymptomatic people.

It also explains in rather plain terms how the model works--it's an ensemble of neural networks:

> One neural network gauges sounds associated with vocal cord strength, while another detects cues related to a person’s emotional state, such as frustration, which can produce a “flat affect.” A third network listens for subtle changes in lung and respiratory performance. The team then combined all three models and overlaid them with an algorithm to detect muscular degradation.

But let's go back to those two statistics on accuracy:

*   It recognized 98.5% of coughs from people with confirmed COVID-19
*   It recognized 100% of coughs from asymptomatic people--note that this 100% of people with COVID-19 who were asymptomatic

Digging deeper into the published paper:

> As shown on the ROC curve, the model discriminates officially tested COVID-19 subjects 97.1% accurately with 98.5% sensitivity and 94.2% specificity, with a 100% asymptomatic detection rate and 88% accuracy on all subjects.

The ROC curve is the Reciever Operating Characteristic curve, which is used to measure the ability of a model to choose between two potential outcomes. In this case, either "Has COVID-19" or "Does not have COVID-19". The curve does this by plotting the true positive rate against the false positive rate. <AUC> The true positive rate is also known as sensitivity. In this case, the true positive rate measures how often the model flags people with COVID as having COVID. The false positive rate is the rate at which the model would incorrectly state that a person free of COVID has COVID. If you subtract this rate from 1, you get specificity. Specificity is the true negative rate, or how often the model correctly states that someone with COVID doesn't have COVID. <graphic?> So looking above:

*   The model was able to identify as having COVID 98.5% of the people who actually had COVID: 1.5% of the people with COVID would be missed
*   The model was able to identify as not having COVID 94.2% of the people who didn't have COVID--this means that 5.8% of people who did not have COVID would be flagged as having COVID

Now, this does sound pretty impressive--and it is. But we need to consider the implications of this number:

*   A true positive rate of 98.5% means that 1.5% of the people with COVID would be missed
*   A false positive rate of 94.2% means that 5.8% of the people without COVID would be flagged as having COVID

Lets put this into the context of the current pandemic. Estimates for the percent of people who have had COVID vary widely from 1% to 10%. This is for a measure of how many people have had COVID, not just those who actively have the disease. For argument sake, we'll use 1% as the current COVID infection rate. Let's assume we randomly test 100,000 people:

*   1,000 people would have COVID-19 (1% of 100,000)
*   985 people would be flagged as having COVID by this test that actully had it (100,000 x 0.01 x 0.985)
*   5,742 people would be flagged as having COVID that do not have it (100,000 x 0.99 x 0.058)
*   15 people with COVID would not be detected by this test (100,000 x 0.01 x 0.015)

![](https://digitalgraphiteblog.files.wordpress.com/2020/11/false_positive_1.png) So six times more people would be flagged as having COVID that do not have it, as composed to those flagged who do have it. Lets put this into real (but hypothetical) numbers. If all 6,727 people get a lab test, and that test has 100% accuracy, we would have a positive rate of 14.6%. This does assume that only people flagged by the model get at test, but this number is also significantly higher than the current 4% threshold set in many states. Without context, this number will be extremely alarming. Any mass adoption of a test like this will require coordinated efforts with state and local health authorities to ensure that people who are testing as the result of a referral are tracked, to avoid... The bottomline is that while this is an exciting innovation, and I look forward to more innovations in this front, it's imporant to consider what the numbers would mean in a real-world setting, and consider the implications of broadly adopting such a test.
