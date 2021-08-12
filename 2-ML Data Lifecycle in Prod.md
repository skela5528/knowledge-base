<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2-ML Data Lifecycle in Prod</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li><a href="#course-2----machine-learning-data-lifecycle-in-production">Course 2 - # Machine Learning Data Lifecycle in Production</a>
<ul>
<li><a href="#week-1">Week 1</a>
<ul>
<li><a href="#itro">Itro</a></li>
<li><a href="#collecting-data">Collecting Data</a></li>
<li><a href="#labeling-data">Labeling Data</a></li>
<li><a href="#validating-data">Validating Data</a></li>
</ul>
</li>
<li><a href="#week-2">Week 2</a>
<ul>
<li><a href="#feature-engineering">Feature Engineering</a></li>
<li><a href="#feature-transformation-at-scale">Feature Transformation at Scale</a></li>
</ul>
</li>
<li><a href="#week-3">Week 3</a></li>
<li><a href="#week-4">Week 4</a></li>
</ul>
</li>
</ul>
</div></p>
<h1 id="course-2----machine-learning-data-lifecycle-in-production">Course 2 - # Machine Learning Data Lifecycle in Production</h1>
<h2 id="week-1">Week 1</h2>
<h3 id="itro">Itro</h3>
<blockquote>
<p>Data is the hardest part of ML and the most important piece to get right…<br>
Broken data is the most common cause of problems in production ML systems</p>
</blockquote>
<p><strong>Production ML = ML dev + SW dev</strong></p>
<p><img src="https://www.dropbox.com/s/stjcvjyxdsvs67x/c2_w1_1.png?raw=1" alt=""><br>
<strong>Difference ML modeling vs production ML:</strong><br>
<img src="https://www.dropbox.com/s/1yprtiqbfry5rqk/c2w1_2.png?raw=1" alt=""><br>
<strong>Modern SW:</strong></p>
<ul>
<li>scalability</li>
<li>extensibility</li>
<li>configuration</li>
<li>consistency and reproducibility</li>
<li>safety/ security</li>
<li>modularity</li>
<li>testability</li>
<li>monitoring</li>
</ul>
<p><strong>TensorFlow Extended (TFX)</strong><br>
End to end platform for deploying prod ML pipelines (open source)<br>
D=Data<br>
D ingestion -&gt; D validation -&gt; Feature Eng -&gt; Train Model -&gt; Validate Model -&gt; Serve Model</p>
<h3 id="collecting-data">Collecting Data</h3>
<p><strong>Key points</strong></p>
<ul>
<li>Understand users -&gt; translate user needs into data problems</li>
<li>Ensure data coverage and predictive signal</li>
<li>Store and monitor data quality</li>
</ul>
<p><strong>Use case</strong><br>
<strong>identify system specs</strong>: users/ users needs/ user actions/ ML system output/ ML system learning<br>
<strong>identify data specs</strong>: what kind of/ how much data is available/ how often does new data come in/ is it annotated/ how?<br>
<strong>translate user needs into data needs</strong>:</p>
<ul>
<li>data needed</li>
<li>features needed</li>
<li>labels needed</li>
</ul>
<p><strong>Get know your data !!!</strong></p>
<ul>
<li>data sources</li>
<li>if data sources are refreshed</li>
<li>consistency for values, units &amp; data types</li>
<li>monitor outliers and errors</li>
</ul>
<p><strong>Dataset issues</strong>: inconsistent formatting /compounding errors from other ML models</p>
<p><strong>Measure data effectiveness</strong>: feature predictive power/ feature eng/ feature selection</p>
<p><strong>Raters/Taggers:</strong> generalist (any people)/ subject matter expert/ users</p>
<h3 id="labeling-data">Labeling Data</h3>
<ul>
<li>mispredictions do not have uniform cost to your business</li>
<li>model objectives is probably a <strong>proxy</strong> for your business objectives</li>
<li>the real world is <strong>changing</strong></li>
</ul>
<p><strong>Data and Concept Change in Prod ML</strong></p>
<ul>
<li>data and scope changes</li>
<li>monitor models and validate data to find problems early</li>
<li>changing GT - label new training data</li>
</ul>
<p><strong>Model performance decays over time</strong>: (due to data and concept drift) can be slow (months, years) or fast (weeks - fashion, days, hours - stock exchange)<br>
<strong>Model retraining helps to improve the performance</strong></p>
<p><strong>Data labeling methods:</strong></p>
<ul>
<li>
<p><em>process feedback (direct labeling)</em> CTR rate, recommendation -&gt; buy or not - <strong>allow frequent retrain on a fresh data</strong>/ similar to reinforcement learning/ suitable for rare usecases</p>
</li>
<li>
<p><em>human labeling</em> : taggers road lanes</p>
</li>
<li>
<p>semi supervised labeling</p>
</li>
<li>
<p>active learning</p>
</li>
<li>
<p>weak supervision</p>
</li>
</ul>
<p><strong>tools for log analysis</strong></p>
<ul>
<li><a href="https://www.elastic.co/logstash/"><em>Logstash</em></a></li>
<li><a href="https://www.fluentd.org/"><em>Fluentd</em></a></li>
<li>cloud log analysis (google cloud logging/ Azure monitor)</li>
</ul>
<p><strong>Human labeling</strong><br>
raw data -&gt; ask people to label -&gt; labeled data</p>
<ul>
<li>need instructions</li>
<li>disagreements between taggers</li>
<li>advantage: good labels, common way</li>
<li>disadvantage: may be complected /expensive / slow, not possible to produce huge amount of data, if need experts</li>
</ul>
<h3 id="validating-data">Validating Data</h3>
<p><strong>Data Drift</strong> - change in data over time (e.g. data collected once a day)<br>
<strong>Data Skew</strong> - diff between two static versions, of diff sources e.g. training data vs production data (serving)<br>
<strong>Concpet Drif</strong> - change in target variable</p>
<p><strong>Data issues:</strong></p>
<ul>
<li>detecting schema skew: int-&gt; float, nan-&gt; Null, 2 categories -&gt; 3</li>
</ul>
<p><img src="https://www.dropbox.com/s/weakijwxu580w4g/c2w1_3.png?raw=1" alt=""><br>
<strong>Solution: continuously monitoring and evaluate the data</strong><br>
Compare training data stats vs Serving data and detect anomalies</p>
<p><strong>TensorFlow Data Validation (TFDV)</strong></p>
<ul>
<li>schema skew/ feature skew/ distribution skew</li>
<li>feature drift</li>
</ul>
<h2 id="week-2">Week 2</h2>
<h3 id="feature-engineering">Feature Engineering</h3>
<p><img src="https://www.dropbox.com/s/wah7svspckj78sx/c2w2_1.png?raw=1" alt=""><br>
<img src="https://www.dropbox.com/s/6vst19drtlrxvhn/c2w2_2.png?raw=1" alt=""><br>
<strong>MaxMinNorm</strong> = (X - X_min) / (X_max - X_min) - good if data distr is not Gaussian: [0, 1]<br>
<strong>Standartization (z-score)</strong> = (X - mean)/std, around 0: [-inf, +inf]<br>
<strong>Bucketizing/ Binning</strong><br>
<strong>Dimensionalty reduction</strong> PCA, t-SNE, UMAP<br>
Embedding projector.</p>
<p><strong>Feature crosses</strong> - combines multiple features into a new feature</p>
<h3 id="feature-transformation-at-scale">Feature Transformation at Scale</h3>
<p>consistent and reproducible pipeline</p>
<p>Preprocessing granularity:<br>
Instance level vs Full data pass: for clipping, scaling, bucketizing etc. need to pass all data<br>
<strong>At serving time we can do only instance-level</strong><br>
preprocessing training vs serving</p>
<p>transform per batch (use batch statistic only and not full dataset statistics)<br>
there is a differences btw batches, can be good or bad</p>
<h2 id="week-3">Week 3</h2>
<h2 id="week-4">Week 4</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

