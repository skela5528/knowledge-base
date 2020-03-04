<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basics</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li>
<ul>
<li><a href="#transfer-learning">Transfer Learning</a></li>
<li><a href="#batch-normalization">Batch Normalization</a></li>
<li><a href="#vanishingexploding-gradients">Vanishing/Exploding Gradients</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <p>[TOC]</p>
<h2 id="transfer-learning">Transfer Learning</h2>
<p><a href="https://pytorch.org/tutorials/advanced/neural_style_tutorial.html">Pytorch tutorial</a><br>
content image<br>
style image<br>
input image - in the end = content + style</p>
<p><code>content_dist</code> - measure how contents are similar<br>
content_loss = MSELoss between features maps</p>
<p><code>style_dist</code> - measure how styles are similar<br>
gram_matrix<br>
MSE between gram_matrix ??</p>
<p>Optimization:<br>
Learn <code>input image</code>  (initialized with <code>content image</code>)<br>
<code>optimizer = optim.LBFGS([input_img.requires_grad_()])</code></p>
<h2 id="batch-normalization">Batch Normalization</h2>
<p>Original paper: <a href="https://arxiv.org/abs/1502.03167">Batch Normalization: Accelerating … </a><br>
Why it works  <a href="https://www.youtube.com/watch?v=nUUqwaxLnWs">video from A. NG</a></p>
<p><strong>What</strong>: normalize layer inputs (activations from prev layer, feature map from previous layer)<br>
<strong>Why</strong>:  normalization of features (input to 1st layer) is helps to the learning, why not to do same for all layers<br>
<strong>Effects</strong>:</p>
<ul>
<li>faster training</li>
<li>reduce covariance shift (WDF?)<br>
Net trained only on black cats will have trouble to work on colored cats.</li>
<li>each layer learn independently ?</li>
<li>allow to use higher LR</li>
<li>reduce averfitting - kind of regularization</li>
</ul>
<p><strong>How</strong>:<br>
<img src="https://miro.medium.com/max/405/1*Hiq-rLFGDpESpr8QNsJ1jg.png" alt="BN transform"><br>
<a href="https://www.youtube.com/watch?v=tNIpEZLv_eg&amp;list=PLkDaE6sCZn6Hn0vK8co82zjQtt3T2Nkqc&amp;index=27">A. Ng - Normalizing Activations in a Network (C2W3L04) </a><br>
<em>Before or after activation</em> - usually BN applies before</p>
<p>Why we need extra params <em>beta</em> and <em>gama</em> ?<br>
<a href="https://youtu.be/tNIpEZLv_eg?list=PLkDaE6sCZn6Hn0vK8co82zjQtt3T2Nkqc&amp;t=406">https://youtu.be/tNIpEZLv_eg?list=PLkDaE6sCZn6Hn0vK8co82zjQtt3T2Nkqc&amp;t=406</a><br>
We control the mean and variance of the layer to something that is best for the net!</p>
<p><em>Regularization effect</em></p>
<ul>
<li>using mean and variance of the batch (sample)</li>
<li>estimation of mean an variance are noisy</li>
<li>make effect of regularization</li>
<li>using bigger batch size reduce the effect!!</li>
</ul>
<p><em>BN during test</em></p>
<ul>
<li>in test time we don’t have batches, or have batches of other size and don’t want to have different results depending on batch size!!</li>
<li>during training estimate mean and variance based on all batches. usually with moving average (more attention to last batches)</li>
<li></li>
</ul>
<h2 id="vanishingexploding-gradients">Vanishing/Exploding Gradients</h2>
<p><a href="https://www.youtube.com/watch?v=qhXZsFVxGKo">andrew ng video</a></p>
<p>Derivatives can be very-very small (vanishing) or big(exploding)</p>
<p>Now when we do Back-propagation i.e moving backward in the Network and calculating gradients of loss(Error) with respect to the weights , the gradients tends to get smaller  and smaller as we keep on moving backward in the Network.  All this to many multiplications.<br>
This means that the neurons in the Earlier  layers learn very slowly as compared to the neurons in the later layers in the Hierarchy. The Earlier layers in the network are slowest to train.</p>
<p>Solutions</p>
<ul>
<li>residual net</li>
<li>ReLU</li>
<li>optimization not bases on gradients, e.g. genetic algorithms</li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

    </div>
  </div>
</body>

</html>
