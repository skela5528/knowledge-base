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
<li><a href="#tensorflow-transforms">TensorFlow Transforms</a></li>
<li><a href="#feature-selection">Feature Selection</a></li>
</ul>
</li>
<li><a href="#week-3">Week 3</a>
<ul>
<li><a href="#data-journey-and-data-storage">Data Journey and Data Storage</a></li>
<li><a href="#evolving-data">Evolving Data</a></li>
<li><a href="#feature-stores">Feature stores</a></li>
</ul>
</li>
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
<h3 id="tensorflow-transforms">TensorFlow Transforms</h3>
<p><img src="https://www.dropbox.com/s/7b54d4is6jnfzzg/c2w2_3.png?raw=1" alt=""><br>
<strong>Tensorflow Extended</strong>:<br>
<a href="https://blog.tensorflow.org/2020/09/brief-history-of-tensorflow-extended-tfx.html">https://blog.tensorflow.org/2020/09/brief-history-of-tensorflow-extended-tfx.html</a><br>
<a href="https://www.tensorflow.org/tfx/guide#tfx_libraries">https://www.tensorflow.org/tfx/guide#tfx_libraries</a><br>
TFX libraries include:</p>
<ul>
<li>
<p><a href="https://www.tensorflow.org/tfx/guide/tfdv"><strong>TensorFlow Data Validation (TFDV)</strong></a>  statistics, schema, anomalies</p>
</li>
<li>
<p><a href="https://www.tensorflow.org/tfx/guide/tft"><strong>TensorFlow Transform (TFT)</strong></a>  is a library for preprocessing data with TensorFlow.</p>
</li>
<li>
<p><a href="https://www.tensorflow.org/tfx/guide/train"><strong>TensorFlow</strong></a></p>
</li>
<li>
<p><a href="https://www.tensorflow.org/tutorials/keras/keras_tuner">KerasTuner</a>  is used for tuning hyperparameters</p>
</li>
<li>
<p><a href="https://www.tensorflow.org/tfx/guide/tfma"><strong>TensorFlow Model Analysis (TFMA)</strong></a>  is a library for evaluating TensorFlow models.</p>
</li>
<li>
<p><a href="https://github.com/tensorflow/metadata"><strong>TensorFlow Metadata (TFMD)</strong></a>  provides standard representations for metadata that are useful when training machine learning models with TensorFlow.</p>
</li>
<li>
<p><a href="https://www.tensorflow.org/tfx/guide/mlmd"><strong>ML Metadata (MLMD)</strong></a>  is a library for recording and retrieving metadata associated with ML developer and data scientist workflows.</p>
</li>
</ul>
<h3 id="feature-selection">Feature Selection</h3>
<p>Feature space<br>
Feature space <strong>coverage</strong>: the training data should “cover” the serving data:</p>
<ul>
<li>same numerical ranges</li>
<li>same classes</li>
<li>similar characteristics for images (object sizes, orientations etc.)</li>
<li>similar vocabulary for NLP</li>
</ul>
<p><strong>Ensure feature space coverage</strong></p>
<ul>
<li>seasonality, trend, drift</li>
<li>continuous monitoring -&gt; key for success</li>
</ul>
<p><strong>Feature Selection - FS</strong></p>
<ul>
<li>identify best f</li>
<li>remove f that don’t influence the outcome</li>
<li>reduce that size of feature space<br>
<strong>Why?</strong> -Reduce storage and IO, minimize training/inference costs<br>
<strong>Unsupervised FS</strong>: not consider correlation to Y, remove redundant features (highly correlated fs)<br>
<strong>Supervised FS</strong>:  Filter method, Wrapper Method, Embedded Methods<br>
<strong>Filter method</strong> - correlated features are usually redundant -&gt; remove them
<ul>
<li>Pearson correlation btw features and btw target</li>
<li>Start from all -&gt; select best subset based on some criteria (1. inter-feature correlation 2. model quality)</li>
<li>Spearman’s correlation -&gt; non parametric, check the <em>ranks</em> instead of the raw values</li>
<li>Mutual info</li>
<li>Chi square</li>
<li>Correlation matrix</li>
<li>sklearn</li>
</ul>
</li>
</ul>
<p><strong>Wrapper methods</strong></p>
<ul>
<li>Forward selection, start with 1 feature,  iteratively add best feature, repeat when improvement &lt; threshold</li>
<li>Backward elimination: start with all, literally remove feature [keep best model], …</li>
<li>Recursive features - <a href="https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.RFE.html">https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.RFE.html</a><br>
require a model which can rank features by importance</li>
</ul>
<p><strong>Embedded methods</strong></p>
<ul>
<li>L1/L2 reg</li>
<li>Feature importance (e.g in RandomForest)<br>
<em>Embedded methods</em> combine the best of both worlds, filter and wrapper methods. It more efficient than filter methods, faster than wrapper methods</li>
</ul>
<h2 id="week-3">Week 3</h2>
<h3 id="data-journey-and-data-storage">Data Journey and Data Storage</h3>
<p>Raw features and labels -&gt; data transforms (feature eng, etc) -&gt; training<br>
Data provenance (origin)<br>
Data lineage(history) - useful for debugging/understanding issues</p>
<p>Data versioning<br>
<strong>ML requires reproducibility</strong></p>
<ul>
<li>code versioning: github</li>
<li>environment versioning: Docker/ Terraform</li>
<li><strong>Data versioning</strong> require different tools: <em>DVC</em>, <em>Git-LFS</em></li>
</ul>
<p><strong>Metadata</strong>: tracking artifacts and pipeline changes [kind of logging in code]<br>
ML metadata terminology</p>
<ul>
<li>units: artifact, execution, context</li>
<li>types</li>
<li>relationships</li>
</ul>
<p><strong><code>ml-metadata</code> Lab</strong></p>
<h3 id="evolving-data">Evolving Data</h3>
<p><strong>Schema</strong>: containing a summary about the features in a dataset. Feature name, data type, required or optional, valency, domain: range, categories, default values.</p>
<ul>
<li>can help find problems, anomalies in a data set. E.g. missing values, values in a wrong type.</li>
<li>system resilience to data issues</li>
<li>scalability</li>
<li>schema multiple versions (training and prod) - version control for schema !!!<br>
multiple schema for different scenarios (same app on e.g. mobile dev vs desktop, maybe diff features available)</li>
</ul>
<p><em><strong>Your system and your development process must treat data errors as first-class citizens, just like code bugs.</strong></em></p>
<h3 id="feature-stores">Feature stores</h3>
<p><strong>Data warehouse</strong> - aggregate data from multiple sources, processed and analyzed, not real time.<br>
subject oriented<br>
<img src="https://www.dropbox.com/s/xywb7qzknf2we2p/c2w3_1.png?raw=1" alt=""><br>
<strong>Data Lakes</strong><br>
system or repository of data stored in its natural and raw format, which is usually in the form of blobs or files.<br>
May include structured / semi-structures/ unstructured data<br>
Don’t do any processing (data in raw format ) - don’t require a schema<br>
Blob - binary large object (image, audio file, code exe, etc.)<br>
<img src="https://www.dropbox.com/s/96uh6lf74rejsnl/c2w3_2.png?raw=1" alt=""></p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

