<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bash Git Ffmpeg etc. cheatsheet</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p><div class="toc">
<ul>
<li>
<ul>
<li><a href="#bash">Bash</a></li>
<li><a href="#video---ffmpeg">Video - ffmpeg</a></li>
<li><a href="#images">Images</a></li>
<li><a href="#python">Python</a></li>
<li><a href="#git">Git</a></li>
<li><a href="#ubuntu">Ubuntu</a></li>
</ul>
</li>
</ul>
</div></p>
<h2 id="bash">Bash</h2>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># count files in cur_dir </span>
<span class="token function">ls</span> -1 <span class="token operator">|</span> <span class="token function">wc</span> -l
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># concat many txt to one</span>
<span class="token function">cat</span> *.txt <span class="token operator">&gt;&gt;</span> <span class="token punctuation">..</span>/all.txt
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># copy 1000 files from cur_dir to target_dir</span>
<span class="token function">find</span> <span class="token keyword">.</span> -maxdepth 1 -type f <span class="token operator">|</span> <span class="token function">head</span> -1000 <span class="token operator">|</span> <span class="token function">xargs</span> <span class="token function">cp</span> -t <span class="token punctuation">..</span>/target_dir
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># copy files from list.txt to target_dir</span>
<span class="token function">xargs</span> -a list.txt <span class="token function">cp</span> -t target_dir  <span class="token comment"># short version</span>
<span class="token function">xargs</span> --arg-file<span class="token operator">=</span>list.txt <span class="token function">cp</span> --target-directory<span class="token operator">=</span>target_dir
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># copy all files from subfolders [Images-&gt; concept1, concept2, ..]</span>
<span class="token function">find</span> <span class="token keyword">.</span> -type f -exec <span class="token function">cp</span> <span class="token string">'{}'</span> <span class="token punctuation">..</span>/all_images/  \<span class="token punctuation">;</span>
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># count files in cur dir </span>
<span class="token function">ls</span> -1 <span class="token operator">|</span> <span class="token function">wc</span> -l
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># rename files </span>
<span class="token function">rename</span> <span class="token string">"s/old_extension/new_extension/"</span> *.txt  <span class="token comment"># extensions in all txt</span>

<span class="token comment"># rename files wich contain "map_roads" in file_name to "map_roads_old" in all subfolders town03_*/*txt</span>
<span class="token function">rename</span> <span class="token string">'s/map_roads/map_roads_old/'</span> town03_*/*txt 
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># delete columns 1 and 8 in csv</span>
<span class="token function">cut</span> -f1,8 --complement origin.csv <span class="token operator">&gt;</span> result.csv
</code></pre>
<h2 id="video---ffmpeg">Video - ffmpeg</h2>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># ffmpeg - create video from frames</span>
ffmpeg -framerate 25 -pattern_type glob -i <span class="token string">'frames/*.png'</span> -c:v libx264 -r 30 -pix_fmt yuv420p <span class="token variable"><span class="token variable">`</span>out_video.mp4<span class="token variable">`</span></span>

<span class="token comment"># short versions</span>
ffmpeg -framerate 10  -i frames/%10d.png out_video.mp4
ffmpeg -framerate 10 -pattern_type glob -i frames/*.png out_video.mp4
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># split video into frames</span>
ffmpeg -i clip1.mp4 -qscale:v 2 frames/frame%04d.jpg
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># merge two video clips into one, placing them side to side</span>
ffmpeg -i left.mp4 -i right.mp4 -filter_complex hstack output.mp4
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># cut start from sec 21.2 and keep 9 sec</span>
ffmpeg -ss 21.2 -i drive_0029_CA.mp4 -ss 21.2 -i drive_0029_CV.mp4 -filter_complex  hstack -t 9 out.mp4
</code></pre>
<h2 id="images">Images</h2>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># merge images verticaly or horizontaly</span>
convert -append *.png out.png
convert +append *.png out.png
</code></pre>
<h2 id="python">Python</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># datetime</span>
datetime<span class="token punctuation">.</span>datetime<span class="token punctuation">.</span>now<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>strftime<span class="token punctuation">(</span><span class="token string">"%b%d_%H%M%S"</span><span class="token punctuation">)</span>
</code></pre>
<h2 id="git">Git</h2>
<pre><code># merge from master to my branch
1 - commit/stage all uncomited changes
2 - min the differenec with master
3 - update master -&gt; co master; pull
4 - co my_branch; merge master
</code></pre>
<pre><code># undo n local commits
git reset --soft HEAD~n  # will erase work!!! stash before
</code></pre>
<h2 id="ubuntu">Ubuntu</h2>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># restart network manager</span>
<span class="token function">sudo</span> <span class="token function">service</span> network-manager restart 
</code></pre>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token comment"># restart nautilius</span>
<span class="token function">ps</span> awx <span class="token operator">|</span> <span class="token function">grep</span> nautilus  <span class="token comment"># print running nautilus process</span>
<span class="token function">sudo</span> <span class="token function">kill</span> -TERM <span class="token operator">&lt;</span>id<span class="token operator">&gt;</span>    <span class="token comment"># kill them</span>
</code></pre>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
</div>
</body>

</html>

