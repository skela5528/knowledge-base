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
<li><a href="#vanishingexploding-gradients">Vanishing/Exploding Gradients</a></li>
<li><a href="#optimizers">Optimizers</a></li>
<li><a href="#focal-loss">Focal Loss</a></li>
<li><a href="#recipe-for-training-neural-networks-a.-karpathny">Recipe for Training Neural Networks (A. Karpathny)</a></li>
<li><a href="#evaluation">Evaluation</a>
<ul>
<li><a href="#roc-vs-pr-curves">ROC vs PR curves</a></li>
</ul>
</li>
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
<h2 id="optimizers">Optimizers</h2>
<p><em>Batch gradient descent</em> - over whole data set<br>
<em>Stohastic GD</em> - iterative over 1 sample, usually over n mini-batches<br>
<em>Minibatch gradient descent</em></p>
<p>W<sub>i</sub> = W<sub>i-1</sub> - α  d/dW  J(W)</p>
<p>Exponentially weighted [moving] average of data stream X:<br>
V<sub>t</sub> = b*V<sub>t-1</sub> + (1-b)*X<sub>t</sub><br>
~b=0.9, aprox. averagage over last 1/(1-0.9) = 10 last samples<br>
b=0.98 50- last samples<br>
b=0.5  2-last samples.</p>
<p><em>Momentum (GD with momentum)</em><br>
<a href="https://youtu.be/k8fTYJPd3_I?list=PL9fbVgKf1HGwmWyfsc14iMsBSsluM5bCP">video</a><br>
Instead of gradient make use in exponential average of last gradients (momentum, acceleration)<br>
Usually momentum=0.9 (last 10 batches average)</p>
<p><em>RMSprop</em> Root mean Square <a href="https://youtu.be/_e-LFe_igno?list=PL9fbVgKf1HGwmWyfsc14iMsBSsluM5bCP">video</a><br>
[link] - (<a href="https://towardsdatascience.com/a-look-at-gradient-descent-and-rmsprop-optimizers-f77d483ef08b">https://towardsdatascience.com/a-look-at-gradient-descent-and-rmsprop-optimizers-f77d483ef08b</a>)<br>
Exponential average of squares of gradients<br>
beta=0.999</p>
<p><em>Adam</em> = Momentum  + RMSprop<br>
Adaptive moment estimation<br>
[video] (<a href="https://youtu.be/JXQT_vxqwIs?list=PL9fbVgKf1HGwmWyfsc14iMsBSsluM5bCP">https://youtu.be/JXQT_vxqwIs?list=PL9fbVgKf1HGwmWyfsc14iMsBSsluM5bCP</a>)</p>
<p><em>Learming rate decay</em><br>
Making LR smaller during training<br>
a = 1/ (1 + dr . epoch_n)  . init_a<br>
a = 0.95^(epoch_n) * init_a</p>
<h2 id="focal-loss">Focal Loss</h2>
<p><a href="https://arxiv.org/pdf/1708.02002.pdf">Paper: Focal Loss for Dense Object Detection</a></p>
<p><img src="https://miro.medium.com/max/606/1*qd7u4PjpaKgO-pUX8vi7XQ.png" alt="focal loss"><br>
Main idea: when you predicted p &gt; 0.5 (and GT class is 1) it’s already good enough, no need to penalize in such cases.<br>
But when you predict p=0.1 (and GT class is 1) it’s a hard example, which is a very important to training - so loss much bigger.</p>
<p>FL is down-weighting easy examples and thus focus training on hard negatives.<br>
Weighted CE is not enough. While α balances the importance of positive/negative examples, it does not differentiate between easy/hard examples.</p>
<p>There is a huge imbalance in classes, during one stage detector training. Background examples are much-much-much-much more frequent than predicted objects. It is a source for 2 issues:</p>
<ul>
<li>training is inefficient as most locations are easy negatives that contribute no useful learning signal</li>
<li>en masse, the easy negatives can overwhelm training and lead to degenerate models</li>
</ul>
<p>Other common solutions:</p>
<ul>
<li>hard example mining</li>
<li>weighted CE</li>
</ul>
<p><em>gamma</em>- focusing parameter, authors suggest 2.</p>
<h2 id="recipe-for-training-neural-networks-a.-karpathny">Recipe for Training Neural Networks (A. Karpathny)</h2>
<p><a href="http://karpathy.github.io/2019/04/25/recipe/">link to blog post</a><br>
<strong>Neural net training fails silently</strong> - everything could be correct syntactically and run without errors, but something wrong/buggy inside.</p>
<p><strong>2 main principles</strong> (actually relevant to any system or even any project):</p>
<ul>
<li>start from simple to complex</li>
<li>at every step make hypothesis about results and validate/investigate them</li>
</ul>
<p>Recipe</p>
<ol>
<li>
<p>Inspect your data</p>
</li>
<li>
<p>Training/ evaluation environment. Validate that works fine on a simple model.</p>
<ul>
<li>fix random seed</li>
<li>simplify (no augmentations/ dropouts etc.)</li>
<li>verify loss at init, for example with 2 classes and CE = - log (1/2)</li>
<li>init well<br>
E.g. if you are regressing some values that have a mean of 50 then initialize the final bias to 50. If you have an imbalanced dataset of a ratio 1:10 of positives:negatives, set the bias on your logits such that your network predicts probability of 0.1 at initialization. Setting these correctly will speed up convergence</li>
<li>Monitor metrics other than loss that are human interpretable and checkable</li>
<li>input-indepent baseline<br>
Input zeros shoud be worse than actual data. E.g. does your model learn to extract any information out of the input at all?</li>
<li>overfit one batch -&gt; loss 0</li>
<li>verify decreasing training loss</li>
<li><strong>visualize just before the net</strong> the  correct place to visualize your <strong>data</strong> is immediately before your <code>y_hat = model(x)</code></li>
<li>visualize prediction dynamics on fixed test batch</li>
<li>generalize a special case<br>
people create bugs when they bite off more than they can chew, writing a relatively general functionality from scratch. I like to write a very specific function to what I’m doing right now, get that to work, and then generalize it later making sure that I get the same result. Often this applies to vectorizing code, where I almost always write out the fully loopy version first and only then transform it to vectorized code one loop at a time.</li>
</ul>
</li>
</ol>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
<h2 id="evaluation">Evaluation</h2>
<h3 id="roc-vs-pr-curves">ROC vs PR curves</h3>
<p>ROC curve - Receiver operating characteristic<br>
TP rate (Recall) vs FP rate: how many TP you are pay per FP.</p>
<p>PR (precision - recall) curve.</p>
<ul>
<li>ROC curves are appropriate when the observations are balanced between each class, whereas precision-recall curves are appropriate for imbalanced datasets.</li>
<li>example where PR is more informative: <a href="https://stats.stackexchange.com/questions/7207/roc-vs-precision-and-recall-curves">link</a></li>
<li>a) Result (I) describes a result where 10 of the 20 hits are in the top ten ranks and the remaining 10 hits are then evenly spread out over the first 1500 ranks.</li>
<li>Result (II) describes a result where the 20 hits are evenly spread over the first 500 (out of 2000) ranks.</li>
</ul>
</div>
</body>

</html>

