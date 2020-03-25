---


---

<h1 id="otto-kaggle-challenge">Otto Kaggle Challenge</h1>
<p>Solution to the Otto challenge hosted on Kaggle. The final submission had a score of 0.39871 which placed 9th on the leaderboard.</p>
<h2 id="structure">Structure</h2>
<p>We used an ensemble of three layers.</p>
<ul>
<li><strong>Layer 1:</strong> 21 base learners</li>
<li><strong>Layer 2:</strong> 3 meta learners</li>
<li><strong>Layer 3:</strong> Non-linear combination of meta learners</li>
</ul>
<p>The predictions of Layer 1 were used as training features for the Layer 2 meta learners, stacked according to the Variant A detailed <a href="https://github.com/vecxoz/vecstack">here</a>.</p>
<h2 id="section"></h2>
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

