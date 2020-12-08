---
title: "Worthwhile Practical ML in Production Papers"
date: 2020-11-24T18:34:42-06:00
draft: false
---

# Worthwhile Practical Papers
Interesting papers for folks engaged in building production ML systems primarily for user-facing use cases. This covers things like computational
advertising, click estimation, search ranking, bandit-based user experience optimization, recommender systems and other related things.

### Ad Click Prediction: a View from the Trenches [[link]](https://research.google/pubs/pub41159/)
A well-known paper from a large group a Google sharing details on Google's sponsored search system.
I like this paper because it naturally mixes lots of practical lessons about using ML in production 
with a notable theory contribution (FTRL). It's a bit dated now I suppose but definitely worth a read at 
least in part because it is also (to my knowledge) [D Sculley's](https://research.google.com/pubs/author38217.html)
opening salvo in his series of articles about using ML in production.

---

### Machine Learning: The High Interest Credit Card of Technical Debt [[link]](https://research.google/pubs/pub43146/)
Another excellent paper from Google (including D Sculley) with a very practical bent. 
This NIPS 2014 paper covers a few of the arguably most important ways in which you can shoot 
yourself in the foot putting machine learning in production.

---

### An efficient bandit algorithm for realtime multivariate optimization [[link]](https://www.kdd.org/kdd2017/papers/view/an-efficient-bandit-algorithm-for-realtime-multivariate-optimization)
KDD '17 paper from Amazon with a very impressive result in a production e-commerce system. If you've worked on these kinds of problems before the 21% improvement they claim is almost too good to be true. From a product perspective this paper is about laying out a small widget or portion of a page. Typically these kinds of things are handled solely by product managers who come up with few variations which are then tested in a standard controlled experiment. This is sub-optimal because you often can't test every possible combination and so intuition rules what ultimately gets tested.
> After only a single week of online optimization, we saw a 21% conversion increase compared to the median layout. Our technique is currently being deployed to optimize content across several locations at Amazon.com

---

### Amazon Search: The Joy of Ranking Products [[video]](https://www.youtube.com/watch?v=NLrhmn-EZ88)
A short but interesting read for anyone working on e-commerce product ranking. There is nothing particularly groundbreaking here but a few details stand out for practitioners: 
* They rank using lambdamart models trained in part on click feedback
* They randomly sample things never rendered as part of the negative class
* They train >100 models corresponding to (site, category) pairs (eg amazon_japan, electronics)
* Model complexity somewhat modest at ~200 trees per model
* Their target is a mixture of clicks, cart adds and purchases
* They use custom feature evaluation code written by Sorokina ([github:dariasor/TreeExtra](https://github.com/dariasor/TreeExtra))

---

### Field-aware Factorization Machines in a Real-world Online Advertising System [[link]](https://arxiv.org/abs/1701.04099)
Criteo team discusses challenges encountered when they tried to take a Kaggle-winning CTR estimation model (based on Field Aware Factorization Machines) into "real" production to replace a status quo logistic regression-based model. Unsurprisingly there were challenges. In particular, while offline evaluation results appeared better than the status quo, the FFM models took substantially longer to train. From there they go on to describe distributed training of FFMs.

---

### Practical Lessons from Predicting Clicks on Ads at Facebook [[link]](http://quinonero.net/Publications/predicting-clicks-facebook.pdf)
Facebook paper covering some similar ground to the Trenches paper listed above. Interesting details here on leaf indexes from decision trees as features in a linear classifier, per-coordinate learning rates and some nice infrastructure details about Facebooks "Online Data Joiner" where they join ad view information with a click/no_click target to allow for online learning.
> We treat each individual tree as a categorical feature that takes as value the index of the leaf an instance ends up falling in. We use 1- of-K coding of this type of features. 
