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
<h2 id="layer-1-models">Layer 1 Models</h2>
<pre class=" language-markdown"><code class="prism  language-markdown">| Model      | Data Transformation | Model               | Data Transformation |
|------------|---------------------|---------------------|---------------------|
| Deep NN    |                     | LGMB Dart           |                     |
| Deep NN    | log(X+1)            | LGMB GBDT           |                     |
| Deep NN    | Standard Scaled     | SKLearn MLP         |                     |
| Deep NN    | 0-1 Scaled          | Naïve Bayes         |                     |
| CatBoost   |                     | Naïve Bayes         | Standard Scaled     |
| ExtraTrees |                     | Random Forest       |                     |
| KNN        |                     | Softmax             |                     |
| KNN        |                     | XGBoost             |                     |
| KNN        |                     | Logistic Regression |                     |
| KNN        |                     | Logistic Regression | Standard Scaled     |
| KNN        |                     |                     |                     |
</code></pre>
<h2 id="layer-2-models">Layer 2 Models</h2>
<p>Three models used on the second layer:</p>
<ul>
<li>Deep Neural Net (pytorch)</li>
<li>XGBoost (XGB)</li>
<li>Calibrated Random Forest (SKLearn)</li>
</ul>
<h2 id="layer-3">Layer 3</h2>
<p>Non-linear combination of the three meta learners according to the below equation. Best results were obtained with <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>a</mi><mo>=</mo><mn>0.995</mn></mrow><annotation encoding="application/x-tex">a=0.995</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.43056em; vertical-align: 0em;"></span><span class="mord mathdefault">a</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 0.64444em; vertical-align: 0em;"></span><span class="mord">0</span><span class="mord">.</span><span class="mord">9</span><span class="mord">9</span><span class="mord">5</span></span></span></span></span>, <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>b</mi><mo>=</mo><mn>1</mn><mi mathvariant="normal">/</mi><mn>3</mn></mrow><annotation encoding="application/x-tex">b=1/3</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.69444em; vertical-align: 0em;"></span><span class="mord mathdefault">b</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">1</span><span class="mord">/</span><span class="mord">3</span></span></span></span></span>, <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>c</mi><mo>=</mo><mn>2</mn><mi mathvariant="normal">/</mi><mn>3</mn></mrow><annotation encoding="application/x-tex">c=2/3</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.43056em; vertical-align: 0em;"></span><span class="mord mathdefault">c</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">2</span><span class="mord">/</span><span class="mord">3</span></span></span></span></span>, <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>d</mi><mo>=</mo><mn>0.05</mn></mrow><annotation encoding="application/x-tex">d=0.05</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.69444em; vertical-align: 0em;"></span><span class="mord mathdefault">d</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 0.64444em; vertical-align: 0em;"></span><span class="mord">0</span><span class="mord">.</span><span class="mord">0</span><span class="mord">5</span></span></span></span></span></p>
<p><span class="katex--display"><span class="katex-display"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>a</mi><mo>×</mo><mo stretchy="false">(</mo><mi>N</mi><msup><mi>N</mi><mi>b</mi></msup><mo>×</mo><mi>X</mi><mi>G</mi><msup><mi>B</mi><mi>c</mi></msup><mo stretchy="false">)</mo><mo>+</mo><mi>d</mi><mo>×</mo><mi>R</mi><mi>F</mi></mrow><annotation encoding="application/x-tex">a \times (NN^b \times XGB^c) + d\times RF</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.66666em; vertical-align: -0.08333em;"></span><span class="mord mathdefault">a</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">×</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1.14911em; vertical-align: -0.25em;"></span><span class="mopen">(</span><span class="mord mathdefault" style="margin-right: 0.10903em;">N</span><span class="mord"><span class="mord mathdefault" style="margin-right: 0.10903em;">N</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.899108em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathdefault mtight">b</span></span></span></span></span></span></span></span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">×</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathdefault" style="margin-right: 0.07847em;">X</span><span class="mord mathdefault">G</span><span class="mord"><span class="mord mathdefault" style="margin-right: 0.05017em;">B</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.714392em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathdefault mtight">c</span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.77777em; vertical-align: -0.08333em;"></span><span class="mord mathdefault">d</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">×</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.68333em; vertical-align: 0em;"></span><span class="mord mathdefault" style="margin-right: 0.00773em;">R</span><span class="mord mathdefault" style="margin-right: 0.13889em;">F</span></span></span></span></span></span></p>
<h2 id="files">Files</h2>
<p><a href="Otto.ipynb">Otto.ipynb</a><br>
Data preprocessing, base models, and XGB and RF meta learners.</p>
<p><a href="base-MLP.ipynb">base-MLP.ipynb</a><br>
Deep NN in pytorch, used for Layer 1 base models</p>
<p><a href="meta-MLP.ipynb">meta-MLP.ipynb</a><br>
Deep NN in pytorch, used as a Layer 2 meta learner</p>
<p><a href="dim_reduction_otto.ipynb">dim_reduction_otto.ipynb</a><br>
Dimensionality reduction analysis of the Otto dataset</p>

