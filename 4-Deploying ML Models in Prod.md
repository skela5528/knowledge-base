<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>4-Deploying ML Models in Prod</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li><a href="#course-4---deploying-machine-learning-models-in-production">Course 4 - Deploying Machine Learning Models in Production</a>
<ul>
<li><a href="#week-1">Week 1</a>
<ul>
<li><a href="#introduction-to-model-serving">Introduction to Model Serving</a></li>
</ul>
</li>
<li><a href="#week-2">Week 2</a>
<ul>
<li><a href="#model-serving-arch">Model Serving Arch</a></li>
</ul>
</li>
<li><a href="#scaling-infrastructure">Scaling Infrastructure</a>
<ul>
<li><a href="#online-inference">Online Inference</a></li>
<li><a href="#data-preprocessing">Data preprocessing</a></li>
</ul>
</li>
<li><a href="#week-3">Week 3</a>
<ul>
<li><a href="#experiments-management-and-tracking">Experiments Management and Tracking</a></li>
<li><a href="#mlops">MLOps</a></li>
<li><a href="#continuous-delivery">Continuous delivery</a></li>
<li><a href="#progressive-delivery">Progressive delivery</a></li>
</ul>
</li>
<li><a href="#week-4">Week 4</a></li>
</ul>
</li>
</ul>
</div></p>
<h1 id="course-4---deploying-machine-learning-models-in-production">Course 4 - Deploying Machine Learning Models in Production</h1>
<h2 id="week-1">Week 1</h2>
<h3 id="introduction-to-model-serving">Introduction to Model Serving</h3>
<p>Serving a models, what is it?<br>
training the model -&gt; make the model available to the users -&gt; provide service or app for interaction<br>
<strong>Important metrics:</strong></p>
<ul>
<li><em>latency:</em> delay btw user action and response of application to user’s action.</li>
<li><em>throughput:</em> num of successful requests served per unit time (e.g. one second)</li>
<li><em>cost</em></li>
</ul>
<p>model complexity -&gt; increase the cost! - tradeoff</p>
<p><strong>Data centers vs embedded device</strong><br>
<img src="https://www.dropbox.com/s/vocc67k8unkznmb/c4w1_1.png?raw=1" alt=""><br>
server arch:<br>
<img src="https://www.dropbox.com/s/cxofajr110umuze/c4w1_2.png?raw=1" alt=""></p>
<h2 id="week-2">Week 2</h2>
<h3 id="model-serving-arch">Model Serving Arch</h3>
<p><em>On Prem</em> (On-premises software, running in the premises - property the opposite of remote) vs <em>On Cloud</em></p>
<p>Model servers:</p>
<ul>
<li><a href="https://www.tensorflow.org/tfx/serving/architecture">Tensorflow Serving</a></li>
<li><a href="https://github.com/pytorch/serve">TorchServe</a></li>
<li>KF Serving (Kubeflow)</li>
<li>Triton inference server - nvidia</li>
</ul>
<h2 id="scaling-infrastructure">Scaling Infrastructure</h2>
<p><strong>vertical scaling</strong> -&gt; bigger and more powerful machine/ hardware</p>
<p><strong>horizontal scaling</strong>: add more machines !!! that’s usually a much better choice</p>
<p><img src="https://www.dropbox.com/s/tisbm213aaqsyxc/c4w2_1.png?raw=1" alt=""><br>
Containers much better than Virtual Machines<br>
To use multiple containers efficient one need Container Orchestration Tools:<br>
Kubernetes or Docker Swarm</p>
<p>In containers, app instances don’t require separate operating systems. In addition, the abstraction of having them run within a container runtime gives you greater flexibility.</p>
<h3 id="online-inference">Online Inference</h3>
<p>Inference Optimization: infrastructure, model architecture,  model compilation</p>
<h3 id="data-preprocessing">Data preprocessing</h3>
<p>Before sending GET requites to the app</p>
<ul>
<li>correcting invalid values</li>
<li>feature normalization</li>
<li>one hot encoding, vectorization</li>
<li>etc</li>
</ul>
<p><img src="https://www.dropbox.com/s/57637r5uhp4ce9n/c4w2_2.png?raw=1" alt=""></p>
<h2 id="week-3">Week 3</h2>
<h3 id="experiments-management-and-tracking">Experiments Management and Tracking</h3>
<ul>
<li>ML requires a lot of experiments, tracking results is important</li>
<li>ML debugging is difficult</li>
<li>Small changes can lead to drastic changes in model performance (layers arch, GT etc) - need to track those changes</li>
<li>Running experiments is time and costs consuming. Difficult to rerun -&gt; better to track properly</li>
</ul>
<p>__ track experiments:__</p>
<ul>
<li>
<p>enable to reproduce results</p>
</li>
<li>
<p>meaningfully compare experiments</p>
</li>
<li>
<p>require to manage code and data versions, hyperparameters, env, metrics.</p>
</li>
<li>
<p>organize in a meaningful way, make them available to access and collaborate on within the organization</p>
</li>
<li>
<p>modular code</p>
</li>
<li>
<p>git</p>
</li>
<li>
<p>directory structures if use a shared repo</p>
</li>
<li>
<p>config files</p>
</li>
</ul>
<p><strong>Tools for exp tracking</strong></p>
<ul>
<li>experimental changes include changes in data</li>
<li>Data Versioning:
<ul>
<li>Neptune - <a href="https://neptune.ai/">https://neptune.ai/</a> commercial</li>
<li>Pachyderm - <a href="https://www.pachyderm.com/">https://www.pachyderm.com/</a></li>
<li>Delta Lake</li>
<li>Git LFS (large files storage) - <a href="https://git-lfs.github.com/">https://git-lfs.github.com/</a> - store the pointer to the big binary file in git when the actual file is stored in separate storage</li>
<li>Dolt - <a href="https://www.dolthub.com/">https://www.dolthub.com/</a></li>
<li>lakeFS <a href="https://lakefs.io/">https://lakefs.io/</a> - open source</li>
<li>DVC</li>
<li>ML-Metadata - TF family</li>
</ul>
</li>
</ul>
<p>in order to track results: save all parameters that can affect results + ADD MEANINGFUL TAGS and notes</p>
<p>tensorBoard<br>
<strong>wandb</strong> <a href="https://wandb.ai/site">https://wandb.ai/site</a></p>
<h3 id="mlops">MLOps</h3>
<p><strong>Data Scientists  vs SW eng</strong><br>
DS:<br>
- focus on fixed data sets<br>
- focus on model metrics<br>
- prrototyping in Jupyter notebooks<br>
- expert in modeling techniques and feature engineering<br>
- model size, cost, latency and fairness are often ignored</p>
<p>SW eng:</p>
<ul>
<li>build a product</li>
<li>concerned about cost, performance, stability, schedule</li>
<li>identify quality through customer satisfaction</li>
<li>scale solutions, handle large amounts of data</li>
<li>consider requirements for security safety and fairness</li>
<li>maintenance and extend the product over long periods</li>
</ul>
<p><strong>Key problems affecting ML today</strong><br>
Those actually same problems that SW were in 90s:<br>
<img src="https://www.dropbox.com/s/v2ahzflva58cyhp/c4w3_1.png?raw=1" alt=""><br>
MLOps is bridging the ML and IT<br>
<img src="https://www.dropbox.com/s/apaytpgzc302qk9/c4w3_2.png?raw=1" alt=""><br>
<strong>MLOps Level 0</strong> - Manual process<br>
Less frequent releases, so no CI/CD<br>
Lack of active performance monitoring - dangerous<br>
Very common in real world</p>
<p><strong>challenges</strong><br>
retraining (e.g. new data, new requirements etc)<br>
contentiously experimenting with new implementation</p>
<p><strong>MLOps Level 1</strong> ML pipeline automation<br>
automated deployment<br>
rapid experimentation<br>
automated data validation</p>
<p><strong>MLOps Level 2</strong> CI/CD pipeline automation</p>
<p><strong>TFX  - tensorflow extended</strong><br>
Orchestrate your ML workflow</p>
<p><a href="https://cloud.google.com/architecture/architecture-for-mlops-using-tfx-kubeflow-pipelines-and-cloud-build">https://cloud.google.com/architecture/architecture-for-mlops-using-tfx-kubeflow-pipelines-and-cloud-build</a></p>
<p><strong>Model versioning</strong><br>
Software versioning:<br>
<img src="https://www.dropbox.com/s/g3a1mevph12v0rb/c4w3_3.png?raw=1" alt=""><br>
<img src="https://www.dropbox.com/s/gjh6lmh1hlmew63/c4w3_4.png?raw=1" alt=""></p>
<p>Machine Learning Model Management: What It Is, Why You Should Care, and How to Implement It<br>
<a href="https://neptune.ai/blog/machine-learning-model-management">https://neptune.ai/blog/machine-learning-model-management</a></p>
<h3 id="continuous-delivery">Continuous delivery</h3>
<p><img src="https://www.dropbox.com/s/k4fu1qobwoci56l/c4w3_5.png?raw=1" alt=""><br>
<img src="https://www.dropbox.com/s/ru7xz7srwqn1xex/c4w3_6.png?raw=1" alt=""></p>
<h3 id="progressive-delivery">Progressive delivery</h3>
<p><img src="https://www.dropbox.com/s/o0buzqa6jipx16o/c4w3_7.png?raw=1" alt=""><br>
<strong>Blue/Green deployment</strong><br>
2 models on (previous and new)<br>
load balancer decide when sent a requiest to green (new) or to blue (prev version) if something goes wrong.</p>
<p><strong>Canary deployment</strong><br>
Similar to blue/green<br>
but the change is done gradually</p>
<p>more details <a href="https://codefresh.io/docs/docs/ci-cd-guides/progressive-delivery/">here</a></p>
<h2 id="week-4">Week 4</h2>
<p><strong>Observability in ML</strong></p>
<ul>
<li>measure how well the internal states of a system can be inferred by knowing the inputs ad outputs.</li>
</ul>
<p>Goals of ML observability:</p>
<ul>
<li>Alertable</li>
<li>Actionable: root cause clearly identified</li>
</ul>
<p><strong>Monitoring Targets in ML</strong><br>
Basics inputs and outputs monitoring</p>
<p>Input feature distribution<br>
Model prediction distribution<br>
model versions</p>
<p>use statistical testing (median, mean, std, min, max values) for comparison</p>
<p><strong>Loging</strong><br>
is important for observability</p>
<p>Understand the issue cause on distributed, cloud base system is much harder:<br>
solution Dapper-Style tracing apps:</p>
<ul>
<li>propagate trace between services</li>
<li></li>
</ul>
</div>
</body>

</html>

