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
<li><a href="#week-3">Week 3</a></li>
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
<h2 id="week-3">Week 3</h2>
<h2 id="week-4">Week 4</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

