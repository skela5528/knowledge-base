<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basics</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li>
<ul>
<li><a href="#transfer-learning">Transfer Learning</a></li>
<li><a href="#batch-normalization">Batch Normalization</a></li>
</ul>
</li>
</ul>
</div></p>
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
<img src="https://miro.medium.com/max/405/1*Hiq-rLFGDpESpr8QNsJ1jg.png" alt="BN transform"></p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

