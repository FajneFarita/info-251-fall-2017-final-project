# Looking for a Needle in a Haystack: Predicting Wikipedia Edits
#### Natalia Timakova, Nathaniel Weinman, Ugur Yildirim


Wikipedia is updated more than 300 thousand times per day and it's not clear sometimes whether you are seeing "a work in progress" or it's a mature article. 

If it was possible to predict which articles were likely to be edited soon, Wikipedia could track the lifetime of an article and notify readers that there may soon be new information.

We've used two data sources: the MediaWiki database that provides metadata about Wikipedia articles (e.g. revision histories) and the Page View Statistics for Wikimedia Projects which is hourly data dump of view counts. Combining these data sources allowed us to generate features based on article name, size, views, edits, and minor edits over a 30-day historic period from the Main and Talk namespaces. However, due to the limitations of Wikimedia’s Quarry interface, we were unable to include additional metadata for unedited articles.

Preliminary analysis of our data shows that ~1/1000 articles viewed on a given day are edited. To balance the train set, we downsampled the majority class and ended up with 82,461 observations. To read about our feature engineering work, refer to the write-up.

Sinse the data wasn't linerly separable, linear models couldn't perform well. Out of the tree-based models, the best performance was expected from the boosted trees because of the high variance. In fact, decision trees performed slightly worse than random forest, which performed slightly worse than gradient boosting. The latter became our primary model.

For the preformance metrics and model outcomes, refer to the whitepaper.

Among the interestin discoveries of this work, we've learned that total views and current size of an article were the most significant features, while data on the talk namespace was not very valuable. Additionally, directional trends (either in absolute difference or relative ratio) were not very valuable, indicating that much of the necessary data is in the current state and very recent past.
