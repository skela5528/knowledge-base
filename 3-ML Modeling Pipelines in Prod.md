<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>3-ML Modeling Pipelines in Prod</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li><a href="#course-3----ml-modeling-in-production">Course 3 - # ML Modeling in Production</a>
<ul>
<li><a href="#week-1">Week 1</a>
<ul>
<li><a href="#hyperparameter-tuning">Hyperparameter tuning</a></li>
<li><a href="#automl">AutoML</a></li>
<li><a href="#automl-on-the-cloud">AutoML on the Cloud</a></li>
</ul>
</li>
<li><a href="#week-2">Week 2</a>
<ul>
<li><a href="#dimensional-effect">Dimensional Effect</a></li>
<li><a href="#why-is-high-dim-data-a-problem">Why is high-dim data a problem?</a></li>
<li><a href="#dimensionality-reduction">Dimensionality Reduction</a></li>
<li><a href="#quantization-and-pruning">Quantization and Pruning</a></li>
</ul>
</li>
<li><a href="#week-3">Week 3</a>
<ul>
<li><a href="#distributed-training">Distributed Training</a></li>
<li><a href="#knowledge-distillation">Knowledge Distillation</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div></p>
<h1 id="course-3----ml-modeling-in-production">Course 3 - # ML Modeling in Production</h1>
<h2 id="week-1">Week 1</h2>
<h3 id="hyperparameter-tuning">Hyperparameter tuning</h3>
<p>NAS - Neural Arch Search - automating the design of AI nets</p>
<p><strong>Types of params in ML</strong></p>
<ul>
<li>trainable params [weights]</li>
<li>hyperparams -&gt; adjustable, set before training (e.g. LR, batch size, activation f, weights initialization)</li>
<li>hard to tune manually</li>
<li>but proper value can bust model performance</li>
</ul>
<p><strong>Automating hyperparams tuning</strong>: Keras Auto Tuner</p>
<h3 id="automl">AutoML</h3>
<p>AutoML automates the entire ML workflow<br>
Data Ingestion -&gt; D validation -&gt; Feat Eng -&gt; Train -&gt; Validation</p>
<p><strong>Neural Arch Search</strong>:</p>
<ul>
<li>search space
<ul>
<li>Macro: combining single layers      Micro: combining cells [net blocs] - more effective</li>
</ul>
</li>
<li>search strategy
<ul>
<li>grid search: all possible combinations</li>
<li>random search: randomly pick</li>
<li>Bayesian</li>
<li>Evolutionary methods: GA</li>
<li>Reinforce Learning: agent reward</li>
</ul>
</li>
</ul>
<p><a href="https://arxiv.org/pdf/1808.05377.pdf">https://arxiv.org/pdf/1808.05377.pdf</a><br>
<a href="https://distill.pub/2020/bayesian-optimization/">https://distill.pub/2020/bayesian-optimization/</a><br>
<a href="https://arxiv.org/pdf/1611.01578.pdf">https://arxiv.org/pdf/1611.01578.pdf</a><br>
<a href="https://arxiv.org/pdf/1712.00559.pdf">https://arxiv.org/pdf/1712.00559.pdf</a><br>
<a href="https://arxiv.org/abs/1603.01670">https://arxiv.org/abs/1603.01670</a></p>
<ul>
<li><strong>performance estimation strategy</strong>
<ul>
<li>straight forward validation evaluation is heavy and costly, alternatives:</li>
<li>Lower Fidelity Estimates: reduce training time: use data subset, lower resolution imgs, fewer filters/ layers. Not works well for many practical cases</li>
<li>Learning Curve Extrapolation</li>
<li>Weight Inheritance: init weights of new arch based on prev trained arch</li>
</ul>
</li>
</ul>
<h3 id="automl-on-the-cloud">AutoML on the Cloud</h3>
<ul>
<li><strong>Amazon SageMaker Autopilot</strong> more classical scenarios [structured data]</li>
<li><strong>Microsoft Azure  AutoML</strong></li>
<li><strong>Google Cloud AutoML</strong> Auto ML VIsion / VideoIntelegence/ NLP/ Translation -&gt; for different tasks/ Tables (for structured data)</li>
</ul>
<h2 id="week-2">Week 2</h2>
<h3 id="dimensional-effect">Dimensional Effect</h3>
<p>on NN:</p>
<ul>
<li>yes NN can perform kind of feature selection</li>
<li>but it’s not efficient
<ul>
<li>much model power will be shut off to ignore unwanted features</li>
<li>consume extra space and resources, both model and data</li>
<li>unwanted f can introduce noise</li>
</ul>
</li>
</ul>
<h3 id="why-is-high-dim-data-a-problem">Why is high-dim data a problem?</h3>
<ul>
<li>more dims more features</li>
<li>risk of over-fitting</li>
<li>distances grow more and more alike</li>
<li>no clear distinction btw clusters/classes<br>
“As we add more dims we also increase the processing power … as well as the amount of training data required.”</li>
<li>redundant/ irrelevant features</li>
<li>more noise added than signal</li>
<li>hard to interpret and vis</li>
<li>hard to store and proc<br>
<img src="https://www.dropbox.com/s/bc3qa9ca5j8lf74/c3w2_1.png?raw=1" alt=""><br>
<strong>The Hughes effect</strong><br>
The more the features, the larger the hypothesis space.<br>
The lower the hypothesis space:</li>
<li>the easier it’s to find the correct hypothesis</li>
<li>the less examples you need</li>
</ul>
<h3 id="dimensionality-reduction">Dimensionality Reduction</h3>
<ul>
<li>Linear dim reduction
<ul>
<li>LDA Linear discriminant analysis (for classification)</li>
<li>PLS partial least squares (regression)</li>
<li>PCA Principal componen (unsup)</li>
</ul>
</li>
</ul>
<p><strong>Singular value decomposition (SVD)</strong></p>
<ul>
<li>decompose not squared matrices</li>
<li>useful for sparse matrices as TF-IDF</li>
<li>remove redundant features from dataset</li>
<li>decompose to 3 matrices: <strong>M=UEV*</strong></li>
</ul>
<p><strong>Independent Component Analysis (ICA)</strong></p>
<ul>
<li>PCA seeks directions on f space that minimize reconstruction error</li>
<li>ICA seeks directions that are most stat. independent</li>
<li>ICA address higher order dependence</li>
</ul>
<p><strong>Non-negative Matrix Factorization (NMF)</strong></p>
<h3 id="quantization-and-pruning">Quantization and Pruning</h3>
<ul>
<li>Mobile, IoT will grow and will require more ML</li>
<li>Demands move ML capability from cloud to on-device</li>
<li>privacy (require to keep a data on device)</li>
</ul>
<p><strong>Why quantize neural net?</strong></p>
<ul>
<li>NNs have many params and take up space</li>
<li>shrinking model file size</li>
<li>reduce comp resources</li>
<li>model run faster and use less power</li>
</ul>
<p><strong>Trade-offs</strong></p>
<ul>
<li>accuracy</li>
<li>loss of interpretability</li>
</ul>
<p><strong>Post-training quantization</strong><br>
avalible at tf.lite</p>
<pre><code>import tensorflow as tf
converter = tf.lite.TFLiteConverter.from_saved_model(saved_model_dir)
converter.optimizations = [tf.lite.Optimize.DEFAULT]
tflite_quant_model = converter.convert()
</code></pre>
<p><strong>Quantization-aware training (QAT)</strong></p>
<ul>
<li>insert fake quantization (FQ) noted in the forward pass</li>
<li>the model learn better quantization</li>
<li>avalible at <code>tensorflow_model_optimization</code></li>
</ul>
<p><strong>Pruning</strong></p>
<ul>
<li>reduce the number of params and/or operations</li>
<li>model sparsity</li>
<li>avalible at <code>tensorflow_model_optimization</code></li>
</ul>
<p><img src="https://www.dropbox.com/s/89pjvnhy91mv994/c3w2_2.png?raw=1" alt=""></p>
<h2 id="week-3">Week 3</h2>
<h3 id="distributed-training">Distributed Training</h3>
<p>more efficient, speed-up<br>
<strong>data vs model parallelism</strong></p>
<p><strong>data parallelism:</strong> models are replicated onto different GPU (workers) and data split btw them.</p>
<ul>
<li>each worker compute loss on their data</li>
<li>do backprop and update the model</li>
<li>pass the deltas to the second worker (synchronize) in the end of each bach</li>
<li>maybe synchronous or asynchronous</li>
</ul>
<p><strong>model parallesm</strong>:  model too large to fit into one device, then they divided into partitions,  and different partitions goes to different workers.</p>
<p><code>tf.distribute.Strategy</code></p>
<p><em>One Device strategy</em> - no distribution (e.g. for testing your code before switching to distr. training)<br>
<em>Mirrored strategy</em> - on one machine with multiple GPUs<br>
<em>Parameter Server strategy</em> - some machines are workers, and other as parameter servers</p>
<p><em>Fault tolerance</em><br>
if one worker fail?</p>
<p><strong>Pipelines</strong></p>
<ul>
<li>prefetching</li>
<li>parallelize data extraction and transformation</li>
<li>caching</li>
</ul>
<h3 id="knowledge-distillation">Knowledge Distillation</h3>
<p><strong>Teacher and Student Nets</strong></p>
<p>Big sophisticated nets have a good quality but difficult for deployment.</p>
<p>Knowledge Dist. goal - duplicate the performance of complex model in a <strong>simpler</strong> model.</p>
<p><strong>Teacher</strong> - training first with normal training procedure<br>
<strong>Student</strong> - learn teacher probability prediction  - “soft target”<br>
the probability is much more informative then predictions themself.</p>
<p><img src="https://www.dropbox.com/s/9od6fsd1pxczqy1/c3w3_1.png?raw=1" alt="">&gt; The relative probabilities of the incorrect outputs tell us a lot about how the model tend to generalize. — <a href="https://arxiv.org/pdf/1503.02531.pdf">https://arxiv.org/pdf/1503.02531.pdf</a></p>
<p><strong>This is the dark knowledge!</strong> Softened probabilities reveal this dark (hidden) knowledge learnt by the model. Extracting and using this dark knowledge is also known as <strong><em>distillation</em></strong>. We will revisit this concept again in the next section with a real world example.</p>
<p><strong>Tecniques</strong></p>
<ol>
<li>Weight objectives (student and teacher) and combine during backprop</li>
<li>Compare distributions of the predictions using KL divergence</li>
</ol>
<p>Loss = (1-a)L<sub>hard</sub> + a*L<sub>KL</sub></p>
</div>
</body>

</html>

