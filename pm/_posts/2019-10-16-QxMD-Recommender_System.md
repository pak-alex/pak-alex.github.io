---
layout: post
title: Post Mortem - QxMD Recommender System
description: >
  Using trending news articles to recommend medical articles.
image: /assets/img/conversation.jpg
noindex: true
---

### Matching Trending News to Medical Articles

If you're interested in cats, you want to have cat videos in your video feed. If you're interested in fashion, you want to have posts about style on your social media feed. If you're interested in heart attacks, you want to have articles about the heart in your medical feed. In this Post Mortem, I aim to go in-depth about the problem QxMD faced, and how we built a personalized recommender system to increase user engagement. This project was done as the final capstone to my Master's Degree, where I worked with three other colleagues alongside QxMD's Data Science team.

From now on, 'news' articles refer to articles you'd find in your daily life, such as articles written by *CNN* or *CBC*. 'Medical' articles refer to articles in peer reviewed journals, such as the *New England Journal of Medicine* or *Nature*.

### Planning Ahead

The goal of this project was to re-engage QxMD's existing users by detecting trending topics in mainstream news, matching those topics to the relevant medical articles, then serving users personal article recommendations. Each of these tasks proved to be challenging problems to think on:

1. What counts as trending?

Even the first step of identifying trending articles required a lot of foresight. In many ways, this would be the stepping stone for the rest of the project. How do we identify what is trending? What does 'trending' really mean? How do we filter down news to healthcare related topics? Wait - how do we pull in news in the first place?

2. How do we match news articles to medical articles?

After considering the news article side of the project, we needed to consider the recommender system itself. The main problem we faced was coming up with a method to compare news articles and medical articles. It needed to accurately encapsulate the 'meaning' or 'topic' of an article, so that articles with similar topics would show up together and find which articles were most similar to each other. This ended up being the crux of our project.

3. What makes a user unique?

The final piece of the project came after matching news articles to medical articles, and that was to actually give the recommended medical article to a relevant user. There were several ways to categorize a user already using information they gave when they signed up for the platform (location or profession, for example). However, we wanted to create a system that would take all of those into account and more: what if we divided users by the articles they interacted with? What other features could we come up with?

These were all problems we considered before we even started coding. I can't lie, a part of me was intimidated by the prospect. Had we bitten off more than we could chew? But another part of me was excited. Looking at each of these issues individually and coming up with potential solutions as a team was fulfilling and *cool*. We were planning on using API's and spinning up clusters located who knows where to build a system hundreds of thousands of people would use.

### Main Takeaways

Unfortunately, I am not allowed to go into the specifics of how we tackled these problems. However, I will go into what I took away from the process.

1. Preprocessing is everything.

In classes and during toy projects, we constantly hear that preprocessing the data is everything. While I knew it was important and I theoretically understood why, I didn't 'believe' it. Well, consider me a devotee. Our initial runs with the bare minimum of preprocessing (stripping stopwords/punctuation, special characters, etc.) were producing less than stellar results. We were running around in circles until one of my colleagues suggested more creative ways of preprocessing the article text, further refining it such that only the true meaning of the article body was left. I couldn't believe the performance increase; our recommendations turned from tangentially related at best (and completely unrelated at worst) to producing recommendations that I thought a human would pick out.

2. Sometimes, the simplest solution is the best solution.

Near the beginning of the project, our team considered a variety of potential model designs to calculate a similarity score between news and medical articles. We decided on a somewhat fancier (and more complex) algorithm, but before implementing it, we built a simple placeholder system to test the pipeline. What we found was that the placeholder system was performing surprisingly well, considering the circumstances (and after the requisite preprocessing). This is not to say that the simple solution was the most high-performance solution we could have gone with. However, performance is not always the be-all-and-end-all of every project, which is hard to swallow when you've been working on something for a long time. After taking into account the time constraints and the opportunity cost elsewhere in the project, we decided to stick with what we had, which ended up improving the project as a whole.

3. Data science is cool.

Like I mentioned before, we were building a system that hundreds of thousands of people would use. This was not a Jupyter notebook that only I would look at, this was real, and it had to be treated like it. It was a cocktail of anxiousness and excitement and I am proud to say that our team was up to the task. Here's an example of one of our recommendations:

* CNN (News Article): CDC investigates after 4 patients got sepsis from contaminated platelet transfusions
* Transfusion (Journal Article): Do older platelets increase the risk of transfusion-associated sepsis?

I couldn't believe it. It was just a click of a button, but the payoff was immense. We were taking into account tens of millions of medical articles, distilling them down to key features, matching them to the daily news, and producing a list of users that we thought would be most interested in the medical article.

Our recommender system is currently being put into production at QxMD. The goal of our project was to increase user engagement with the QxMD app by serving users relevant journal articles recommendations, and our team laid the ground work. This project reaffirmed by suspicions: Data science is my passion. 
