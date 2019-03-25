<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Deep Learning</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p>[TOC]</p>
<h1 id="overview-papers">Overview Papers</h1>
<ul>
<li>Awesome deep learning papers  - <a href="%5Bhttps://github.com/terryum/awesome-deep-learning-papers%5D(https://github.com/terryum/awesome-deep-learning-papers)">github link</a></li>
<li>A Non-Technical Survey on Deep Convolutional Neural Network Architectures [2018-cit 5] <a href="%5Bhttps://arxiv.org/pdf/1803.02129.pdf%5D(https://arxiv.org/pdf/1803.02129.pdf)">link</a></li>
<li>Recent Advances in Object Detection in the Age of Deep Convolutional Neural Networks [2018-cit 0] <a href="https://arxiv.org/abs/1809.03193">link</a></li>
<li>Deep Convolutional Neural Networks for Image Classification: A Comprehensive Review [2017 cit 145] <a href="https://www.mitpressjournals.org/doi/pdf/10.1162/neco_a_00990">link</a></li>
</ul>
<h1 id="cnn-visualization">CNN Visualization</h1>
<p><strong>Hierarchical interpretations for neural network predictions</strong> [2018 cit 3] <a href="https://arxiv.org/pdf/1806.05337">link</a><br>
Use of hierarchical interpretations to explain DNN predictions.</p>
<p>Given a prediction from a trained DNN, ACD produces a hierarchical clustering of the input features, along with the contribution of each cluster to the final prediction. This hierarchy is optimized to identify clusters of features that the DNN learned are predictive.</p>
<p>Agglomerative contextual decomposition (ACD)</p>
<h1 id="segmentation">Segmentation</h1>
<p><strong>Mask R-CNN</strong> [2017 cit 1730] <a href="https://arxiv.org/pdf/1703.06870.pdf">paper</a> <a href="https://github.com/matterport/Mask_RCNN">github</a></p>
<h1 id="unsupervised">Unsupervised</h1>
<p><strong>Unsupervised Feature Learning via Non-Parametric Instance Discrimination</strong> [2018 cit 7] <a href="https://arxiv.org/pdf/1805.01978.pdf">link</a><br>
Code available</p>
<p>Unsupervised learning of image embedding<br>
“learn to discriminate between individual instances, without any notion of semantic categories, …, that captures apparent similarity among instances.”<br>
“now that the number of “classes” is the size of the entire training set”</p>
<p><strong>Learning to Segment Every Thing</strong> (<em>Kaiming He</em>) [2017 cit 41] <a href="https://arxiv.org/pdf/1711.10370.pdf">link</a><br>
Is it possible to train high quality instance segmentation models without complete instance segmentation annotations for all categories?</p>
<p>…Partially supervised instance segmentation task - transfer learning method to address it.</p>
<p><em>Tasks</em>: (1) given a set of categories of interest, a small subset has instance mask annotations, while the other categories have only bounding box annotations; (2) the instance segmentation algorithm should utilize this data to fit a model that can segment instances of all object categories in the set of interest.</p>
<p><em>How?</em> - #TODO</p>
<h1 id="anomaly-and-action-detection-in-video">Anomaly and Action Detection in Video</h1>
<h1 id="self-driving-cars--trajectories">Self Driving Cars / Trajectories</h1>
<h1 id="pruning">Pruning</h1>
<h1 id="activation-units">Activation Units</h1>
<h1 id="face-recognition">Face Recognition</h1>
<p><strong>Deep Face Recognition: A Survey</strong> [2018 cit 14] [link]](<a href="https://arxiv.org/pdf/1804.06655.pdf">https://arxiv.org/pdf/1804.06655.pdf</a>))</p>
<hr>
<h3 id="triplet-loss">Triplet Loss</h3>
<p>Ng video - <a href="https://www.coursera.org/learn/convolutional-neural-networks/lecture/HuUtN/triplet-loss">link</a></p>
<p><span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi mathvariant="normal">Γ</mi><mo>(</mo><mi>n</mi><mo>)</mo><mo>=</mo><mo>(</mo><mi>n</mi><mo>−</mo><mn>1</mn><mo>)</mo><mo>!</mo><mspace width="1em"></mspace><mi mathvariant="normal">∀</mi><mi>n</mi><mo>∈</mo><mi mathvariant="double-struck">N</mi></mrow><annotation encoding="application/x-tex">\Gamma(n) = (n-1)!\quad\forall
n\in\mathbb N</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">Γ</span><span class="mopen">(</span><span class="mord mathit">n</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mopen">(</span><span class="mord mathit">n</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">1</span><span class="mclose">)</span><span class="mclose">!</span><span class="mspace" style="margin-right: 1em;"></span><span class="mord">∀</span><span class="mord mathit">n</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">∈</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 0.68889em; vertical-align: 0em;"></span><span class="mord mathbb">N</span></span></span></span></span></p>
<h1 id="cnn-misc">CNN Misc</h1>
<h2 id="weights-initialization">Weights initialization</h2>
<h2 id="net-speedresources-consumption">Net speed/resources consumption</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>
