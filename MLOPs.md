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
<li><a href="#week-2---modeling">Week 2 - Modeling</a>
<ul>
<li><a href="#error-analysis">Error Analysis</a></li>
<li><a href="#data-iterations">Data Iterations</a></li>
</ul>
</li>
<li><a href="#week-3">Week 3</a>
<ul>
<li><a href="#data">Data</a></li>
</ul>
</li>
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
<p><strong>Monitoring</strong><br>
<strong>Monitoring dashboard</strong> (server load, fraction of nan/missing inputs, fraction of not null outputs)</p>
<ul>
<li>Brainstorming of metric that will detect problems</li>
<li>Many metrics in beginning and keep only useful/</li>
<li><em>Software metrics</em> (memory, load, latency etc)</li>
<li><em>Input metrics</em> - data distribution, % missing values</li>
<li><em>Output metrics</em> - times return Null, CTR</li>
<li>Set thresholds for alarms, adapt over time</li>
</ul>
<p>Deployment is iterative.</p>
<p><strong>Pipeline monitoring</strong><br>
System build from multiple modules.<br>
Monitoring each module individually.</p>
<h2 id="week-2---modeling">Week 2 - Modeling</h2>
<p>Model-centric AI vs Data-centric AI (even more important and kind of low-hanging fruit)<br>
Data centric - improve the data<br>
AI system = Code + Data.            (code is also algorithm/model)</p>
<ol>
<li>Doing well on training set (training error)</li>
<li>Doing well on dev/test sets.</li>
<li>Doing well on business metrics/project goals!</li>
</ol>
<p><strong>Why low AVERAGE error isn’t good enough?</strong><br>
Performance on disproportionately <em>important</em> examples!</p>
<ul>
<li>discriminate some group of users (by language or ethnicity) / small retailers</li>
<li>rare (unbalanced) classes</li>
<li>the ML job is not doing well on the test set. BUT SOLVE REAL BUSINESS ISSUE!</li>
</ul>
<p><strong>Establish a baseline</strong> - indicate what is possible</p>
<ul>
<li>HLP (human level performance), but depends if structured or unstructured data (people usually good )</li>
<li>Literature search for SOTA / open source</li>
<li>Quick and dirty implementation</li>
<li>Performance of older system</li>
</ul>
<p><strong>Tips</strong></p>
<ul>
<li>Find reasonable open source algo (github)</li>
<li>sanity check: over-fit to small dataset</li>
</ul>
<h3 id="error-analysis">Error Analysis</h3>
<ol>
<li>manually go over N errors and fill a googleDoc with error reasons / <em>tags</em></li>
<li>iterative process</li>
<li>metrics for each tag:<br>
3.1 what fraction of errors has that tag<br>
3.2 of all data with the tag, what fraction is misclassified<br>
3.3 what fraction of all <strong>data</strong> has that tag!<br>
3.4 how much room for improvement is there on data with that tag (compare to HLP)</li>
</ol>
<p>How to prioritize:</p>
<ul>
<li>multiply 3.1 * 3.3 can be a prioritizing metric!</li>
<li>how much room for improvement</li>
<li>how easy to improve</li>
<li>how important is it</li>
</ul>
<p><strong>Adding improving data for specific categories! - more efficient that add general data!</strong></p>
<p><strong>Skewed datasets:</strong></p>
<ul>
<li>confusion matrix</li>
<li>0 /1 TN FN FP TP</li>
<li>precision / recall =&gt; F1 = 2 / (1/P + 1/R)</li>
<li>multiple classes: precision/recall/F1 for each class<br>
Use cases when you want high recall: fabric with human inspection after algo, legal doc retrieval system<br>
or high precision: google on top1/3 result</li>
</ul>
<p><img src="https://www.dropbox.com/s/zjr5u98yoyrlf95/C1W2_1.png?raw=1" alt="last auditing"><br>
ESTABLISH METRICS on APPROPRIATE SLICES OF DATA<br>
Cars/ pedestrians/ cyclist, long/mid/short distance, angle of view.<br>
Lane Detection: Highway vs Country road, Day vs Night</p>
<h3 id="data-iterations">Data Iterations</h3>
<ul>
<li><em>model centric</em> - most academic researches. Take data and dev  a best model for this data. Hold data fix</li>
<li><em>data-centric</em> view</li>
</ul>
<p><strong>Data augmentation</strong>:</p>
<ul>
<li>does it realistic</li>
<li>is x-&gt;y mapping clear (e.g. humans recognize speech)</li>
<li>is algo currently doing poorly on those examples</li>
</ul>
<p><strong>Can adding data hurt?</strong><br>
For unstructured data: if model is <strong>large</strong> and the <strong>mapping is clear x-&gt;y</strong> (e.g. human recognize good), then adding data rarely hurts accuracy.<br>
BUT it change data distribution! and can hurt in some rare cases.</p>
<p><strong>Adding features - structure data</strong><br>
user - restaurant recommendation<br>
add features “is person vegetarian” “is rest has vegetarian options?”</p>
<p><strong>Experiment tracking</strong></p>
<ul>
<li>Algo/code version</li>
<li>Data</li>
<li>Hyper-parameters</li>
<li>Results</li>
</ul>
<p><em>Tracking tools</em>: Spreadsheets, Experiment tracking system: <em>MLflow</em>, <em>weights&amp;biases</em>,  <em>Amazon SageMaker Studio</em>, <em>verta ai</em></p>
<h2 id="week-3">Week 3</h2>
<p><strong>Define Data and Establish Baseline</strong><br>
Data definition is hard - different ways of labeling (lanes- middle, inner ), <em>inconsistent</em><br>
<strong>Types of data problems:</strong><br>
Unstructured/ structured data<br>
small/ big data (thresh: 10k )<br>
<img src="https://www.dropbox.com/s/yasagooj9ldoe8k/c1w3_1.png?raw=1" alt="types of data/ML projects">Shifting from one quadrant to another is more difficult. (hiring new people, taking advice from another ML eng.)</p>
<p><em>Unstructured</em>: humans can label more, data augmentation<br>
<em>Structured</em>: how hard to collect more data? / is human labeling possible?</p>
<p><em>Small vs big data (10k)</em><br>
small data: clean label are critical / can manually look and fix/ small labeling team - easy to be consistent.<br>
big data: establish data process</p>
<p><strong>Improving label consistency</strong><br>
<img src="https://www.dropbox.com/s/s1gysnvslp673ne/c1w3_2.png?raw=1" alt="img">Sometimes merging 2 classes to 1 - make things simpler -&gt; more consistent</p>
<p><strong>HLP - Human Level Performance</strong><br>
Great baseline, or max level of performance (depends of context).<br>
Detect what can be possible<br>
How to measure HLP? -&gt; compare human to GT… but if GT is also created by human is just how 2 people agree/consistent …</p>
<p>Bit HLP level ? sometimes good (publish a paper), sometimes misleading, mask Algo errors</p>
<p>If <strong>GT is externally defined</strong>(e.g. come from precise measurements) HLP provide and estimation of irreducible error<br>
if <strong>GT is comes from human label</strong> HLP &lt;&lt; 100% may indicate ambiguous labeling instructions.</p>
<p>On <em>Structured data</em> HLP is less common (exceptions: User ID merging - same person, based on net traffic is the computer hacked, is transaction fraudulent, spam )</p>
<h3 id="data">Data</h3>
<p><strong>How long should you spend obtaining data</strong><br>
Avoid that data collection stage slow down the iterative cycle<br>
<img src="https://www.dropbox.com/s/l1j34cawb9tmt6b/c1w3_3.png?raw=1" alt="img"><br>
<strong>Inventory data:</strong> list down and compare data sources: <em>source</em>, <em>amount</em>, <em>cost</em>, <em>time</em><br>
sometimes purchase is better than in house labeling.</p>
<ul>
<li><em>in-house</em> vs <em>outsourced</em> vs <em>crowdsourced</em></li>
<li>it’s OK to label data by yourself, even help to better understand the project</li>
<li>who is qualified?
<ul>
<li>any reasonable person</li>
<li>subject matter expert</li>
<li>some times it’s almost impossible to label well - recommendation systems (need to relay on real data)</li>
</ul>
</li>
<li>don’t increase data too drastically, for sure less  than x10 at a time (x2 -x3 times)</li>
</ul>
<p><strong>Data pipeline</strong><br>
Development vs Production pipeline !!!<br>
Replicable data pipeline<br>
Separete POC stagean and production stage</p>
<p><strong>Structured data pipelines usually more complex</strong>:<br>
multiple data sources, cleaning, ip black list filtering, spam filtering, ID merge, for each task different sub-models etc. and in the end the main ML task model.<br>
Missing data/ missing features treatment</p>
<p><strong>Meta - data</strong> (data about data) - super important to save</p>
<ul>
<li>Time of pictures, factory, manufacture line #,  camera setting, phone model, inspector ID etc</li>
<li>device type, labeler ID, preprocess model id, data origin</li>
<li><strong>useful for error analysis, unexpected effects</strong></li>
</ul>
</div>
</body>

</html>

