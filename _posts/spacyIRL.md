---
title: 'SpaCy IRL 2019 - Wikidata-based NER in v3.0'
date: 2019-07-12
permalink: /posts/2019/07/12/post/
tags:
  - spacyirl
  - nlp
  - berlin
---

![](https://d33wubrfki0l68.cloudfront.net/ea71ef11a36bd7a2188096727d3103225726caa3/277f0/static/logo-105101938b9bc43bbb9d3d13ea3bc630.svg)

On July, 6th in Berlin I attended [spaCy IRL](https://irl.spacy.io/2019) - a conference organized by [explosion.ai](https://explosion.ai/) and [spacy](https://spacy.io/) which you probably know as one of the most popular, powerful and fast NLP libraries. Here is a short overview of the event.

We use spaCy in our daily work as well, so we couldn't miss the chance to meet the community and exchange research ideas as well as thoughts and expectations on the future of spaCy. 
Keynotes were not only covering applications of spaCy in research and industry but also more broad and diverse topics.
There exist already great highlights (like [this](https://www.linkedin.com/pulse/spacyirl-2019-conference-overview-ivan-bilan/) and [that](https://medium.com/@arnelapnin/highlights-from-spacy-irl-802229333785)), so in this post I'd like to go more into details of particular talks.


### Wikidata-based NER to appear in spaCy 3.0
![](https://irl.spacy.io/static/IMG_6246-21dfa3fa389e10392f3c70425d80055b.jpg)

Sofie Van Landeghem delivered a great talk (here are the [slides](https://tinyurl.com/entity-linking-spacy)) on the upcoming changes in the Named Entity Recognition (NER) module in the next major spaCy version.

In the current version, basic NER is fixed to a predefined set of entity types which you can manually extend. 
Nevertheless, the prediction quality even in larger models was not perfect so community wanted to have something more robust and customizable for domain-specific tasks.

Uniquely identified named entities? And with synonyms? And formally described? Sounds like a **knowledge graph**, right? For instance, Wikidata? :wink:

SpaCy think the same! So they took the latest version of Wikidata, sliced it from 50M entities to 1M based on the amount of incoming edges (interwiki links) retaining about 1.5M aliases, i.e., synonyms of named entities.
The training process is as follows:

![](/images/spacyirl/spacy3_ner1.png)  

Wikitext with named entities mentions is passed through a context encoder to obtain a 128D vector, 16 supported entity types comprise a 16D vector, then from the extracted Wikidata they encode entity description into a 64D vector, and finally concatenate the vectors together with the 1D prior probability vector. 
And the classifier is trained to maximize the probability of a Wikidata entity ID, entity type for a given piece of text. What is the accuracy of this approach?

![](/images/spacyirl/spacy3_ner3.png)

Well, it achieves decent 80% with 200K mentions on 1.1M entites - a nice initial result, and the trained model is just about 350MB.
What is even more fascinating - you don't need huge amounts of text to train a NER component as the following slide shows:

![](/images/spacyirl/spacy3_ner2.png)  

It's actually fine to have just 6-10K of mentions to achieve almost peak quality!
Alright, let me repeat it in simpler words: the approach allows to plug in your own knowledge graph with domain-specific entities and train a NER system with relatively small amounts of data, that's awesome :heart_eyes: And the following talk gave an application example in the biomedical domain.

### scispaCy
![](https://irl.spacy.io/static/IMG_6291-1cf735a9499277d5e41f48b44a436725.jpg)

Mark Neumann from Allen AI presented [scispaCy](https://allenai.github.io/scispacy/), a spaCy-based package for processing biomedial, clinical or scientific texts ([slides](https://docs.google.com/presentation/d/1CEc3pTMLX-XV1zgirydhURZdcNlgB2l4TXQv6mxLhy8/edit#slide=id.p)).
Open domain general purpose NER systems have little coverage of biomedical entities. 
They can probably identify DNA as a named entity, but struggle to link something as complex as "17beta-estradiol".
So the team took two major steps:
* trained a NER system on UMLS, the largest biomedical vocabulary
* employed small amount of rules to identify abbreviations, e.g., phosphatidylinositol-3-kinase (PI3K)

Given just that, they already achieve quite impressive results:

![](/images/spacyirl/spacy3_ner4.png)  

Well, it you were looking how to adapt NER systems to your domain, say, finance, law, or hydrodynamics, looks like we have a working solution now - take (or build) a rich knowledge graph of your domain (and KGs are inherently cool, too), get some decent volumes of training data (come on, 6-10K is not a leviathan after all), put them into spaCy v3.0 and you're done :sunglasses:

### Conclusions

Video recordings are now available as [a playlist on YouTube](https://www.youtube.com/playlist?list=PLBmcuObd5An4UC6jvK_-eSl6jCvP1gwXc) and I encourage you to check out all of them - thanks to the speakers for informative but not-rocket-science-complex talks!
More photos are available in the gallery on the [official website](https://irl.spacy.io/2019/#photos), credit goes to [Ema Discordant](https://www.instagram.com/ema_discordant/).
Thanks spaCy for bringing together the audience from so many fields with diverse backgrounds, e.g., I was not the only KG guy in the room :)

See you next time!

![](https://irl.spacy.io/static/IMG_6112-78cf6b86f2d22b8e7e59b44a82cd988f.jpg)






