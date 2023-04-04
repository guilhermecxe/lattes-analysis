# Predicting article major field by its title

On this project I tried to use Natural Language Processing (NLP) methods and Machine Learning (ML) to predict, based on an article title, which major field a researcher who wrote it belongs.

I understand that an article can be written by researchers from different areas. But I try to abstract this by keeping duplicate occurrences of article titles in the training and test data. Also, I want the ML model understands that certain articles can be written by researchers from different fields.

The correct order of the `jupyter notebook`'s is:
1. `data-collection.ipynb`
2. `analysis-and-cleaning.ipynb`
3. `training-on-all-articles.ipynb`
4. `training-on-balanced-articles.ipynb`

## Simplified summary:

At start, I used my package called `html_lattes_parser` to read 2000 doctors' resumes from the Plataforma Lattes in html format (this data is not available in this repository). Then I built a `pandas` `DataFrame` with four columns:

    - researcher_name
    - researcher_lattes_id
    - researcher_major_field
    - article_title

where each row represents and article.

The major fields considered were the eight main ones from the platform:
- Ciências Agrárias
- Ciências Biológicas
- Ciências da Saúde
- Ciências Exatas e da Terra
- Ciências Humanas
- Ciências Sociais Aplicadas
- Engenharias
- Lingüística, Letras e Artes

My goal was: for a sample of `article_title` to predict the `major_field` of the researcher who wrote (or helped to write) the article.

After data collection, I removed some rows that I thought were meaningless for the purpose of this projext, such as rows containing articles with less than 3 words. After that, we ended up with 14547 articles not equally distributed by major field. The field with the most articles was *Ciências da Saúde* with 2539 articles and the one with least was *Ciências Exatas e da Terra* with 1164.

In the next `jupyter notebook`, I trained a Logistic Regression model on 13810 articles to predict the probability of a given article belonging to each of the 8 fields. Evaluating it, we got an accuracy of 76% in guessing the right researcher's major field in the test set (727 articles).

In the notebook there is the accuracy broken down by field.

So I thought "what If the articles were equally distributed by major field?". To answear that, I started the `training-on-balanced-articles` notebook. Using 1164 articles from each field (9312 in all) we obtained an accuracy of 73%.

The model with balanced data had a lower accuracy, but that could be due to the decrease in the amount of data.

Future attempts to increase the accuracy may include:
- Training a model with a balanced number of articles but with 13810 articles in total to check if the accuracy goes above 76%.
- Think about whether there is a better way to fit the Logistic Regression model.
- Try other models like Random Forest, K-Neighbors or Neural Networks.

And futures projects could be:
- Predict researcher major field based on all their articles at once.