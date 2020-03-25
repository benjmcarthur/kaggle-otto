---


---

<h1 id="otto-kaggle-challenge">Otto Kaggle Challenge</h1>
<p>Solution to the Otto challenge hosted on Kaggle. The final submission had a score of 0.39871 which placed 9th on the leaderboard.</p>
<pre class=" language-markdown"><code class="prism  language-markdown">| Model      | Data Transformation | Model               | Data Transformation |
|------------|---------------------|---------------------|---------------------|
| Deep NN    |                     | LGMB Dart           |                     |
| Deep NN    | log(X+1)            | LGMB GBDT           |                     |
| Deep NN    | Standard Scaled     | MLP                 |                     |
| Deep NN    | 0-1 Scaled          | Naïve Bayes         |                     |
| CatBoost   |                     | Naïve Bayes         | Standard Scaled     |
| ExtraTrees |                     | Random Forest       |                     |
| KNN        |                     | Softmax             |                     |
| KNN        |                     | XGBoost             |                     |
| KNN        |                     | Logistic Regression |                     |
| KNN        |                     | Logistic Regression | Standard Scaled     |
| KNN        |                     |                     |                     |
</code></pre>

