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
<li><a href="#object-detection">Object Detection</a></li>
<li><a href="#cnn-visualization">CNN Visualization</a></li>
<li><a href="#segmentation">Segmentation</a></li>
<li><a href="#unsupervised">Unsupervised</a></li>
<li><a href="#anomaly-and-action-detection-in-video">Anomaly and Action Detection in Video</a></li>
<li><a href="#self-driving-cars">Self Driving Cars</a>
<ul>
<li><a href="#trajectory-prediction">Trajectory prediction</a></li>
<li><a href="#environmental-model">Environmental model</a></li>
</ul>
</li>
<li><a href="#pruning">Pruning</a></li>
<li><a href="#convolution-layers">Convolution Layers</a></li>
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
<li><a href="#arch">Arch</a></li>
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
<h1 id="object-detection">Object Detection</h1>
<p><strong>RepPoints: Point Set Representation for Object Detection</strong>-microsoft [2019 cit 5] <a href="https://arxiv.org/pdf/1904.11490.pdf">paper</a><br>
<img src="https://github.com/microsoft/RepPoints/blob/master/demo/reppoints.png?raw=true" alt="RepPoints">RepPoints is a new representation for object detection that consists of a set of points which indicate the spatial extent of an object and semantically significant local areas.</p>
<p><em>RepPoints more informative than boxes</em></p>
<ul>
<li>more precise localization</li>
<li>shape / pose estimation</li>
<li>as a result better feature learned during training</li>
<li>anchor free</li>
</ul>
<p><em>RepPoints representation</em></p>
<ul>
<li>R={(Xk, Yk)} - set of n points per object (n=9 in paper)</li>
</ul>
<p>*Learning *</p>
<ol>
<li>Localization Loss:</li>
</ol>
<ul>
<li>RepPoints converted to pseudoBox (for example: min and max of each dimension)</li>
<li>Computer diff between pseudoBox and GTbox</li>
<li>2 stages a) offsets from central point - KP center b) offsets from points found in a)</li>
</ul>
<ol start="2">
<li>object recognition loss: objectness + class score vecror with <em>focal loss</em></li>
</ol>
<p><em>FPN backbone</em></p>
<ul>
<li>multiple scale features help to overcome the absence of anchors (when two different objects locating at the same position in a feature map).</li>
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
<h1 id="self-driving-cars">Self Driving Cars</h1>
<h2 id="trajectory-prediction">Trajectory prediction</h2>
<p><strong>Social LSTM: human trajectory prediction in crowded spaces</strong> [2016 cit 357] <a href="http://cvgl.stanford.edu/papers/CVPR16_Social_LSTM.pdf">link</a><br>
Humans moving in crowded scenes adapt their motion based on the behaviour of other people in their vicinity.<br>
Such deviation in trajectory cannot be predicted by observing the person in isolation.</p>
<p>One LSTM for each person. This LSTM learns the state of the person and predicts their future positions. The vanilla LSTM is agnostic to the behaviour of other sequences. We address this limitation by connecting neighboring LSTMs through a new social pooling strategy.</p>
<p>Many to many LSTM: from input historical trajectory[(X<sub>1</sub>,Y<sub>1</sub>), …, (X<sub>obs</sub>, Y<sub>obs</sub>)] predict future  trajectory [(X<sub>obs+1</sub>,Y<sub>obs+1</sub>), …, (X<sub>pred</sub>, Y<sub>pred</sub>)]</p>
<p>During test time, we observe a trajectory for 3.2secs and predict their paths for the next 4.8secs. At a frame rate of 0.4, this corresponds to observing 8 frames and predicting for the next 12 frames.</p>
<p><strong>Short-term Motion Prediction of Traffic Actors for Autonomous Driving using Deep Convolutional Networks</strong> (<em>Uber</em>) [2018 cit 10] <a href="https://arxiv.org/pdf/1808.05819.pdf">link</a><br>
<em>Main topic</em> - predicting future state of autonomous vehicle’s surrounding.<br>
Good related works survey.</p>
<p><em>Input</em><br>
State of each actor: bounding box, position, velocity, acceleration, heading, and heading change rate.<br>
Maps: road and crosswalk locations, lane directions, lane boundaries etc.</p>
<p><em>Target</em><br>
Predict future x,y locations of all actors. Time step 0.1s, prediction horizon 3s.</p>
<p><em>Data</em><br>
Real world Uber data, 240 hours manually driving, not published.</p>
<p><em>Approach</em></p>
<ul>
<li>Instead of manually defining features that represent context for each actor, we propose to rasterize scene for the i-th actor at time step tj into an RGB image. Then, we train CNN using rasterized images as inputs to predict actor trajectory, where the network automatically infers relevant features.</li>
<li>Separate raster-image created for each actor.</li>
<li>Loss: Average distance(true_location, predicted_location)</li>
<li>Net: base CNN extract features from raster-image and concatenate with state vector (velocity, acceleration, heading change) -&gt; fully_connected(4096) -&gt; output 30 location coordinates (for 3 sec horizon).</li>
</ul>
<p>Used CNN (no LSTM or other RNN), in which all temporal data (past trajectory) encoded in one raster-image.</p>
<p><strong>Multi-Modal Trajectory Prediction of Surrounding Vehicles with Maneuver based LSTMs</strong> (<em>MicrosoftResearch</em>) [2018 cit 13] <a href="https://arxiv.org/pdf/1805.05499.pdf">link</a><br>
<em>Main topic</em> Maneuvers and trajectory prediction on straight highways.</p>
<h2 id="environmental-model">Environmental model</h2>
<p><strong>MonoGRNet: A Geometric Reasoning Network for Monocular 3D Object Localization</strong> [2018 cit 1] <a href="https://arxiv.org/pdf/1811.10247.pdf">link</a><br>
<a href="https://github.com/Zengyi-Qin/MonoGRNet">code</a></p>
<p><strong>Spatial As Deep: Spatial CNN for Traffic Scene Understanding</strong> (<em>SenseTime</em>) [2018 cit 22] <a href="https://arxiv.org/pdf/1712.06080.pdf">link</a><br>
Spatial CNN layers on top of VGG16 for lane detection<br>
CULane Dataset release</p>
<h1 id="pruning">Pruning</h1>
<p><strong>SlimYOLOv3: Narrower, Faster and Better for Real-Time UAV Applications</strong>  [2019 cit 1] <a href="https://arxiv.org/abs/1907.11093v1">link</a><br>
Keywords: SlimYOLOv3, object detection, drone, channel pruning, sparsity training</p>
<p>Channel pruning strategy applicable on any conv net.<br>
<img src="https://www.dropbox.com/s/0pkz5u0rpdwqgfd/slim_yolo3.jpg?raw=1" alt="Channel prunng"><br>
<em>YOLOv3 vs YOLOv3-SPP3</em></p>
<ul>
<li>
<p>add spatial pyramid pooling (SPP). SPP consists of 4 parallel maxpool  layers: 1x1, 5x5, 9x9, 13x13, extract multiscale deep features and fuse them by concat.</p>
</li>
<li>
<p>sparsity training. Learn importance score (scaling factors) for each channel during training.</p>
</li>
<li>
<p>channel pruning. Prune with some adaptive threshold (percentile).</p>
</li>
<li>
<p>fine tuning after pruning is necessary.</p>
</li>
</ul>
<h1 id="convolution-layers">Convolution Layers</h1>
<p><strong>Summary of several types of convolution commonly used in Deep Learning.</strong> <a href="https://towardsdatascience.com/a-comprehensive-introduction-to-different-types-of-convolutions-in-deep-learning-669281e58215">link</a></p>
<ol>
<li>Convolution v.s. Cross-correlation</li>
<li>Convolution in Deep Learning (single channel version, multi-channel version)</li>
<li>3D Convolution</li>
<li>1 x 1 Convolution</li>
<li>Convolution Arithmetic</li>
<li>Transposed Convolution (Deconvolution, checkerboard artifacts)</li>
<li>Dilated Convolution (Atrous Convolution)</li>
<li>Separable Convolution (Spatially Separable Convolution, Depthwise Convolution)</li>
<li>Flattened Convolution</li>
<li>Grouped Convolution</li>
<li>Shuffled Grouped Convolution</li>
<li>Pointwise Grouped Convolution</li>
</ol>
<p><strong>Transposed vs dilated</strong><br>
Both insert spaces between elements - confusing.</p>
<p><em>Transposed</em> (deconv/ fractionally-strided conv)<br>
<code>torch.nn.``ConvTranspose2d</code><br>
“smart” up-sampling, very useful for segmentation - during decoder stage. High-resolution.<br>
<em>output dims &gt; input dims</em><br>
Insert 0 between kps in <strong>feature map</strong> ,  padding.</p>
<p><em>Dilated</em><br>
<code>torch.nn.Conv2d</code>(<em>in_channels</em>, <em>out_channels</em>, <em>kernel_size</em>, <em>stride=1</em>, <strong><em>dilation=2</em></strong>)<br>
Insert spaces between the <strong>kernel elements</strong> (dilation=1 insert 0 elements)<br>
increase receptive fields. Make use in segmentation during encoder stage.</p>
<h1 id="activation-units">Activation Units</h1>
<p><img src="https://www.dropbox.com/s/qzuznr1ukcw8y0s/activations.jpg?raw=1" alt="activation functions"></p>
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
<h2 id="arch">Arch</h2>
<p><strong>Scale-Aware Trident Networks for Object Detection</strong> [2019 cit 30] <a href="https://arxiv.org/pdf/1901.01892v2.pdf">link</a><br>
<strong>Motivation</strong><br>
To remedy the large scale:<br>
(1) <em>Image Pyramid</em><br>
Multiple images of several scales as input. Feature extraction and detection independently for each scale.<br>
MSSD<br>
For face detection - detectors of different scales<br>
Multi scale training and testing??<br>
<em>Simple | price: inference time</em></p>
<p>(2) <em>Feature Pyramid</em><br>
utilize the features from different layers of CNNs for different scales<br>
I will put yolo2 here, utilize image once, and have detectors for different sizes (5 anchors).<br>
<em>Comp is fast, price - feature for different scales extracted from different layers, lack of features consistency -&gt; less effective training -&gt; more chances to offer-fit for each scale. Imbalance.</em></p>
<p>(3)<em>Trident network</em><br>
Get the best of two worlds.<br>
Generates scale-aware feature maps by trident blocks with different receptive fields.</p>
<p><strong>Investigation of Receptive Field</strong><br>
…as the receptive field increases, the performance of the detector on small objects drops… While for large objects, the detector benefits from the increasing receptive fields. [unbelievable]</p>
<p><strong>Trident Network</strong><br>
…takes a singlescale image as input, and then creates scale-specific feature maps through parallel branches where convolutions share the same parameters but with different dilation rates.</p>
<p><em>Trident multi-branch blocks</em></p>
<ul>
<li>3 branches with different dilation</li>
<li>weight sharing</li>
</ul>
<p><em>Weight sharing effects</em></p>
<ul>
<li>less params</li>
<li>“objects of different scales should go through a uniform transformation with the same representational power” ???</li>
<li>params trained on more data [3 scales and not each scale for each branch]</li>
</ul>
<p><em>Scale - aware training</em></p>
<ul>
<li>each branch trained on objects of specific scales (avoid training objects of extreme scales on mismatched branches)</li>
</ul>
<p><em>Inference</em></p>
<ul>
<li>generate prediction for each branch [for each scale]</li>
<li>NMS</li>
</ul>
<p><strong>Spatial Transformer Networks</strong>(Max Jaderberg Karen Simonyan Andrew Zisserman Koray Kavukcuoglu, GOOGLE) [2015 cit 2508] <a href="http://papers.nips.cc/paper/5854-spatial-transformer-networks.pdf">link</a><br>
<a href="https://pytorch.org/tutorials/intermediate/spatial_transformer_tutorial.html">Pytorch tutorial</a></p>
<p>Make long story short:</p>
<ul>
<li>learn transformation matrix T (e.g affine transform with 6 params)</li>
<li>this T is applied on the feature map (for example last layer with spatial dimension)</li>
<li>T learned in such way that is minimized the Loss</li>
<li>It is possible to learn multiple T, one for each type of objects.</li>
<li>During inference: before prediction layer, apply T on feature map!</li>
</ul>
<p><strong>EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks</strong> [2019 cit 300] <a href="https://arxiv.org/pdf/1905.11946.pdf">link</a></p>
<p><strong>Network scaling</strong></p>
<ul>
<li>width scaling - more kernels (aka channels, filters)</li>
<li>depth scaling - more layers (ResNet-202 ;))</li>
<li>resolution scaling - higher resolution of input image</li>
</ul>
<blockquote>
<p>The main difficulty of problem 2 is that the optimald,w,rdepend on each other and the values change under differentresource constraints. Due to this difficulty, conventionalmethods mostly scale ConvNets in one of these dimensions</p>
</blockquote>
<p><em>But what if one can compound all 3 scaling methods? -&gt; EfficientNet</em></p>
<p><code>w,d,r</code> are coefficients for scaling network width,depth, and resolution<br>
Paper find those w, d, r coefficients.</p>
<blockquote>
<p>Observation 1 –Scaling up any dimension of network width, depth, or resolution improves accuracy, but the accuracy gain diminishes for bigger models.</p>
</blockquote>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

