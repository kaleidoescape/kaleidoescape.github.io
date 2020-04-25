---
layout: post
title: "Term-Aware Machine Translation"
date: 2020-04-25
featured-image: term-aware-mt-lemma-demo.png 
featured-image-alt: Lemmatization and factors being used to prepare training data for a term-aware MT model.
---

Businesses requesting translations like to see consistency in the tone and terminology used. However, when many different translators work to translate documents for the business, it is difficult to ensure that translations remain consistent over time. While the use of NMT can improve translation speed for businesses, fixing inconsistent terminology represents a significant portion of the post-editing effort for translators. A robust NMT system should be able to incorporate term translations from human-curated term banks as guidance, to ensure more consistent translations from the start.

In this talk, that I made for a friend who runs a Belarus NLP meetup from [NLProc.by](https://nlproc.by/), I presented:
- How term banks are used in the typical translation industry workflow
- Challenges and methods for identifying terms from the term bank in the source sentence
- Methods for incorporating term guidance in the NMT system, agnostic to the specific term bank used at inference time


The slides are available [here]({{ site.baseurl }}{{ post.url }}/assets/pdfs/term-aware-mt-presentation.pdf), and the recording of the presentation can be viewed on YouTube:

<p align="center">
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/c3-Ma8TAXRw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

