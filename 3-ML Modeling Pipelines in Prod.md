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
</div>
</body>

</html>

