<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MLOPs</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li><a href="#course-1---introduction-to-machine-learning-in-production">Course 1 - Introduction to Machine Learning in Production</a>
<ul>
<li><a href="#week-1">Week 1</a></li>
<li><a href="#week-2">Week 2</a></li>
<li><a href="#week-3">Week 3</a></li>
</ul>
</li>
</ul>
</div></p>
<h1 id="course-1---introduction-to-machine-learning-in-production">Course 1 - Introduction to Machine Learning in Production</h1>
<h2 id="week-1">Week 1</h2>
<p><img src="https://www.dropbox.com/s/dynlfyekxd83psl/c1w1_1.png?raw=1" alt="ML proj cycle"></p>
<p><strong>Steps of an ML Project</strong><br>
<strong>Scoping:</strong>  	define project<br>
<strong>Data:</strong> 		a) define data and baseline b) Label and or the data<br>
<strong>Modeling:</strong> 	a) select and train model b) error analysis<br>
<strong>Deployment:</strong> 	a) deploy in prod. b) monitor and maintain</p>
<p><strong>Deployment challenges</strong><br>
<strong>Concept drift</strong> the rules of mapping X-&gt;Y is different. For example COVID- more purchases online.<br>
<strong>Data drift</strong> different devices (different microphone or camera). Gradual change (usually) or Sudden change. Input data distribution is changes.<br>
<strong>Software eng. issues</strong></p>
<ul>
<li>real-time vs batch</li>
<li>cloud vs edge/browser</li>
<li>computer resources cpu/gpu/memory</li>
<li>latency/ throughput (QPS)</li>
<li>logging (need to save as much as possible, enable retrain data if needed)/ user feedbacks</li>
<li>security and privacy</li>
</ul>
<p><strong>Deployment Patterns</strong><br>
USE CASES:</p>
<ol>
<li>New product/capability</li>
<li>Automate/assist with manual task</li>
<li>Replace previous ML system</li>
</ol>
<p>Key ideas : <strong>Gradual ramp-up</strong> and  <strong>Rollback</strong></p>
<p>PATTERNS:</p>
<ol>
<li>Shadow mode - AI system in parallel with human or prev. system.</li>
<li>Small scale mode (canary) only 5% (X%) of the traffic and gradually increase</li>
<li>Easy rollback (Blue/green) - switch to old version in click if something wrong. Keep 2 systems (old and new) in parallel.</li>
</ol>
<p><img src="https://www.dropbox.com/s/dsruled6x4hxcy8/c1w1_2.png?raw=1" alt="levels of automation"></p>
<h2 id="week-2">Week 2</h2>
<h2 id="week-3">Week 3</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

