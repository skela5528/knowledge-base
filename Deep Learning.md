<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Deep Learning</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li><a href="#overview-papers">Overview Papers</a></li>
<li><a href="#cnn-visualization">CNN Visualization</a></li>
<li><a href="#segmentation">Segmentation</a></li>
<li><a href="#unsupervised">Unsupervised</a></li>
<li><a href="#anomaly-and-action-detection-in-video">Anomaly and Action Detection in Video</a></li>
<li><a href="#self-driving-cars--trajectories">Self Driving Cars / Trajectories</a></li>
<li><a href="#pruning">Pruning</a></li>
<li><a href="#activation-units">Activation Units</a></li>
<li><a href="#face-recognition">Face Recognition</a>
<ul>
<li>
<ul>
<li><a href="#triplet-loss">Triplet Loss</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#cnn-misc">CNN Misc</a>
<ul>
<li><a href="#weights-initialization">Weights initialization</a></li>
<li><a href="#net-speedresources-consumption">Net speed/resources consumption</a></li>
</ul>
</li>
</ul>
</div></p>
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
<p><strong>Deep Face Recognition: A Survey</strong> [2018 cit 14] <a href="https://arxiv.org/pdf/1804.06655.pdf">link</a></p>
<p><strong>UnitBox: An Advanced Object Detection Network</strong> [2016 cit 84] <a href="https://arxiv.org/pdf/1608.01471.pdf">link</a></p>
<blockquote>
<p>The paper proposes a highly effective and efficient CNNbased object detection network, called UnitBox.<br>
Predict the object bounds as well as the pixel-wise classification scores on the feature maps.<br>
Particularly, UnitBox takes advantage of a novel Intersection over Union (IoU) loss function for bounding box prediction.</p>
</blockquote>
<p>Replacing L2 localization loss of each coordinate with IOU loss (log of IOU), which links all the coordinated together, since the bounds of an object are highly correlated.<br>
Faster converge, more robust than L2 loss.<br>
Show results on face data set.</p>
<p><img src="https://www.dropbox.com/s/feb0k0b64f7y9y0/l2_iou_loss.jpg?raw=1" alt="img"></p>
<pre><code>input: feature_map_pixel[i, j] with feature_vector
e.g. center pixel from some region proposal algorithms 
output: bounding box (bbox) - top, bottom, left, right (t, b, l, r) distances from pixel
how: regression which predict bbox t, b, l, r from feature_vector
</code></pre>
<p><em>L2 Loss</em><br>
<code>SumSquares(gt_tblr, pred_tblr)</code></p>
<ul>
<li>4 values optimizes separably, *but * them correlated.<br>
Frequent error: one or two bounds of a predicted box are very close to the gt but the entire bounding box is unacceptable.</li>
<li>Bigger bboxes have bigger impact to the loss f. (bigger distances from center pxl to bounds)<br>
Overcome with image patches  normalization, but still have negative effect to detection.</li>
</ul>
<p><em>IoU Loss</em><br>
<img src="https://www.dropbox.com/s/ekpmpqipx2lh12d/IoULossAlgo.jpg?raw=1" alt="iouLoss"></p>
<p><em>UnitBox Net</em><br>
<code>Input: 1) orig img 2) pixelwise conf heatmap - object mask 3) bbox heatmap -&gt; gt bbox</code><br>
2 branches net</p>
<pre><code>1st branch: 
   VGG16-4th block-&gt;CONV[512x3x3x1] (1-output_size)-&gt; 
   Upsample[DE-CONV] -&gt; 1-channel feature_map with orig_ima size
   sigmoid cross-entropy loss -&gt; conf_scores
</code></pre>
<pre><code>2nd branch: 
   VGG16-5th block-&gt;CONV[512x3x3x4] (4-output_size)-&gt; 
   Upsample[DE-CONV] -&gt; 4-channel feature_map with orig_ima size
   ReLU[ensure positive values] -&gt; IoULoss -&gt; box coordiantes t, b, l, r 
</code></pre>
<p>The final loss is calculated as the weighted average over the losses of the two branches.</p>
<h3 id="triplet-loss">Triplet Loss</h3>
<p>Andrew Ng video - <a href="https://www.coursera.org/learn/convolutional-neural-networks/lecture/HuUtN/triplet-loss">link</a><br>
Force that similar things will have embedded features with high similarity score.</p>
<pre><code>Given 3 samples: anchor -a, positive -p and negative -n:

   d - distance function e.g. d(a, p)=L2_norm(f(a), f(p))
   L(a, p, n) = max{d(a,p) - d(a,n) + margin, 0}
</code></pre>
<p>How to choose those triplets?<br>
Randomly? - too easy, not much to learn<br>
Choose triplets that are “hard”! : d(a, p) close to d(a, n)</p>
<h1 id="cnn-misc">CNN Misc</h1>
<h2 id="weights-initialization">Weights initialization</h2>
<h2 id="net-speedresources-consumption">Net speed/resources consumption</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

