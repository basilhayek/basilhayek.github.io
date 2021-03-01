---
title: covid-19-digital-surveillance
---
Last month I came across an [article in Nature](https://www.nature.com/articles/s41598-021-81333-1) assessing the use of social media as an early warning for COVID. Naturally, I was intrigued.

But as I read it, I couldn't help but think back to the Google Flu debacle. Google touted--in what was later labeled as "big data hubris"--it's ability to predict flu outbreaks simply by using it's vast amounts of search data. 

As we learned, [they couldn't](https://theconversation.com/googles-flu-fail-shows-the-problem-with-big-data-19363#:~:text=Flu%20Trends%20had%20already%20made,size%20of%20the%20initial%20outbreak.). 

There were numerous critiques of Google Flu Trends, with some of the key points being: 
* The inherent noise in any internet search signal: when only 8.8% of people who visited their health care provider with flu-like symptoms test positive, that means there's a lot more people searching for flu than have it
* The retrospective nature of the model: it's easy to "predict" the past
* Overfitting in the model: using a data-mining approach to create a retrospective model could lead to unrelated seasonal terms being interpreted as a signal for flu; one such example was searches for "high school basketball"

[A post-mortem](https://www.wired.com/2015/10/can-learn-epic-failure-google-flu-trends) of Google Flu Trends called out this overfitting:
> With millions of search terms being fit to the CDC’s data, there were bound to be searches that were strongly correlated by pure chance, and these terms were unlikely to be driven by actual flu cases or predictive of future trends.  

The last sentence made me think of the Bonferroni correction from statistics. When testing multiple hypotheses, the chance you'll find something of significance increases simply because you're testing multiple hypotheses. As [XKCD](https://xkcd.com/882/) illustrates, you will find a link between green jelly beans and acne if you test enough colors ([explanation](https://www.explainxkcd.com/wiki/index.php/882:_Significant)). 

The Bonferroni correction accounts for this by essentially raising the bar on what's consider significant. If you're testing 20 colors of jelly beans and want a significance level of 0.05 (e.g., 5% chance of coincidence) you would test each individual color at 0.0025 (0.05 / 20 = 0.0025).

This same principle generally applies to data mining. [KD Nuggets](https://www.kdnuggets.com/2016/07/big-data-bible-codes-bonferroni.html) gives a nice overview of the Bonferroni Principle in data mining. This article also discusses the closely related [Look-elsewhere Effect](https://en.wikipedia.org/wiki/Look-elsewhere_effect), which was responsible for the purported linkage of power lines to childhood leukemia.

Google's attempt's to predict flu based on data mining of search data failed to correct for the Bonferroni Principle. The approach taken by the authors of the Nature article was much different. They had a much more limited set of terms they were searching for. 

However, that presents its own challenge. Once a symptom is publicly linked to a condition, the keyword becomes extremely noisy as the [authors explain](https://www.nature.com/articles/s41598-021-81333-1):
> Since the detection and geo-localization of potential viral outbreaks are based on suitable keywords clearly linked to well-known symptoms, our approach cannot be directly used for the forecasting of otherwise unknown diseases. Indeed the usage of the word “pneumonia” on Twitter could have served as a useful proper predictor only before pneumonia was publicly linked to COVID-19, and not at a time when news outlets and the public in general were already discussing it widely. 

Effective digital surveillance of infectious disease requires integrating multiple data streams, not just Google searches or Twitter tweets. A [paper referenced](https://arxiv.org/pdf/2007.00756v1.pdf) in the Nature article calls out combining five signals that predicted spikes by several weeks: 
> Analysis of COVID-19-related activity on social network microblogs, Internet searches, point-of-care medical software, and a metapopulation mechanistic model, as well as fever
anomalies captured by smart thermometer networks, shows exponential growth roughly 2-3 weeks prior to comparable growth in confirmed COVID-19 cases and 3-4 weeks prior to comparable growth in COVID-19 deaths across the US over the last 6 months. 

Adding [anonymized location data](https://www.businessinsider.com/sturgis-rally-attendees-traveling-covid-phone-data-2020-8) could help predict areas that might be at risk for spikes due to people traveling from hot spots. [Voluntary active surveillance](https://outbreaksnearme.org/us/en-US/) could help calibrate other signals, although self-selection bias would need to be accounted for.

Bringing this all together represents a true big data problem: there's a large amount of data (volume), coming in real-time (velocity), in multiple different formats (variety), with bias, noise, and abnormalities (veracity).

I'm sure there are smart and ambitious teams that are taking this forward and developing the next generation of infection disease digital surveillance. Given the anticipation of COVID-19 becoming [endemic](https://www.nature.com/articles/d41586-021-00396-2) perhaps we'll be using it to predict seasonal patterns to help keep people safe.