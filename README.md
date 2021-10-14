# data-512-a2

## Goal:
The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries. For this assignment, we combine a dataset of Wikipedia articles with a dataset of country populations, and use a machine learning service called ORES to estimate the quality of each article.

We perform an analysis of how the coverage of politicians on Wikipedia and the quality of articles about politicians varies between countries. The analysis will consist of a series of tables that show:
- the countries with the greatest and least coverage of politicians on Wikipedia compared to their population.
- the countries with the highest and lowest proportion of high quality articles about politicians.
- a ranking of geographic regions by articles-per-person and proportion of high quality articles.

Folder Structure
```
├── data_clean
    ├── wp_wpds_countries-no_match.csv
    ├── wp_wpds_politicians_by_country.csv
├── data_raw
    ├── WPDS_2020_data.csv
    ├── page_data.csv
└── hcds-a2-bias.ipynb
```

## API Documentation/ Data Sources
- [Wikipedia Politician Data](https://figshare.com/articles/dataset/Untitled_Item/5513449)
- [Population Data](https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit)
- [ORES REST API] (https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model)

The ORES API outputs a categoriacl variable that is the prediction of a ML model of the quality of a wikipedia article
1) FA - Featured article
2) GA - Good article
3) B - B-class article
4) C - C-class article
5) Start - Start-class article
6) Stub - Stub-class article

## Output
| Column Name             | Description                                     |
|-------------------------|-------------------------------------------------|
| country                 | Country Name |
| article name            | Name of the politician that the article is about|
| revision_id             | unique ID for each article - key that is passed to the API |
| article_quality_est.    | Qualitative output of the ORES API |
| population              | Population of the country that the politician is from |

## Issues
- In some cases, when we passed the revision id to the API, the API did not return a quality estimate
- When we joined the population table with the wikipedia table, we joined it on the country, there were couple of rows that couldn't be merged
In both the aove cases, we discarded those rows and noted them down in a log

## Reflections
### What (potential) sources of bias did you discover in the course of your data processing and analysis?
I found it really interesting to see the data about the %of high quality articles in a region vis-a-vis the number of articles as a ratio of the population. Northern America had the highest ratio of high quality articles, however they're articles as a ratio of the population was one of the lowest. There are a number of possible factors that could explain this. 
1) I'd be interested to look into who contributes to these articles - is there bias in the authorship? There could be a language/cultural/access to technology reason for this
2) I'm also interested in the API that is estimating the quality of the article - what sources of bias went into the model training? 
3) Also, looking just at ratios can be misleading - It might be interesting to also look at raw numbers of the total articles and then use a threshold to filter out those that have very few/ try to understand reasons for why they have very few?

### What might your results suggest about the internet and global society in general?
Looking at the wikipedia results - it seems to suggest that high quality articles are heavily biased towards the western world. This seems to be a circular problem though as the media looks through the world through the lens of the west which in turn exemplifies the bias that already exists

### Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?
I think in any situation where we use these results as a proxy for the strength of a regions popularity/global reach would result in misleading interpretations due to the inherent bias of the data
