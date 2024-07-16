---
draft: false
date: 2024-07-16
categories:
  - Deep Learning
  - Project
authors:
  - junho
---

<!DOCTYPE html><html><head>
      <title>Implement-Cat-vs.-Non-cat-Classifier-on-EKS</title>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      
      <link rel="stylesheet" href="file:///c:\Users\user\.cursor\extensions\shd101wyy.markdown-preview-enhanced-0.8.13\crossnote\dependencies\katex\katex.min.css">
      
      
      
      
      <style>
      code[class*=language-],pre[class*=language-]{color:#333;background:0 0;font-family:Consolas,"Liberation Mono",Menlo,Courier,monospace;text-align:left;white-space:pre;word-spacing:normal;word-break:normal;word-wrap:normal;line-height:1.4;-moz-tab-size:8;-o-tab-size:8;tab-size:8;-webkit-hyphens:none;-moz-hyphens:none;-ms-hyphens:none;hyphens:none}pre[class*=language-]{padding:.8em;overflow:auto;border-radius:3px;background:#f5f5f5}:not(pre)>code[class*=language-]{padding:.1em;border-radius:.3em;white-space:normal;background:#f5f5f5}.token.blockquote,.token.comment{color:#969896}.token.cdata{color:#183691}.token.doctype,.token.macro.property,.token.punctuation,.token.variable{color:#333}.token.builtin,.token.important,.token.keyword,.token.operator,.token.rule{color:#a71d5d}.token.attr-value,.token.regex,.token.string,.token.url{color:#183691}.token.atrule,.token.boolean,.token.code,.token.command,.token.constant,.token.entity,.token.number,.token.property,.token.symbol{color:#0086b3}.token.prolog,.token.selector,.token.tag{color:#63a35c}.token.attr-name,.token.class,.token.class-name,.token.function,.token.id,.token.namespace,.token.pseudo-class,.token.pseudo-element,.token.url-reference .token.variable{color:#795da3}.token.entity{cursor:help}.token.title,.token.title .token.punctuation{font-weight:700;color:#1d3e81}.token.list{color:#ed6a43}.token.inserted{background-color:#eaffea;color:#55a532}.token.deleted{background-color:#ffecec;color:#bd2c00}.token.bold{font-weight:700}.token.italic{font-style:italic}.language-json .token.property{color:#183691}.language-markup .token.tag .token.punctuation{color:#333}.language-css .token.function,code.language-css{color:#0086b3}.language-yaml .token.atrule{color:#63a35c}code.language-yaml{color:#183691}.language-ruby .token.function{color:#333}.language-markdown .token.url{color:#795da3}.language-makefile .token.symbol{color:#795da3}.language-makefile .token.variable{color:#183691}.language-makefile .token.builtin{color:#0086b3}.language-bash .token.keyword{color:#0086b3}pre[data-line]{position:relative;padding:1em 0 1em 3em}pre[data-line] .line-highlight-wrapper{position:absolute;top:0;left:0;background-color:transparent;display:block;width:100%}pre[data-line] .line-highlight{position:absolute;left:0;right:0;padding:inherit 0;margin-top:1em;background:hsla(24,20%,50%,.08);background:linear-gradient(to right,hsla(24,20%,50%,.1) 70%,hsla(24,20%,50%,0));pointer-events:none;line-height:inherit;white-space:pre}pre[data-line] .line-highlight:before,pre[data-line] .line-highlight[data-end]:after{content:attr(data-start);position:absolute;top:.4em;left:.6em;min-width:1em;padding:0 .5em;background-color:hsla(24,20%,50%,.4);color:#f4f1ef;font:bold 65%/1.5 sans-serif;text-align:center;vertical-align:.3em;border-radius:999px;text-shadow:none;box-shadow:0 1px #fff}pre[data-line] .line-highlight[data-end]:after{content:attr(data-end);top:auto;bottom:.4em}html body{font-family:'Helvetica Neue',Helvetica,'Segoe UI',Arial,freesans,sans-serif;font-size:16px;line-height:1.6;color:#333;background-color:#fff;overflow:initial;box-sizing:border-box;word-wrap:break-word}html body>:first-child{margin-top:0}html body h1,html body h2,html body h3,html body h4,html body h5,html body h6{line-height:1.2;margin-top:1em;margin-bottom:16px;color:#000}html body h1{font-size:2.25em;font-weight:300;padding-bottom:.3em}html body h2{font-size:1.75em;font-weight:400;padding-bottom:.3em}html body h3{font-size:1.5em;font-weight:500}html body h4{font-size:1.25em;font-weight:600}html body h5{font-size:1.1em;font-weight:600}html body h6{font-size:1em;font-weight:600}html body h1,html body h2,html body h3,html body h4,html body h5{font-weight:600}html body h5{font-size:1em}html body h6{color:#5c5c5c}html body strong{color:#000}html body del{color:#5c5c5c}html body a:not([href]){color:inherit;text-decoration:none}html body a{color:#08c;text-decoration:none}html body a:hover{color:#00a3f5;text-decoration:none}html body img{max-width:100%}html body>p{margin-top:0;margin-bottom:16px;word-wrap:break-word}html body>ol,html body>ul{margin-bottom:16px}html body ol,html body ul{padding-left:2em}html body ol.no-list,html body ul.no-list{padding:0;list-style-type:none}html body ol ol,html body ol ul,html body ul ol,html body ul ul{margin-top:0;margin-bottom:0}html body li{margin-bottom:0}html body li.task-list-item{list-style:none}html body li>p{margin-top:0;margin-bottom:0}html body .task-list-item-checkbox{margin:0 .2em .25em -1.8em;vertical-align:middle}html body .task-list-item-checkbox:hover{cursor:pointer}html body blockquote{margin:16px 0;font-size:inherit;padding:0 15px;color:#5c5c5c;background-color:#f0f0f0;border-left:4px solid #d6d6d6}html body blockquote>:first-child{margin-top:0}html body blockquote>:last-child{margin-bottom:0}html body hr{height:4px;margin:32px 0;background-color:#d6d6d6;border:0 none}html body table{margin:10px 0 15px 0;border-collapse:collapse;border-spacing:0;display:block;width:100%;overflow:auto;word-break:normal;word-break:keep-all}html body table th{font-weight:700;color:#000}html body table td,html body table th{border:1px solid #d6d6d6;padding:6px 13px}html body dl{padding:0}html body dl dt{padding:0;margin-top:16px;font-size:1em;font-style:italic;font-weight:700}html body dl dd{padding:0 16px;margin-bottom:16px}html body code{font-family:Menlo,Monaco,Consolas,'Courier New',monospace;font-size:.85em;color:#000;background-color:#f0f0f0;border-radius:3px;padding:.2em 0}html body code::after,html body code::before{letter-spacing:-.2em;content:'\00a0'}html body pre>code{padding:0;margin:0;word-break:normal;white-space:pre;background:0 0;border:0}html body .highlight{margin-bottom:16px}html body .highlight pre,html body pre{padding:1em;overflow:auto;line-height:1.45;border:#d6d6d6;border-radius:3px}html body .highlight pre{margin-bottom:0;word-break:normal}html body pre code,html body pre tt{display:inline;max-width:initial;padding:0;margin:0;overflow:initial;line-height:inherit;word-wrap:normal;background-color:transparent;border:0}html body pre code:after,html body pre code:before,html body pre tt:after,html body pre tt:before{content:normal}html body blockquote,html body dl,html body ol,html body p,html body pre,html body ul{margin-top:0;margin-bottom:16px}html body kbd{color:#000;border:1px solid #d6d6d6;border-bottom:2px solid #c7c7c7;padding:2px 4px;background-color:#f0f0f0;border-radius:3px}@media print{html body{background-color:#fff}html body h1,html body h2,html body h3,html body h4,html body h5,html body h6{color:#000;page-break-after:avoid}html body blockquote{color:#5c5c5c}html body pre{page-break-inside:avoid}html body table{display:table}html body img{display:block;max-width:100%;max-height:100%}html body code,html body pre{word-wrap:break-word;white-space:pre}}.markdown-preview{width:100%;height:100%;box-sizing:border-box}.markdown-preview ul{list-style:disc}.markdown-preview ul ul{list-style:circle}.markdown-preview ul ul ul{list-style:square}.markdown-preview ol{list-style:decimal}.markdown-preview ol ol,.markdown-preview ul ol{list-style-type:lower-roman}.markdown-preview ol ol ol,.markdown-preview ol ul ol,.markdown-preview ul ol ol,.markdown-preview ul ul ol{list-style-type:lower-alpha}.markdown-preview .newpage,.markdown-preview .pagebreak{page-break-before:always}.markdown-preview pre.line-numbers{position:relative;padding-left:3.8em;counter-reset:linenumber}.markdown-preview pre.line-numbers>code{position:relative}.markdown-preview pre.line-numbers .line-numbers-rows{position:absolute;pointer-events:none;top:1em;font-size:100%;left:0;width:3em;letter-spacing:-1px;border-right:1px solid #999;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}.markdown-preview pre.line-numbers .line-numbers-rows>span{pointer-events:none;display:block;counter-increment:linenumber}.markdown-preview pre.line-numbers .line-numbers-rows>span:before{content:counter(linenumber);color:#999;display:block;padding-right:.8em;text-align:right}.markdown-preview .mathjax-exps .MathJax_Display{text-align:center!important}.markdown-preview:not([data-for=preview]) .code-chunk .code-chunk-btn-group{display:none}.markdown-preview:not([data-for=preview]) .code-chunk .status{display:none}.markdown-preview:not([data-for=preview]) .code-chunk .output-div{margin-bottom:16px}.markdown-preview .md-toc{padding:0}.markdown-preview .md-toc .md-toc-link-wrapper .md-toc-link{display:inline;padding:.25rem 0}.markdown-preview .md-toc .md-toc-link-wrapper .md-toc-link div,.markdown-preview .md-toc .md-toc-link-wrapper .md-toc-link p{display:inline}.markdown-preview .md-toc .md-toc-link-wrapper.highlighted .md-toc-link{font-weight:800}.scrollbar-style::-webkit-scrollbar{width:8px}.scrollbar-style::-webkit-scrollbar-track{border-radius:10px;background-color:transparent}.scrollbar-style::-webkit-scrollbar-thumb{border-radius:5px;background-color:rgba(150,150,150,.66);border:4px solid rgba(150,150,150,.66);background-clip:content-box}html body[for=html-export]:not([data-presentation-mode]){position:relative;width:100%;height:100%;top:0;left:0;margin:0;padding:0;overflow:auto}html body[for=html-export]:not([data-presentation-mode]) .markdown-preview{position:relative;top:0;min-height:100vh}@media screen and (min-width:914px){html body[for=html-export]:not([data-presentation-mode]) .markdown-preview{padding:2em calc(50% - 457px + 2em)}}@media screen and (max-width:914px){html body[for=html-export]:not([data-presentation-mode]) .markdown-preview{padding:2em}}@media screen and (max-width:450px){html body[for=html-export]:not([data-presentation-mode]) .markdown-preview{font-size:14px!important;padding:1em}}@media print{html body[for=html-export]:not([data-presentation-mode]) #sidebar-toc-btn{display:none}}html body[for=html-export]:not([data-presentation-mode]) #sidebar-toc-btn{position:fixed;bottom:8px;left:8px;font-size:28px;cursor:pointer;color:inherit;z-index:99;width:32px;text-align:center;opacity:.4}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] #sidebar-toc-btn{opacity:1}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc{position:fixed;top:0;left:0;width:300px;height:100%;padding:32px 0 48px 0;font-size:14px;box-shadow:0 0 4px rgba(150,150,150,.33);box-sizing:border-box;overflow:auto;background-color:inherit}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc::-webkit-scrollbar{width:8px}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc::-webkit-scrollbar-track{border-radius:10px;background-color:transparent}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc::-webkit-scrollbar-thumb{border-radius:5px;background-color:rgba(150,150,150,.66);border:4px solid rgba(150,150,150,.66);background-clip:content-box}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc a{text-decoration:none}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc .md-toc{padding:0 16px}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc .md-toc .md-toc-link-wrapper .md-toc-link{display:inline;padding:.25rem 0}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc .md-toc .md-toc-link-wrapper .md-toc-link div,html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc .md-toc .md-toc-link-wrapper .md-toc-link p{display:inline}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .md-sidebar-toc .md-toc .md-toc-link-wrapper.highlighted .md-toc-link{font-weight:800}html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .markdown-preview{left:300px;width:calc(100% - 300px);padding:2em calc(50% - 457px - 300px / 2);margin:0;box-sizing:border-box}@media screen and (max-width:1274px){html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .markdown-preview{padding:2em}}@media screen and (max-width:450px){html body[for=html-export]:not([data-presentation-mode])[html-show-sidebar-toc] .markdown-preview{width:100%}}html body[for=html-export]:not([data-presentation-mode]):not([html-show-sidebar-toc]) .markdown-preview{left:50%;transform:translateX(-50%)}html body[for=html-export]:not([data-presentation-mode]):not([html-show-sidebar-toc]) .md-sidebar-toc{display:none}
/* Please visit the URL below for more information: */
/*   https://shd101wyy.github.io/markdown-preview-enhanced/#/customize-css */

      </style>
      <!-- The content below will be included at the end of the <head> element. --><script type="text/javascript">
  document.addEventListener("DOMContentLoaded", function () {
    // your code here
  });
</script></head><body for="html-export">
    
    
      <div class="crossnote markdown-preview  ">
      
<h2 id="system-overview">System overview </h2>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/DwRBYMd.png" alt="EKS architecture" width="750"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em><b>NLB</b> with Nginx Ingress Controller</em></td>
</tr>
</tbody>
</table>

<!-- more -->

<p>There are several ways to configure external access into the application, which I will be explaining in details.</p>
<h2 id="demo">Demo </h2>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/VbKBWdO.gif" alt="demo" width="650"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>application demo</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/tbG85hA.png" alt="demo" width="600"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>applications diagram</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li><a href="https://github.com/jnuho/simpledl" target="_blank">🔗 Github Repository</a></li>
</ul>
<ul>
<li><a href="#motivation"><code>Motivation</code></a></li>
<li><a href="#why-kubernetes"><code>Why Kuberenetes?</code></a>
<ul>
<li><a href="#scalability"><code>Scalability</code></a></li>
<li><a href="#load-balancing"><code>Load Balancing</code></a>
<ul>
<li><a href="#nginx-ingress-controller"><code>Nginx Ingress Controller</code></a></li>
<li><a href="#aws-load-balancer-controller"><code>AWS Load Balancer Controller</code></a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#skill-used"><code>Skill Used</code></a></li>
<li><a href="#microservices"><code>Microservices</code></a>
<ul>
<li><a href="#frontend-nginx"><code>1.Frontend - Nginx</code></a></li>
<li><a href="#backend-golang-web-server"><code>2. Backend - Golang</code></a></li>
<li><a href="#backend-python-web-server"><code>3. Backend - Python</code></a></li>
</ul>
</li>
<li><a href="#dockerize"><code>Dockerize</code></a></li>
<li><a href="#iac"><code>IaC</code></a>
<ul>
<li><a href="#terraform"><code>Terraform</code></a></li>
<li><a href="#helm"><code>Helm</code></a></li>
</ul>
</li>
<li><a href="#kubernetes-for-mlops"><code>Kubernetes for MLOps</code></a></li>
<li><a href="#appendix"><code>Appendix</code></a></li>
</ul>
<h2 id="motivation">Motivation </h2>
<p>My initial goal was to <strong>revisit</strong> the <a href="#skills-used"><code>skills</code></a> I've acquired during my work experiences.</p>
<p>I have a <strong>great interest</strong> in deep learning. So I decided to implement a Cat vs. Non-cat image classifier for URL images from user inputs. The prediction model uses the following steps to train a Neural Network:</p>
<ul>
<li>Forward Propagation
<ul>
<li><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mi>a</mi><mrow><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo></mrow></msup><mo>=</mo><mi>R</mi><mi>e</mi><mi>L</mi><mi>U</mi><mo stretchy="false">(</mo><msup><mi>z</mi><mrow><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo></mrow></msup><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">a^{[l]}  = ReLU(z^{[l]})</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.888em;"></span><span class="mord"><span class="mord mathnormal">a</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.888em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mopen mtight">[</span><span class="mord mathnormal mtight" style="margin-right:0.01968em;">l</span><span class="mclose mtight">]</span></span></span></span></span></span></span></span></span><span class="mspace" style="margin-right:0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right:0.2778em;"></span></span><span class="base"><span class="strut" style="height:1.138em;vertical-align:-0.25em;"></span><span class="mord mathnormal" style="margin-right:0.00773em;">R</span><span class="mord mathnormal">e</span><span class="mord mathnormal" style="margin-right:0.10903em;">LU</span><span class="mopen">(</span><span class="mord"><span class="mord mathnormal" style="margin-right:0.04398em;">z</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.888em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mopen mtight">[</span><span class="mord mathnormal mtight" style="margin-right:0.01968em;">l</span><span class="mclose mtight">]</span></span></span></span></span></span></span></span></span><span class="mclose">)</span></span></span></span> for <span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>=</mo><mn>1</mn><mo separator="true">,</mo><mi mathvariant="normal">.</mi><mi mathvariant="normal">.</mi><mi mathvariant="normal">.</mi><mi>L</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">l=1,...L-1</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.6944em;"></span><span class="mord mathnormal" style="margin-right:0.01968em;">l</span><span class="mspace" style="margin-right:0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right:0.2778em;"></span></span><span class="base"><span class="strut" style="height:0.8778em;vertical-align:-0.1944em;"></span><span class="mord">1</span><span class="mpunct">,</span><span class="mspace" style="margin-right:0.1667em;"></span><span class="mord">...</span><span class="mord mathnormal">L</span><span class="mspace" style="margin-right:0.2222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right:0.2222em;"></span></span><span class="base"><span class="strut" style="height:0.6444em;"></span><span class="mord">1</span></span></span></span></li>
<li><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mi>a</mi><mrow><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo></mrow></msup><mo>=</mo><mi>σ</mi><mo stretchy="false">(</mo><msup><mi>z</mi><mrow><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo></mrow></msup><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">a^{[l]}  = \sigma(z^{[l]})</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.888em;"></span><span class="mord"><span class="mord mathnormal">a</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.888em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mopen mtight">[</span><span class="mord mathnormal mtight" style="margin-right:0.01968em;">l</span><span class="mclose mtight">]</span></span></span></span></span></span></span></span></span><span class="mspace" style="margin-right:0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right:0.2778em;"></span></span><span class="base"><span class="strut" style="height:1.138em;vertical-align:-0.25em;"></span><span class="mord mathnormal" style="margin-right:0.03588em;">σ</span><span class="mopen">(</span><span class="mord"><span class="mord mathnormal" style="margin-right:0.04398em;">z</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.888em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mopen mtight">[</span><span class="mord mathnormal mtight" style="margin-right:0.01968em;">l</span><span class="mclose mtight">]</span></span></span></span></span></span></span></span></span><span class="mclose">)</span></span></span></span> for <span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>=</mo><mi>L</mi></mrow><annotation encoding="application/x-tex">l=L</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.6944em;"></span><span class="mord mathnormal" style="margin-right:0.01968em;">l</span><span class="mspace" style="margin-right:0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right:0.2778em;"></span></span><span class="base"><span class="strut" style="height:0.6833em;"></span><span class="mord mathnormal">L</span></span></span></span></li>
</ul>
</li>
<li>Compute cost</li>
<li>Backward Propagation</li>
<li>Gradient descent (Update parameters -  <span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi></mrow><annotation encoding="application/x-tex">\omega</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.4306em;"></span><span class="mord mathnormal" style="margin-right:0.03588em;">ω</span></span></span></span>, <span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>b</mi></mrow><annotation encoding="application/x-tex">b</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height:0.6944em;"></span><span class="mord mathnormal">b</span></span></span></span>)</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*iNPHcCxIvcm7RwkRaMTx1g.jpeg" alt="gradient descent" width="400"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>gradient descent</em></td>
</tr>
</tbody>
</table>
<p>I tried to focus on <strong><code>Kubernetes</code> implementation</strong>, which I consider myself to be more competent, especially configuring <code>external access</code> into the application in different Kubernetes environments - Cloud(EKS), On-premise (microk8s, minikube, docker-compoise)</p>
<pre data-role="codeBlock" data-info="python" class="language-python python"><code><span class="token keyword keyword-def">def</span> <span class="token function">L_layer_model</span><span class="token punctuation">(</span>
        parameters <span class="token operator">=</span> init_params<span class="token punctuation">(</span>layers_dims<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        X<span class="token punctuation">:</span> np<span class="token punctuation">.</span>ndarray<span class="token punctuation">,</span>
        Y<span class="token punctuation">:</span> np<span class="token punctuation">.</span>ndarray<span class="token punctuation">,</span>
        layers_dims<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        learning_rate<span class="token punctuation">:</span> <span class="token builtin">float</span> <span class="token operator">=</span> <span class="token number">0.0075</span><span class="token punctuation">,</span>
        num_iterations<span class="token punctuation">:</span> <span class="token builtin">int</span> <span class="token operator">=</span> <span class="token number">2500</span><span class="token punctuation">)</span>
    <span class="token comment"># RETURNS Updated `parameters` and `costs`</span>
    <span class="token operator">-</span><span class="token operator">&gt;</span> Tuple<span class="token punctuation">[</span><span class="token builtin">dict</span><span class="token punctuation">,</span> List<span class="token punctuation">[</span><span class="token builtin">float</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
</code></pre><ul>
<li><code>TODO</code>:
<ul>
<li>I've yet to explore Pytorch implementation to classify Cat vs. Non-cat.</li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="why-kubernetes">Why Kubernetes? </h2>
<ul>
<li>While docker-compose <img src="https://i0.wp.com/codeblog.dotsandbrackets.com/wp-content/uploads/2016/10/compose-logo.jpg?w=28"> can be a reasonable choice for local development, it falls short in terms of <code>scalability</code>, <code>load balancing</code>, <code>IaC support</code>(Terraform, Helm), and seamless <code>cloud-native integration</code>.</li>
<li>Kubernetes offers a rich set of APIs to address these challenges.</li>
<li>For local development, I chose <img src="https://blog.radwell.codes/wp-content/uploads/2021/05/minikube-logo-full.png" alt="minikube logo" width="75"> over docker-compose to align with Kuberentes best practices. This <code>consistency</code> ensures a smoother transition to <img src="https://diagrams.mingrammer.com/img/resources/aws/compute/elastic-kubernetes-service.png" alt="EKS logo" width="28"> EKS production.</li>
</ul>
<table>
<thead>
<tr>
<th></th>
<th>docker-compose</th>
<th>Kubernetes</th>
</tr>
</thead>
<tbody>
<tr>
<td>Scalability</td>
<td>Limited to a Single host</td>
<td>Multi-node scaling</td>
</tr>
<tr>
<td>Load Balancing</td>
<td>Requires manual setup (e.g., HAProxy)</td>
<td>Support <a href="#load-balancing">Load Balancing</a> in various ways</td>
</tr>
<tr>
<td>IaC Support</td>
<td>Resticted to docker compose cli</td>
<td>Terraform, Helm for fast and reliable resource provisioning (<em>&lt; ~15 minutes</em>)</td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/qqDsoa2.png" alt="dc vs k8s" width="650"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>docker-compose vs. Kubernetes</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="scalability">Scalability </h3>
<p>Kubernetes offers orchestration of containerized applications across a cluster of nodes, ensuring scalability and high availability.</p>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/KxETYaG.png" alt="ingress" width="750"></th>
</tr>
</thead>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/rvtBRlL.png" alt="metric-server" width="650"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>HPA and metric-server</em></td>
</tr>
</tbody>
</table>
<ul>
<li>
<p><code>Horizonal Pod Autoscaling</code> control loop checks <code>CPU</code> and <code>Memory</code> usage via api-server's metric api  and scales accordingly.</p>
<ul>
<li>Install <code>metric-server</code> on the worker nodes (kube-system namespace) with helm!
<ul>
<li>scrapes metrics from kublet and publish to <code>metrics.k8s.io/v1beta</code> Kubernetes api → consumed by HPA!</li>
</ul>
</li>
<li>deployment.yaml: <code>spec.template.spec.containers[i].resources</code> must be specified.</li>
<li>deployment.yaml: <code>spec.replicas</code> is to be omitted.</li>
</ul>
</li>
<li>
<p>hpa.yaml</p>
<ul>
<li><code>spec.metrics[i].resource</code> to specify CPU and Memory threshold</li>
<li><code>spec.scaleTargetRef.name</code> to identify the target</li>
<li>in order to enable HPA to work on another metrics, you need to define addtional component.</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> autoscaling/v2
<span class="token key atrule">kind</span><span class="token punctuation">:</span> HorizontalPodAutoscaler
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
  <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>hpa
<span class="token key atrule">spec</span><span class="token punctuation">:</span>
  <span class="token key atrule">scaleTargetRef</span><span class="token punctuation">:</span>
    <span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> apps/v1
    <span class="token key atrule">kind</span><span class="token punctuation">:</span> Deployment
    <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>deployment
  <span class="token key atrule">minReplicas</span><span class="token punctuation">:</span> <span class="token number">1</span>
  <span class="token key atrule">maxReplicas</span><span class="token punctuation">:</span> <span class="token number">1</span>
  <span class="token key atrule">metrics</span><span class="token punctuation">:</span>
  <span class="token punctuation">-</span> <span class="token key atrule">type</span><span class="token punctuation">:</span> Resource
    <span class="token key atrule">resource</span><span class="token punctuation">:</span>
      <span class="token key atrule">name</span><span class="token punctuation">:</span> cpu
      <span class="token key atrule">target</span><span class="token punctuation">:</span>
        <span class="token key atrule">type</span><span class="token punctuation">:</span> Utilization
        <span class="token key atrule">averageUtilization</span><span class="token punctuation">:</span> <span class="token number">80</span>
  <span class="token punctuation">-</span> <span class="token key atrule">type</span><span class="token punctuation">:</span> Resource
    <span class="token key atrule">resource</span><span class="token punctuation">:</span>
      <span class="token key atrule">name</span><span class="token punctuation">:</span> memory
      <span class="token key atrule">target</span><span class="token punctuation">:</span>
        <span class="token key atrule">type</span><span class="token punctuation">:</span> Utilization
        <span class="token key atrule">averageUtilization</span><span class="token punctuation">:</span> <span class="token number">70</span>
</code></pre><ul>
<li>deployment.yaml
<ul>
<li>Omit <code>spec.replica: xx</code> in order to use HPA functionality.</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code>          <span class="token key atrule">resources</span><span class="token punctuation">:</span>
            <span class="token key atrule">requests</span><span class="token punctuation">:</span>
              <span class="token key atrule">cpu</span><span class="token punctuation">:</span> 100m
              <span class="token key atrule">memory</span><span class="token punctuation">:</span> 256Mi
            <span class="token key atrule">limits</span><span class="token punctuation">:</span>
              <span class="token key atrule">cpu</span><span class="token punctuation">:</span> 100m
              <span class="token key atrule">memory</span><span class="token punctuation">:</span> 256Mi
</code></pre><table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/7RHqdu8.png" alt="hpa" width="720"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>metric-server</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/1EiedmA.png" alt="hpa" width="720"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>HPA monitoring</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="load-balancing">Load Balancing </h3>
<p>Kubernetes provides native support for load balancing and traffic routing through <code>Ingress</code>, <code>Ingress Controller</code>, and <code>AWS Load Balancer Controller</code>. I will be exploring two ways for exposing the Kuberentes application to the outside world:</p>
<ul>
<li><a href="#nginx-ingress-controller"><code>Nginx Ingress Controller</code></a></li>
<li><a href="#aws-load-balancer-controller"><code>AWS Load Balancer Controller</code></a></li>
</ul>
<h4 id="nginx-ingress-controller">Nginx Ingress Controller </h4>
<p>Nginx Ingress Controller is a 3rd party implementation of Ingress controller.</p>
<ul>
<li>Install with Helm or kubectl. (in <code>ingress</code> namespace)</li>
<li>it provisions <code>NLB</code> upon installation.
<ul>
<li>the Service of type LoadBalancer triggers the NLB creation during installation</li>
</ul>
</li>
<li>it monitors <code>Ingress</code> resource:
<ul>
<li>for each Ingress being created, it is converted to Nignx native <code>Lua</code> configuration and routes to the target service! The controller acts as a proxy and redirects traffic into services.</li>
</ul>
</li>
<li>Monitoring tools like <code>Prometheus</code> <img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Prometheus_software_logo.svg" width="28"> can scrape metrics (traffic, latency, errors for all Ingresses) from the nginx ingress controller pod without implementing anything on the Application side!  <!-- - must specify `ingressClassName` as the name of Ingress Nginx controller. (helm installing using Terraform, specify same name as this)
  - When you create an Ingress resource with the specified ingressClassName, the NGINX Ingress Controller reads the Ingress rules and updates its configuration accordingly. -->
  <!-- - Traffic flow: `AWS NLB ->  Nginx ingress controller ->(Ingres Rule) Service -> Pod` -->
  <!-- - All the Ingresses use the same Load Balancer! COST and MAINTENANCE saved! -->
</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/7QR1Wpn.png" alt="nginx-ingress-controller" width="480"></th>
</tr>
</thead>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/DwRBYMd.png" alt="EKS architecture" width="750"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em><b>NLB</b> with Nginx Ingress Controller</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://kubernetes.io/docs/images/ingress.svg" alt="ingress" width="520"></th>
</tr>
</thead>
</table>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>kubectl get ingressclass <span class="token parameter variable">-A</span>
<span class="token comment"># NAME            CONTROLLER            PARAMETERS  AGE</span>
<span class="token comment"># alb             ingress.k8s.aws/alb   &lt;none&gt;      20m</span>
<span class="token comment"># external-nginx  k8s.io/ingress-nginx  &lt;none&gt;      20m</span>
</code></pre><table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/pSGCLP9.png" alt="ingress" width="720"></th>
</tr>
</thead>
</table>
<ul>
<li>Baremetal (To-be-tested)
<ul>
<li><a href="https://kubernetes.github.io/ingress-nginx/deploy/baremetal/">https://kubernetes.github.io/ingress-nginx/deploy/baremetal/</a></li>
<li>A pure software solution: MetalLB</li>
<li>Over a NodePort Service</li>
</ul>
</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://kubernetes.github.io/ingress-nginx/images/baremetal/baremetal_overview.jpg" alt="ingress" width="500"></th>
</tr>
</thead>
</table>
<h4 id="aws-load-balancer-controller">AWS Load Balancer Controller </h4>
<ul>
<li>The controller (in <code>kube-system</code> namespace) watches for Kubernetes Ingress or Service resources. In response, it creates the appropriate AWS Elastic Load Balancing resources.
<ul>
<li>The LBC provisions <code>ALB</code> when you create an <em>Ingress</em>.</li>
<li>The LBC provisions <code>NLB</code> when you create a <em>Service</em> of type <em>LoadBalancer</em>.</li>
<li>ALB is slower than NLB and more expensive.</li>
</ul>
</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/UaF1vHK.png" alt="aws-lbc" width="520"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>AWS Load Balancer Controller - L4 or L7</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/tg4GAzA.png" alt="EKS architecture" width="750"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em><b>ALB</b> with AWS Load Balancer Controller</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="skills-used">Skills used </h2>
<ul>
<li><code>Kubernetes</code>
<ul>
<li>AWS: EKS cluster with 3 worker nodes. Terraform to deploy EKS and AWS Load Balancer Controller and Ingress for exposing the app.</li>
<li>Local: 3-node cluster w/ <a href="https://microk8s.io/docs/getting-started">microk8s</a>.</li>
</ul>
</li>
<li><code>Terraform</code> iac to create:
<ul>
<li><a href="https://blogd.org/blog/2024/07/01/eks-with-terraform-and-helm"><code>LINK</code></a></li>
<li>IAM Role and policy association with serviceaccount</li>
<li>Networks, EKS cluster, node group, addons</li>
</ul>
</li>
<li><code>Helm Chart</code>
<ul>
<li>deploy application using templates</li>
<li><a href="https://blogd.org/blog/helm.pdf"><code>LINK</code></a></li>
</ul>
</li>
<li><code>Docker</code> and <code>Dockerfile</code> for building images</li>
<li><code>Github Actions</code> for CI
<ul>
<li>Github repository -&gt; Dockerhub image repository</li>
</ul>
</li>
<li><code>Microservices Architecture</code>
<ul>
<li>Frontend : Nginx (with html, css, js)</li>
<li>Backend : Golang (go-gin), Python (uvicorn) as backend web server</li>
</ul>
</li>
<li><code>Deep learning</code> algorithm for training and predicting Cat images using <code>numpy</code> and <code>pytorch</code> (in-progress)</li>
<li><code>Virtualbox</code> (with cli) to test configure 3 microk8s Kubernetes master nodes (ubuntu) in local environment</li>
<li><code>Golang Concurrency</code>
<ul>
<li>used context, channel, goroutine for concurrent programming</li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="microservices">Microservices </h2>
<ul>
<li>Kubelet configures Pods' DNS so that running containers can lookup Services by name rather than IP.</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/tbG85hA.png" alt="demo" width="600"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>applications diagram</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/KxETYaG.png" alt="ingress" width="750"></th>
</tr>
</thead>
</table>
<ul>
<li>
<p><code>Frontend - Nginx</code></p>
<ul>
<li>Nginx serves as the static content server, handling HTML, CSS, and JavaScript files.</li>
<li>It ensures efficient delivery of frontend resources to users' browsers.</li>
</ul>
</li>
<li>
<p><code>Backend - Go-Gin web-server</code></p>
<ul>
<li>The Go-Gin server acts as an intermediary between the frontend and backend services.</li>
<li>It receives requests from the frontend, including requests for cat-related information.</li>
<li>Additionally, it performs utility functions, such as fetching weather data for three cities using goroutine concurrency (5-worker).</li>
<li><a href="https://github.com/jnuho/simpledl/blob/main/cmd/backend-web-server/main.go#L50">main.go</a></li>
<li><a href="https://github.com/jnuho/simpledl/blob/main/pkg/weatherapi.go#L160">weatherapi.go</a>
<ul>
<li>Implemented with <code>Fan-out/Fan-in pattern</code></li>
<li>Another possible pattern: <a href="https://blogd.org/blog/2024/05/29/golang-worker-pool-pattern/"><code>Worker-pool pattern</code></a></li>
</ul>
</li>
</ul>
</li>
<li>
<p><code>Backend - Python uvicorn + fast api web-server</code></p>
<ul>
<li>The Python backend worker is responsible for image classification.</li>
<li>TODO (not complete):</li>
<li>Given an image URL, it uses PyTorch (and possibly NumPy) to perform binary classification (cat vs. non-cat).</li>
<li>The result of the classification is then relayed back to the Go-Gin server.</li>
</ul>
</li>
<li>
<p><code>How it works?</code></p>
<ul>
<li>When a user submits an image URL via the frontend(browser), the Go-Gin server receives the request.</li>
<li>It forwards the request to the Python backend.</li>
<li>The Python backend processes the image using the deep learning algorithm.</li>
<li>Finally, the result (whether the image contains a cat or not) is sent back to the frontend.</li>
</ul>
</li>
<li>
<p><code>Next Goal</code></p>
<ul>
<li>Enhance the Python backend by incorporating a deep learning algorithm using pytorch.</li>
<li>I initially did a Numpy implementation with 5-Layer and 2,500 iterations for training parameters.</li>
<li>Now, I'm exploring the use of PyTorch for training the model and performing predictions</li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="frontend-nginx">Frontend nginx </h2>
<ul>
<li>Vanilla Javascript</li>
<li>HTML/CSS - bootstrap</li>
<li>Nginx server that serves static files: /usr/share/nginx/html</li>
<li>Dockerized with <code>nginx:alpine</code> Image</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="backend-python-web-server">Backend Python web server </h2>
<ul>
<li>
<p>Use FastAPI + Unicorn</p>
<ul>
<li>FastAPI is an ASGI (<b>Asynchronous</b> Server Gateway Interface) framework which requires an ASGI server to run.</li>
<li>Unicorn is a lightning-fast ASGI server implementation</li>
</ul>
</li>
<li>
<p>install python (download .exe from <a href="http://python.org">python.org</a>)</p>
<ul>
<li>check Add to PATH option (required)</li>
</ul>
</li>
<li>
<p>Run the python web server</p>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>uvicorn main:app <span class="token parameter variable">--port</span> <span class="token number">3002</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="dockerize">Dockerize </h2>
<p><strong>NOTE</strong>: It is crucial to optimize Docker images to be as compact as possible. To achieve this is by utilizing base images that are minimalistic, such as the Alpine image and using <a href="#multi-stage-builds">Multi-stage builds</a>.</p>
<h3 id="multi-stage-builds">Multi-stage builds </h3>
<ul>
<li>Reference <a href="https://docs.docker.com/build/building/multi-stage">LINK</a></li>
</ul>
<pre data-role="codeBlock" data-info="Dockerfile" class="language-dockerfile Dockerfile"><code><span class="token comment"># Use an golang alpine as the base image</span>
<span class="token instruction"><span class="token keyword keyword-FROM">FROM</span> golang:1.22.3-alpine <span class="token keyword keyword-as">as</span> build</span>

<span class="token comment"># Set the temporary working directory in the container in the first stage</span>
<span class="token instruction"><span class="token keyword keyword-WORKDIR">WORKDIR</span> /</span>

<span class="token comment"># # Copy package.json and package-lock.json into the working directory</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> go.mod go.sum ./</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> backend/web ./backend/web</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> cmd/backend-web-server/main.go ./cmd/backend-web-server/main.go</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> pkg ./pkg</span>

<span class="token comment"># Copy the .env file into the working directory</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> .env .env</span>

<span class="token comment"># # Install the app dependencies inside the docker image</span>
<span class="token instruction"><span class="token keyword keyword-RUN">RUN</span> go mod download &amp;&amp; go mod verify</span>

<span class="token comment"># Set GOARCH and GOOS for the build target</span>
<span class="token instruction"><span class="token keyword keyword-ENV">ENV</span> CGO_ENABLED=0 GOOS=linux GOARCH=amd64</span>

<span class="token comment"># # Define the command to run your app using CMD which defines your runtime</span>
<span class="token instruction"><span class="token keyword keyword-RUN">RUN</span> go build -o backend-web-server ./cmd/backend-web-server</span>

<span class="token instruction"><span class="token keyword keyword-RUN">RUN</span> rm -rf /var/cache/apk/* /tmp/*</span>

<span class="token comment"># Use a smaller base image for the final image</span>
<span class="token instruction"><span class="token keyword keyword-FROM">FROM</span> alpine:latest</span>

<span class="token comment"># Copy the binary from the build stage</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> <span class="token options"><span class="token property">--from</span><span class="token punctuation">=</span><span class="token string">build</span></span> /backend-web-server /usr/local/bin/backend-web-server</span>

<span class="token comment"># Copy the .env file from the build stage</span>
<span class="token comment"># put in root directory / becasuse running CMD "backend-web-server" is ru</span>
<span class="token instruction"><span class="token keyword keyword-COPY">COPY</span> <span class="token options"><span class="token property">--from</span><span class="token punctuation">=</span><span class="token string">build</span></span> /.env /.env</span>

<span class="token instruction"><span class="token keyword keyword-EXPOSE">EXPOSE</span> 3001</span>

<span class="token comment"># When you specify CMD ["go-app"], Docker looks for an executable named go-app in the system’s $PATH.</span>
<span class="token comment"># The $PATH includes common directories where executables are stored, such as /usr/local/bin, /usr/bin, and others.</span>
<span class="token instruction"><span class="token keyword keyword-CMD">CMD</span> [<span class="token string">"backend-web-server"</span>, <span class="token string">"-web-host=:3001"</span>]</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="iac">IaC </h2>
<h3 id="terraform">Terraform </h3>
<ul>
<li>
<p><a href="https://github.com/jnuho/simpledl/tree/main/script/terraform">terraform scripts in repository</a></p>
</li>
<li>
<p>VPC, Subnet, igw, nat, route table, etc.</p>
</li>
<li>
<p>IAM role with assume-role-policy</p>
<ul>
<li>attach the required Amazon EKS IAM managed policy to it.</li>
</ul>
</li>
<li>
<p>Attach AmazonEKSClusterPolicy policy to IAM role: <code>6-eks.tf</code></p>
</li>
<li>
<p>Download terraform.exe</p>
<ul>
<li>Environment variable &gt; Add Path: C:\Program Files\terraform_1.8.5_windows_amd64</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># Navigate to your Terraform configuration directory</span>
<span class="token comment"># cd path/to/your/terraform/configuration</span>
<span class="token builtin class-name">cd</span> terraform

<span class="token comment"># Initialize Terraform</span>
terraform init

<span class="token comment"># Validate the configuration</span>
terraform validate

<span class="token comment"># Format the Configuration</span>
terraform <span class="token function">fmt</span>

<span class="token comment"># Plan the deployment</span>
terraform plan

<span class="token comment"># Apply the configuration</span>
terraform apply

<span class="token comment"># With DEBUGGING enabled</span>
<span class="token assign-left variable">TF_LOG</span><span class="token operator">=</span>DEBUG terraform apply

<span class="token comment"># Destroy</span>
<span class="token comment"># terraform destroy</span>
</code></pre><ul>
<li>Check ingressClass</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>kubectl get ingressclass <span class="token parameter variable">-A</span>
<span class="token comment"># NAME            CONTROLLER            PARAMETERS  AGE</span>
<span class="token comment"># alb             ingress.k8s.aws/alb   &lt;none&gt;      20m</span>
<span class="token comment"># external-nginx  k8s.io/ingress-nginx  &lt;none&gt;      20m</span>
</code></pre><h3 id="helm-chart">Helm Chart </h3>
<ul>
<li>
<p><a href="https://github.com/jnuho/simpledl/tree/main/script/tst-chart">helm chart scripts in repository</a></p>
</li>
<li>
<p>Configure <code>kubectl</code></p>
<ul>
<li>Check context : <code>kubectl config current-context</code></li>
<li>Update <code>.kube/config</code></li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># TO LOCAL</span>
kubectl config use-context minikube

<span class="token comment"># TO EKS</span>
aws eks update-kubeconfig <span class="token parameter variable">--region</span> ap-northeast-2 <span class="token parameter variable">--name</span> my-cluster <span class="token parameter variable">--profile</span> terraform
</code></pre><ul>
<li>Install <code>helm</code> on the same client PC as <code>kubectl</code></li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">curl</span> <span class="token parameter variable">-fsSL</span> <span class="token parameter variable">-o</span> get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
<span class="token function">chmod</span> <span class="token number">700</span> get_helm.sh
./get_helm.sh
</code></pre><ul>
<li>Create</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># Create helm chart</span>
helm create tst-chart
</code></pre><ul>
<li>Validate</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token builtin class-name">cd</span> simpledl/script
tree
    tst-chart
       ├── Chart.yaml
       ├── charts
       ├── templates
       │   ├── _helpers.tpl
       │   ├── deployment.yaml
       │   ├── hpa.yaml
       │   ├── ingress.yaml
       │   └── service.yaml
       ├── values.dev.yaml
       ├── values.prd.AWS.L4.lbc.yaml
       ├── values.prd.AWS.L7.lbc.yaml
       └── values.prd.AWS.L4.ingress.controller.yaml

helm lint tst-chart
helm template tst-chart <span class="token parameter variable">--debug</span>
<span class="token comment"># check results without installation</span>
<span class="token comment"># helm install --dry-run tst-chart --generate-name</span>
helm <span class="token function">install</span> --dry-run tst-release ./tst-chart <span class="token parameter variable">-f</span> ./tst-chart/values.prd.AWS.L4.ingress.controller.yaml
</code></pre><ul>
<li>Install</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>helm <span class="token function">install</span> tst-release ./tst-chart <span class="token parameter variable">-f</span> ./tst-chart/values.prd.AWS.L4.ingress.controller.yaml
</code></pre><ul>
<li>Upgrade
<ul>
<li>Helm will perform a rolling update for the affected resources (e.g., Deployments, StatefulSets).</li>
<li>Pods are replaced one by one, ensuring zero-downtime during the update.</li>
<li>Helm manages this process transparently.</li>
<li>Edit <code>values.dev.yaml</code> and apply <code>helm upgrade</code> command</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code>kubectl patch deployment my<span class="token punctuation">-</span>app <span class="token punctuation">-</span><span class="token punctuation">-</span>type='json' <span class="token punctuation">-</span>p='<span class="token punctuation">[</span><span class="token punctuation">{</span>"op"<span class="token punctuation">:</span><span class="token string">"replace"</span><span class="token punctuation">,</span>"path"<span class="token punctuation">:</span><span class="token string">"/spec/replicas"</span><span class="token punctuation">,</span>"value"<span class="token punctuation">:</span><span class="token number">5</span><span class="token punctuation">}</span><span class="token punctuation">]</span>'

<span class="token key atrule">services</span><span class="token punctuation">:</span> 
  <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
    <span class="token key atrule">replicaCount</span><span class="token punctuation">:</span> <span class="token number">3</span>
</code></pre><pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>helm list
    NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART              APP VERSION
    tst-release     default         <span class="token number">1</span>               <span class="token number">2024</span>-07-09 <span class="token number">14</span>:25:50.410043621 +0900 KST deployed        tst-chart-0.1.0    <span class="token number">1.16</span>.0

helm upgrade tst-release ./tst-chart <span class="token parameter variable">-f</span> ./tst-chart/values.prd.AWS.L4.ingress.controller.yaml
    Release <span class="token string">"tst-release"</span> has been upgraded. Happy Helming<span class="token operator">!</span>
    NAME: tst-release
    LAST DEPLOYED: Tue Jul  <span class="token number">9</span> <span class="token number">14</span>:35:35 <span class="token number">2024</span>
    NAMESPACE: default
    STATUS: deployed
    REVISION: <span class="token number">2</span>
    TEST SUITE: None

helm list
    NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART              APP VERSION
    tst-release     default         <span class="token number">2</span>               <span class="token number">2024</span>-07-09 <span class="token number">14</span>:35:35.404055879 +0900 KST deployed        tst-chart-0.1.0    <span class="token number">1.16</span>.0
</code></pre><ul>
<li>Rollback</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>helm rollback tst-release VERSION_NO
</code></pre><ul>
<li>Uninstall (Helm v3)
<ul>
<li><code>helm delete --purge</code> in Helm V2</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>helm uninstall tst-release
</code></pre><ul>
<li>Helm Repository
<ul>
<li>While you can deploy a Helm chart directly from the filesystem,</li>
<li>it’s recommended to use Helm repositories.</li>
<li>Helm repositories allow versioning, collaboration, and easy distribution of charts</li>
<li><a href="https://www.kubernet.dev/getting-started-with-helm-simplifying-kubernetes-application-deployments"><code>LINK</code></a></li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/YpjRWc6.png" alt="pods" width="700"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>ingress resource</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/Ymkj2PH.png" alt="pods" width="400"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>aws load-balancer controller pod in <code>kube-system</code> namespace</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="kubernetes-for-mlops">Kubernetes for MLOps </h2>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://coffeewhale.com/assets/images/mlops/hidden-model.png" alt="pods" width="580"></th>
</tr>
</thead>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://www.determined.ai/assets/images/blogs/kubernetes-bad/kubeflow-unicorns.png" alt="pods" width="480"></th>
</tr>
</thead>
</table>
<ul>
<li>Challenges of Using Kubernetes-Based ML Tools
<ul>
<li>Containerizing Code (Docker Image Build and Execution):</li>
<li>Writing Kubernetes Manifests (YAML Files):</li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="appendix">Appendix </h2>
<ul>
<li><a href="#exposing-external-service"><code>Exposing external service</code></a></li>
<li><a href="#terraform-reference"><code>Terraform Reference</code></a></li>
<li><a href="#binary-classification"><code>Binary classification</code></a></li>
<li><a href="#mathematical-background"><code>Mathematical background</code></a></li>
<li><a href="#image-classification"><code>Image Classification</code></a></li>
<li><a href="#vite-for-development"><code>vite for development</code></a></li>
<li><a href="#virtualbox-network-architecture"><code>Virtualbox network architecture</code></a></li>
<li><a href="#virtualbox-setup"><code>Virtualbox setup</code></a></li>
<li><a href="#cors-issue"><code>CORS issue</code></a></li>
<li><a href="#minikube-implementation"><code>Minikube implementation</code></a></li>
<li><a href="#microk8s-implemntation"><code>Microk8s implemntation</code></a></li>
<li><a href="#golang-ini-setting"><code>Golang ini setting</code></a></li>
<li><a href="#aws-loadbalancer-controller"><code>AWS LoadBalancer Controller</code></a></li>
</ul>
<h3 id="exposing-external-service">Exposing external service </h3>
<ul>
<li><a href="#https://youtu.be/ePqUq06WoLk?si=jlRgm1oI9RI_d7RF"><code>LINK</code></a></li>
</ul>
<h3 id="terraform-reference">Terraform Reference </h3>
<ul>
<li><a href="#https://antonputra.com/terraform/how-to-create-eks-cluster-using-terraform">LINK</a></li>
</ul>
<h3 id="binary-classification">Binary classification </h3>
<p>It is a basic deep learning image recognizers, one of which was covered in Andrew Ng's coursera course. I plan to test two simple deep learning models to identify cat images and hand-written digits (0-9), respectively and return the result of identification to the browser.</p>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="mathematical-background">Mathematical background </h3>
<p>The basic operations for forward and backward propagations in deep learning algorithm are as follows:</p>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/ZJ94x9B.png" alt="propagation" width="450"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>Forward and Backward propagation</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="image-classification">Image Classification </h3>
<ul>
<li>
<p>cat vs.non-cat image classification and hand-written digits recognition</p>
</li>
<li>
<p><a href="https://www.youtube.com/watch?v=JgtWVML4Ykg&amp;ab_channel=SheldonVon">https://www.youtube.com/watch?v=JgtWVML4Ykg&amp;ab_channel=SheldonVon</a></p>
</li>
<li>
<p><a href="https://detexify.kirelabs.org/classify.html">https://detexify.kirelabs.org/classify.html</a></p>
</li>
<li>
<p><a href="https://mco-mnist-draw-rwpxka3zaa-ue.a.run.app/">https://mco-mnist-draw-rwpxka3zaa-ue.a.run.app/</a></p>
</li>
<li>
<p>pytorch</p>
<ul>
<li><a href="https://youtu.be/EMXfZB8FVUA?si=XL8SckGQi9xQDgtc">https://youtu.be/EMXfZB8FVUA?si=XL8SckGQi9xQDgtc</a></li>
<li><a href="https://pytorch.org/get-started/locally/">https://pytorch.org/get-started/locally/</a></li>
</ul>
</li>
<li>
<p>CPU (Without Nvidia CUDA) only</p>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>pip3 <span class="token function">install</span> torch torchvision torchaudio

<span class="token comment"># requirements.txt</span>
<span class="token assign-left variable">torch</span><span class="token operator">==</span><span class="token number">2.3</span>.0
<span class="token assign-left variable">torchaudio</span><span class="token operator">==</span><span class="token number">2.3</span>.0
<span class="token assign-left variable">torchvision</span><span class="token operator">==</span><span class="token number">0.18</span>.0

<span class="token comment"># install using requirements.txt</span>
python <span class="token function">install</span> <span class="token parameter variable">-r</span> requirements.txt
</code></pre><pre data-role="codeBlock" data-info="python" class="language-python python"><code><span class="token keyword keyword-import">import</span> torch

x <span class="token operator">=</span> torch<span class="token punctuation">.</span>rand<span class="token punctuation">(</span><span class="token number">3</span><span class="token punctuation">)</span>
<span class="token comment"># tensor([.5907, .0781, .3094])</span>
<span class="token keyword keyword-print">print</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span>

<span class="token keyword keyword-print">print</span><span class="token punctuation">(</span>torch<span class="token punctuation">.</span>cuda<span class="token punctuation">.</span>is_available<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="vite-for-development">vite for development </h3>
<ul>
<li>Download &amp; install nodejs 20.12.2
<ul>
<li>for local development using <code>vite</code></li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">npm</span> create vite@latest
    ? Project name: lesson11
    <span class="token operator">&gt;</span> choose Vanilla, TypeScript
</code></pre><ul>
<li>Edit <code>package.json</code> to edit port and dependencies</li>
</ul>
<pre data-role="codeBlock" data-info="json" class="language-json json"><code>    <span class="token property">"scripts"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"dev"</span><span class="token operator">:</span> <span class="token string">"vite --host 0.0.0.0 --port 8080"</span><span class="token punctuation">,</span>
        <span class="token property">"build"</span><span class="token operator">:</span> <span class="token string">"tsc &amp;&amp; vite build"</span><span class="token punctuation">,</span>
        <span class="token property">"preview"</span><span class="token operator">:</span> <span class="token string">"vite preview"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>

    <span class="token property">"dependencies"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"axios"</span><span class="token operator">:</span> <span class="token string">"^1.6.8"</span>
    <span class="token punctuation">}</span>
</code></pre><p>I used nodejs vite for local development environment.<br>
I will be using nginx in production environment.</p>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># install dependencies specified in package.json</span>
<span class="token comment"># install if package.json changes e.g. project name</span>
<span class="token function">npm</span> i
<span class="token function">npm</span> run dev
    VITE v5.2.9    ready <span class="token keyword keyword-in">in</span> <span class="token number">180</span> ms

    ➜    Local:     http://localhost:4200/
    ➜    Network: use <span class="token parameter variable">--host</span> to expose
    ➜    press h + enter to show <span class="token builtin class-name">help</span>
</code></pre><ul>
<li>Edit code
<ul>
<li>Write <code>index.html</code></li>
<li>Create directory: <code>./model</code>, <code>./templates</code></li>
<li>Define models and templates</li>
<li>Edit <code>main.ts</code></li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h2 id="backend-golang-web-server">Backend Golang web server </h2>
<ul>
<li><code>go.mod</code>, <code>go.sum</code> must be in github repo root directory</li>
<li>sources:
<ul>
<li><code>cmd/backend-server/main.go</code></li>
<li><code>backend/web/handler.go</code></li>
<li><code>backend/web/server.go</code></li>
<li><code>backend/web/util.go</code></li>
<li><code>backend/pkg/weatherapi.go</code></li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token builtin class-name">cd</span> simpledl
go mod init github.com/jnuho/simpledl
go mod tidy
</code></pre><h3 id="virtualbox-network-architecture">Virtualbox network architecture </h3>
<p>I had to construct a virtualbox environment in which my kubernetes cluster and application will be deployed. 🔥</p>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://i.imgur.com/w8PxxXk.png" alt="simpledl architecture" width="400"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>kubernetes architecture (Local VirtualBox)</em></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/tyhjPsG.png" alt="pods" width="520"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>NAT network</em></td>
</tr>
</tbody>
</table>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="virtualbox-setup">Virtualbox Setup </h3>
<ul>
<li>
<p>Download ubuntu iso image</p>
</li>
<li>
<p>Run vm instacne using iso image</p>
</li>
<li>
<p>Install ubuntu</p>
</li>
<li>
<p>Hosts: 10.0.2.3, 10.0.2.4, 10.0.2.5</p>
</li>
<li>
<p>OS: Ubuntu 24.04 server</p>
</li>
</ul>
<pre data-role="codeBlock" data-info="bat" class="language-bat bat"><code>vboxmanage list dhcpservers
vboxmanage list natnetworks
vboxmanage list vms

VBoxManage dhcpserver remove --netname k8snetwork
VBoxManage natnetwork remove --netname k8snetwork

VBoxManage unregistervm ubuntu-1 --delete
VBoxManage unregistervm ubuntu-2 --delete
VBoxManage unregistervm ubuntu-3 --delete

./vb-create.bat &gt; log.txt 2&gt;&amp;1
</code></pre><pre data-role="codeBlock" data-info="bat" class="language-bat bat"><code>VBoxManage natnetwork add --netname k8snetwork --network "10.0.2.0/24" --enable --dhcp on
VBoxManage dhcpserver add --netname k8snetwork --server-ip "10.0.2.2" --netmask "255.255.255.0" --lower-ip "10.0.2.3" --upper-ip "10.0.2.254" --enable

vboxmanage dhcpserver restart --network=k8snetwork

for /L %%i in (1, 1, 3) do (
    REM Create VM
    VBoxManage createvm --name ubuntu-%%i --register --ostype Ubuntu_64
    REM ...
    REM ...
)

REM Set up port forwarding rules
VBoxManage natnetwork modify --netname k8snetwork --port-forward-4 "Rule 1:tcp:[127.0.0.1]:22021:[10.0.2.3]:22"
VBoxManage natnetwork modify --netname k8snetwork --port-forward-4 "Rule 2:tcp:[127.0.0.1]:22022:[10.0.2.4]:22"
VBoxManage natnetwork modify --netname k8snetwork --port-forward-4 "Rule 3:tcp:[127.0.0.1]:22023:[10.0.2.5]:22"

REM application port
VBoxManage natnetwork modify --netname k8snetwork --port-forward-4 "Http:tcp:[127.0.0.1]:80:[10.0.2.3]:80"
</code></pre><pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># ethernet device info</span>
nmcli d

nmcli d show enp0s3

<span class="token function">ip</span> a dev enp0s3

<span class="token function">sudo</span> <span class="token function">ip</span> <span class="token function">link</span> <span class="token builtin class-name">set</span> enp0s3 down
<span class="token function">sudo</span> <span class="token function">ip</span> <span class="token function">link</span> <span class="token builtin class-name">set</span> enp0s3 up
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="cors-issue">CORS issue </h3>
<ul>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS">https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS</a></li>
</ul>
<p>When a web application tries to make a request to a server that’s on a different domain, protocol, or port,<br>
it encounters a CORS (Cross-Origin Resource Sharing) issue. Add headers to backend server accordingly</p>
<pre data-role="codeBlock" data-info="" class="language-text"><code>For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts.
For example, fetch() and XMLHttpRequest follow the same-origin policy.

This means that a web application using those APIs can only request resources
from the same origin the application was loaded from unless the response
from other origins includes the right CORS headers.

=&gt; Add appropriate headers in golang server.
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="minikube-implementation">Minikube implementation </h3>
<p>To set up your Nginx, Golang, and Python microservices on Minikube, you'll need to create Kubernetes Deployment and Service YAML files for each of your microservices. You'll also need to set up an Ingress controller to expose your services to the public. Here's a high-level overview of the steps:</p>
<ol>
<li><strong>Install Minikube</strong>: If you haven't already, you'll need to install Minikube on your machine. Minikube is a tool that lets you run Kubernetes locally.</li>
</ol>
<ul>
<li>ubuntu 24.04 install minikube</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">curl</span> <span class="token parameter variable">-LO</span> https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
<span class="token function">sudo</span> dpkg <span class="token parameter variable">-i</span> minikube_latest_amd64.deb

<span class="token comment"># unintstall</span>
<span class="token comment">#sudo dpkg -r minikube</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="2">
<li><strong>Start Minikube</strong>: Once installed, you can start a local Kubernetes cluster with the command <code>minikube start</code>.</li>
</ol>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># As a TROUBLE SHOOTING:</span>
<span class="token function">docker</span> context use default
    default
    Current context is now <span class="token string">"default"</span>

minikube start
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="3">
<li><strong>Create secret</strong></li>
</ol>
<p>3-1. Login to docker hub</p>
<pre data-role="codeBlock" data-info="" class="language-text"><code>docker login --username YOUR_USERNAME
</code></pre><p>3-2. Create secret</p>
<pre data-role="codeBlock" data-info="" class="language-text"><code>k create secret docker-registry regcred \
    --docker-server=https://index.docker.io/v1/ \
    --docker-username=USER \
    --docker-password=PW \
    --docker-email=EMAIL

k get secret
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="4">
<li><strong>Create Deployment and Service YAML Files</strong>: For each of your microservices (Nginx, Golang, Python), you'll need to create a Deployment and a Service. The Deployment defines your application and the Docker image it uses, while the Service defines how your application is exposed to the network</li>
</ol>
<p>4-1. deployment.yaml</p>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> apps/v1
<span class="token key atrule">kind</span><span class="token punctuation">:</span> Deployment
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
    <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>deployment
<span class="token key atrule">spec</span><span class="token punctuation">:</span>
    <span class="token key atrule">replicas</span><span class="token punctuation">:</span> <span class="token number">1</span>
    <span class="token comment"># Deployement manages pods with label 'app: fe-nginx</span>
    <span class="token key atrule">selector</span><span class="token punctuation">:</span>
        <span class="token key atrule">matchLabels</span><span class="token punctuation">:</span>
            <span class="token key atrule">app</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
    <span class="token comment"># define labels for the Pods:</span>
    <span class="token comment">#     must be matched by service.yaml &gt; spec.selector</span>
    <span class="token key atrule">template</span><span class="token punctuation">:</span>
        <span class="token key atrule">metadata</span><span class="token punctuation">:</span>
            <span class="token key atrule">labels</span><span class="token punctuation">:</span>
                <span class="token key atrule">app</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
        <span class="token key atrule">spec</span><span class="token punctuation">:</span>
            <span class="token key atrule">containers</span><span class="token punctuation">:</span>
            <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
                <span class="token key atrule">image</span><span class="token punctuation">:</span> jnuho/fe<span class="token punctuation">-</span>nginx<span class="token punctuation">:</span>latest
                <span class="token key atrule">ports</span><span class="token punctuation">:</span>
                <span class="token punctuation">-</span> <span class="token key atrule">containerPort</span><span class="token punctuation">:</span> <span class="token number">80</span>
            <span class="token key atrule">imagePullSecrets</span><span class="token punctuation">:</span>
            <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> regcred

</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<p>4-2. service.yaml</p>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> v1
<span class="token key atrule">kind</span><span class="token punctuation">:</span> Service
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
    <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>service
    <span class="token key atrule">namespace</span><span class="token punctuation">:</span> simple
<span class="token key atrule">spec</span><span class="token punctuation">:</span>
    <span class="token comment"># must match deployment.yaml &gt; spec.template.metadata.labels</span>
    <span class="token key atrule">selector</span><span class="token punctuation">:</span>
        <span class="token key atrule">app</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
    <span class="token key atrule">ports</span><span class="token punctuation">:</span>
        <span class="token punctuation">-</span> <span class="token key atrule">protocol</span><span class="token punctuation">:</span> TCP
            <span class="token key atrule">port</span><span class="token punctuation">:</span> <span class="token number">8080</span>
            <span class="token key atrule">targetPort</span><span class="token punctuation">:</span> <span class="token number">80</span>
    <span class="token key atrule">type</span><span class="token punctuation">:</span> ClusterIP
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="5">
<li><strong>Apply the YAML Files</strong>: Once you've created your YAML files, you can apply them to your Kubernetes cluster with the command <code>kubectl apply -f &lt;filename.yaml&gt;</code>.</li>
</ol>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="6">
<li><strong>Enable Ingress Controller</strong>:</li>
</ol>
<p>6-1. NGINX ingress controller using Minikube addons: you can use the command <code>minikube addons enable ingress</code></p>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>minikube addons <span class="token builtin class-name">enable</span> ingress
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<p>6-2. Nginx ingress controller</p>
<ul>
<li><a href="https://medium.com/@amirhosseineidy/how-to-set-up-nginx-ingress-controller-in-local-server-6cc4bd7d6a6b">setting up an NGINX ingress controller</a> in a bare metal or local server:</li>
</ul>
<p>Ingress is an API in Kubernetes that routes traffic to different services, making applications accessible to clients from the Kubernetes cluster. Among multiple choices like HAProxy or Envoy for setting up an ingress controller, NGINX is the most popular one. It is powered by the NGINX web server and is a fast and secure controller that delivers your applications to the clients easily.</p>
<ul>
<li>Install NGINX ingress controller with <code>helm</code></li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># inside cmd or powershell</span>
winget <span class="token function">install</span> Helm.Helm

<span class="token comment"># RESTART terminal and do:</span>
helm upgrade <span class="token parameter variable">--install</span> ingress-nginx ingress-nginx <span class="token punctuation">\</span>
    <span class="token parameter variable">--repo</span> https://kubernetes.github.io/ingress-nginx <span class="token punctuation">\</span>
    <span class="token parameter variable">--namespace</span> ingress-nginx --create-namespace
</code></pre><ul>
<li>Check if ingress controller is working:</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>helm list
    NAME                        NAMESPACE             REVISION                UPDATED                                                                 STATUS                    CHART                                     APP VERSION
    ingress-nginx     default                 <span class="token number">1</span>                             <span class="token number">2024</span>-04-30 <span class="token number">14</span>:26:18.9350713 +0900 KST     deployed                ingress-nginx-4.10.1        <span class="token number">1.10</span>.1

k get ClusterRole <span class="token operator">|</span> <span class="token function">grep</span> ingress
    ingress-nginx                                                                                                                    <span class="token number">2024</span>-04-30T07:01:05Z

k get all
    NAME                                                                                     READY     STATUS        RESTARTS     AGE
    pod/ingress-nginx-controller-cf668668c-zvkd9     <span class="token number">1</span>/1         Running     <span class="token number">0</span>                    44s

    NAME                                                                                 TYPE                     CLUSTER-IP             EXTERNAL-IP     PORT<span class="token punctuation">(</span>S<span class="token punctuation">)</span>                                            AGE
    service/ingress-nginx-controller                         LoadBalancer     <span class="token number">10.100</span>.168.236     <span class="token operator">&lt;</span>pending<span class="token operator">&gt;</span>         <span class="token number">80</span>:32020/TCP,443:31346/TCP     44s
    service/ingress-nginx-controller-admission     ClusterIP            <span class="token number">10.107</span>.208.79        <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>                <span class="token number">443</span>/TCP                                            44s
    service/kubernetes                                                     ClusterIP            <span class="token number">10.96</span>.0.1                <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>                <span class="token number">443</span>/TCP                                            4m8s

    NAME                                                                             READY     UP-TO-DATE     AVAILABLE     AGE
    deployment.apps/ingress-nginx-controller     <span class="token number">1</span>/1         <span class="token number">1</span>                        <span class="token number">1</span>                     44s

    NAME                                                                                                 DESIRED     CURRENT     READY     AGE
    replicaset.apps/ingress-nginx-controller-cf668668c     <span class="token number">1</span>                 <span class="token number">1</span>                 <span class="token number">1</span>             44s
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="7">
<li><strong>Create an Ingress YAML File</strong>: The Ingress YAML file will define the rules for routing external traffic to your services. You'll need to specify the host and path for each service, and the service that should handle traffic to each host/path</li>
</ol>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="8">
<li><strong>Apply the Ingress YAML File</strong>: Just like with the Deployment and Service files, you can apply the Ingress file with <code>kubectl apply -f &lt;ingress-filename.yaml&gt;</code>.</li>
</ol>
<ul>
<li>Ingress rules
<ul>
<li>Ingress rules are resources that help route services to your desired domain name or prefix. They are divided into prefix and DNS.</li>
<li>.yaml mainifest for ingress rules</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>k apply ingress.yaml
k get ingress
    NAME                             CLASS     HOSTS                                ADDRESS                PORTS     AGE
    fe-nginx-ingress     nginx     my-app.example.com     <span class="token number">192.168</span>.49.2     <span class="token number">80</span>            4m35s
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ol start="9">
<li><strong>Access Your Services</strong>: With the Ingress set up, you should be able to access your services from outside your Kubernetes cluster. You can get the IP address of your Minikube cluster with the command <code>minikube ip</code>, and then access your services at that IP</li>
</ol>
<ul>
<li>
<p>Accessing application</p>
<ul>
<li>For accessing these applications in a local cluster, you should access it through node port (30000 ports) or use a reverse proxy to send them.</li>
<li>But is there any way to access app on port 80 or 443?
<ul>
<li>use Port-forward or <code>MetalLB</code> to allow access to app on port 80 or 443.</li>
</ul>
</li>
</ul>
</li>
<li>
<p>port forward</p>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>k get svc <span class="token parameter variable">-n</span> ingress-nginx
NAME                                                                 TYPE                CLUSTER-IP         EXTERNAL-IP     PORT<span class="token punctuation">(</span>S<span class="token punctuation">)</span>                                            AGE
ingress-nginx-controller                         NodePort        <span class="token number">10.107</span>.26.28     <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>                <span class="token number">80</span>:32361/TCP,443:31064/TCP     3h9m
ingress-nginx-controller-admission     ClusterIP     <span class="token number">10.106</span>.14.66     <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>                <span class="token number">443</span>/TCP                                            3h9m

kubectl port-forward <span class="token parameter variable">-n</span> <span class="token operator">&lt;</span>namespace<span class="token operator">&gt;</span> svc/<span class="token operator">&lt;</span>service-name<span class="token operator">&gt;</span> <span class="token operator">&lt;</span>local-port<span class="token operator">&gt;</span>:<span class="token operator">&lt;</span>service-port<span class="token operator">&gt;</span>
kubectl port-forward <span class="token parameter variable">-n</span> ingress-nginx svc/ingress-nginx-controller <span class="token number">80</span>:80 <span class="token number">3001</span>:3001 <span class="token number">3002</span>:3002

</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>Installing Metallb</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># strictARP to true</span>
kubectl edit configmap <span class="token parameter variable">-n</span> kube-system kube-proxy

    apiVersion: kubeproxy.config.k8s.io/v1alpha1
    kind: KubeProxyConfiguration
    mode: <span class="token string">"ipvs"</span>
    ipvs:
        strictARP: <span class="token boolean">true</span>

kubectl apply <span class="token parameter variable">-f</span> https://raw.githubusercontent.com/metallb/metallb/v0.13.10/config/manifests/metallb-frr.yaml

kubectl get pods <span class="token parameter variable">-n</span> metallb-system
    NAME                                                    READY     STATUS        RESTARTS     AGE
    controller-596589985b-jrnmk     <span class="token number">1</span>/1         Running     <span class="token number">0</span>                    34m
    speaker-hdrmc                                 <span class="token number">4</span>/4         Running     <span class="token number">0</span>                    34m
</code></pre><ul>
<li>Now set a range IPs for your local load balancer by creating a configMap.
<ul>
<li>Remember that the set of IP addresses you apply must be in the same range as your nodes IPs</li>
</ul>
</li>
</ul>
<p>The range of IP addresses you choose for MetalLB should be in the same subnet as your nodes' IPs. These IP addresses are used by MetalLB to assign to services of type LoadBalancer.<br>
Using command, <code>k get node -o wide</code>, the INTERNAL-IP of my node is 192.168.49.2. So, choose a range of IP addresses in the 192.168.49.x range for MetalLB. For example, 192.168.49.100-192.168.49.110 as my range.</p>
<p>The IP addresses you choose for MetalLB should be reserved for MetalLB's use and should not conflict with any other devices on your network.</p>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token comment"># to see ip range for node</span>
kubectl get nodes <span class="token punctuation">-</span>o wide
    NAME             STATUS     ROLES                     AGE     VERSION     INTERNAL<span class="token punctuation">-</span>IP        EXTERNAL<span class="token punctuation">-</span>IP     OS<span class="token punctuation">-</span>IMAGE                         KERNEL<span class="token punctuation">-</span>VERSION                                             CONTAINER<span class="token punctuation">-</span>RUNTIME
    minikube     Ready        control<span class="token punctuation">-</span>plane     41m     v1.30.0     192.168.49.2     &lt;none<span class="token punctuation">&gt;</span>                Ubuntu 22.04.4 LTS     5.15.146.1<span class="token punctuation">-</span>microsoft<span class="token punctuation">-</span>standard<span class="token punctuation">-</span>WSL2     docker<span class="token punctuation">:</span>//26.0.1

cat <span class="token punctuation">&gt;</span> configmap.yaml
<span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> metallb.io/v1beta1
<span class="token key atrule">kind</span><span class="token punctuation">:</span> IPAddressPool
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
    <span class="token key atrule">name</span><span class="token punctuation">:</span> nat
    <span class="token key atrule">namespace</span><span class="token punctuation">:</span> metallb<span class="token punctuation">-</span>system
<span class="token key atrule">spec</span><span class="token punctuation">:</span>
    <span class="token key atrule">addresses</span><span class="token punctuation">:</span>
        <span class="token punctuation">-</span> 192.168.49.100<span class="token punctuation">-</span>192.168.49.110
<span class="token punctuation">---</span>
<span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> metallb.io/v1beta1
<span class="token key atrule">kind</span><span class="token punctuation">:</span> L2Advertisement
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
    <span class="token key atrule">name</span><span class="token punctuation">:</span> empty
    <span class="token key atrule">namespace</span><span class="token punctuation">:</span> metallb<span class="token punctuation">-</span>system


k apply <span class="token punctuation">-</span>f configmap.yaml

kubectl rollout restart deployment controller <span class="token punctuation">-</span>n metallb<span class="token punctuation">-</span>system

<span class="token comment"># check EXTERNAL-IP for nginx-controller is assigned!!!</span>
<span class="token comment"># the external IPS is assigned to your NGINX load balancer service and all other load balancer typed services.</span>
k get svc
    NAME                                                                 TYPE                     CLUSTER<span class="token punctuation">-</span>IP             EXTERNAL<span class="token punctuation">-</span>IP            PORT(S)                                            AGE
    ingress<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>controller                         LoadBalancer     10.100.168.236     192.168.49.100     80<span class="token punctuation">:</span>32020/TCP<span class="token punctuation">,</span>443<span class="token punctuation">:</span>31346/TCP     68m
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>DNS Setup
<ul>
<li>Finally, you need to set the domain names defined in the ingress rules in your DNS server or hosts file</li>
<li>edit hosts file, <code>C:\Windows\System32\drivers\etc\hosts</code></li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="" class="language-text"><code>192.168.49.100 my-app.example.com
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="using-minikube-for-image-build-and-local-development">Using Minikube for image build and local development </h3>
<ul>
<li><a href="https://www.youtube.com/watch?v=_1uWY1GdDVY&amp;ab_channel=GoogleOpenSource">https://www.youtube.com/watch?v=_1uWY1GdDVY&amp;ab_channel=GoogleOpenSource</a></li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>minikube docker-env
        W0502 <span class="token number">10</span>:17:02.728250     <span class="token number">12636</span> main.go:291<span class="token punctuation">]</span> Unable to resolve the current Docker CLI context <span class="token string">"default"</span><span class="token builtin class-name">:</span> context <span class="token string">"default"</span><span class="token builtin class-name">:</span> context not found: <span class="token function">open</span> C:<span class="token punctuation">\</span>Users<span class="token punctuation">\</span>user<span class="token punctuation">\</span>.docker<span class="token punctuation">\</span>contexts<span class="token punctuation">\</span>meta<span class="token punctuation">\</span>37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f<span class="token punctuation">\</span>meta.json: The system cannot <span class="token function">find</span> the path specified.
        <span class="token builtin class-name">export</span> <span class="token assign-left variable">DOCKER_TLS_VERIFY</span><span class="token operator">=</span><span class="token string">"1"</span>
        <span class="token builtin class-name">export</span> <span class="token assign-left variable">DOCKER_HOST</span><span class="token operator">=</span><span class="token string">"tcp://127.0.0.1:57853"</span>
        <span class="token builtin class-name">export</span> <span class="token assign-left variable">DOCKER_CERT_PATH</span><span class="token operator">=</span><span class="token string">"C:\Users\user\.minikube<span class="token entity" title="\c">\c</span>erts"</span>
        <span class="token builtin class-name">export</span> <span class="token assign-left variable">MINIKUBE_ACTIVE_DOCKERD</span><span class="token operator">=</span><span class="token string">"minikube"</span>

<span class="token comment"># To point your shell to minikube's docker-daemon, run:</span>
<span class="token comment"># eval $(minikube -p minikube docker-env)</span>


<span class="token comment"># Now your PC directs to minikube's docker</span>
<span class="token comment"># From now, Any image you build will be directory on built on minikube's docker</span>

<span class="token comment"># list images inside minikube cluster</span>
<span class="token function">docker</span> images <span class="token parameter variable">-a</span>

<span class="token builtin class-name">cd</span> dockerfiles
<span class="token function">docker</span> build <span class="token parameter variable">-f</span> dockerfiles/Dockerfile-nginx <span class="token parameter variable">-t</span> fe-nginx <span class="token builtin class-name">.</span>

</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>deployment.yaml</li>
</ul>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">spec</span><span class="token punctuation">:</span>
    <span class="token key atrule">templates</span><span class="token punctuation">:</span>
        <span class="token key atrule">spec</span><span class="token punctuation">:</span>
            <span class="token key atrule">containers</span><span class="token punctuation">:</span>
            <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
                <span class="token key atrule">image</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">:</span>latest
                <span class="token key atrule">ports</span><span class="token punctuation">:</span>
                <span class="token punctuation">-</span> <span class="token key atrule">containerPort</span><span class="token punctuation">:</span> <span class="token number">80</span>
</code></pre><pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>k apply <span class="token parameter variable">-f</span> deployment.yaml
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>suppose source changed -&gt; change image</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">docker</span> rmi fe-nginx:latest
<span class="token function">docker</span> build <span class="token parameter variable">-f</span> dockerfiles/Dockerfile-nginx <span class="token parameter variable">-t</span> fe-nginx <span class="token builtin class-name">.</span>
k delete <span class="token parameter variable">-f</span> deployment.yaml
k apply <span class="token parameter variable">-f</span> deployment.yaml
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>mount data to minikube cluster
<ul>
<li>suppose golang docker container source does:</li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="go" class="language-go go"><code><span class="token keyword keyword-var">var</span> version <span class="token operator">=</span> <span class="token string">"0.0.2"</span>
<span class="token keyword keyword-func">func</span> <span class="token function">indexHandler</span><span class="token punctuation">(</span>w http<span class="token punctuation">.</span>ResponseWriter<span class="token punctuation">,</span> req <span class="token operator">*</span>http<span class="token punctuation">.</span>Request<span class="token punctuation">)</span><span class="token punctuation">{</span> 
        <span class="token comment">// after deployment.yaml volumeMount, this will printout</span>
        <span class="token comment">// NOTE:</span>
        localFile<span class="token punctuation">,</span> err <span class="token operator">:=</span> os<span class="token punctuation">.</span><span class="token function">ReadFile</span><span class="token punctuation">(</span><span class="token string">"/tmp/data/hello-world.txt"</span><span class="token punctuation">)</span>
        <span class="token keyword keyword-if">if</span> err <span class="token operator">!=</span> <span class="token boolean">nil</span> <span class="token punctuation">{</span>
                fmt<span class="token punctuation">.</span><span class="token function">Printf</span><span class="token punctuation">(</span><span class="token string">"couldn't read file %v\n"</span><span class="token punctuation">,</span> err<span class="token punctuation">)</span>
        <span class="token punctuation">}</span>
        <span class="token comment">// before deployment.yaml volumeMount, this will printout</span>
        fmt<span class="token punctuation">.</span><span class="token function">FPrintf</span><span class="token punctuation">(</span>w<span class="token punctuation">,</span><span class="token string">"&lt;h1&gt;hello world :) &lt;/h1&gt; \n Version %s\n File Content:%s"</span><span class="token punctuation">,</span> version<span class="token punctuation">,</span> localFile<span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre><pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>minikube <span class="token function">mount</span>    <span class="token punctuation">{</span>localdir<span class="token punctuation">}</span>:<span class="token punctuation">{</span>minikube hostdir<span class="token punctuation">}</span>

<span class="token comment"># mount a volume to minikube cluster (persistant storage)</span>
<span class="token comment"># mount files to minikube cluster</span>
minikube <span class="token function">mount</span>    /c/Users/user/Downloads/tmp:/tmp/data
</code></pre><pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">spec</span><span class="token punctuation">:</span>
    <span class="token key atrule">templates</span><span class="token punctuation">:</span>
        <span class="token key atrule">spec</span><span class="token punctuation">:</span>
            <span class="token key atrule">containers</span><span class="token punctuation">:</span>
            <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
                <span class="token key atrule">image</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">:</span>latest
                <span class="token key atrule">ports</span><span class="token punctuation">:</span>
                <span class="token punctuation">-</span> <span class="token key atrule">containerPort</span><span class="token punctuation">:</span> <span class="token number">80</span>
                <span class="token comment"># target dir inside pod: /tmp/data</span>
                <span class="token key atrule">volumeMounts</span><span class="token punctuation">:</span>
                <span class="token punctuation">-</span> <span class="token key atrule">mountPath</span><span class="token punctuation">:</span> /tmp/data
                    <span class="token key atrule">name</span><span class="token punctuation">:</span> test<span class="token punctuation">-</span>volume
            <span class="token key atrule">volumes</span><span class="token punctuation">:</span>
                <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> test<span class="token punctuation">-</span>volume
                    <span class="token comment"># host is kubernetes host(vm)</span>
                    <span class="token key atrule">hostPath</span><span class="token punctuation">:</span>
                        <span class="token comment"># directory location on host</span>
                        <span class="token key atrule">path</span><span class="token punctuation">:</span> /tmp/data
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>apply the changes:</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">docker</span> rmi fe-nginx:latest
<span class="token function">docker</span> build <span class="token parameter variable">-f</span> dockerfiles/Dockerfile-nginx <span class="token parameter variable">-t</span> fe-nginx <span class="token builtin class-name">.</span>
k delete <span class="token parameter variable">-f</span> deployment.yaml
k apply <span class="token parameter variable">-f</span> deployment.yaml

<span class="token comment"># deploy the app</span>
minikube <span class="token function">service</span> my-fe-nginx
</code></pre><ul>
<li>now edit local hello-world.txt file</li>
<li>then refresh browser to check the change is immediately applied</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>dashboard</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>minikube <span class="token function">ip</span>
minikube dashboard <span class="token parameter variable">--url</span>
        http://127.0.0.1:45583/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>minikube ingress</li>
</ul>
<p><a href="https://stackoverflow.com/a/73735009">https://stackoverflow.com/a/73735009</a></p>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># minikube start --cpus 4 --memory 4096</span>
minikube start
minikube addons <span class="token builtin class-name">enable</span> ingress
minikube addons <span class="token builtin class-name">enable</span> ingress-dns

<span class="token comment"># Wait until you see the ingress-nginx-controller-XXXX is up and running using Kubectl get pods -n ingress-nginx</span>
<span class="token comment"># Create an ingress using the K8s example yaml file</span>
<span class="token comment"># Update the service section to point to the NodePort Service that you already created</span>
<span class="token comment"># Append 127.0.0.1 hello-world.info to your /etc/hosts file on MacOS (NOTE: Do NOT use the Minikube IP)</span>

<span class="token comment"># ( Keep the window open. After you entered the password there will be no more messages, and the cursor just blinks)</span>
minikube tunnel

<span class="token comment"># Hit the hello-world.info ( or whatever host you configured in the yaml file) in a browser and it should work</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<p>Here's a high-level overview of the traffic flow when you access <code>http://localhost</code> in your setup:</p>
<ol>
<li>
<p><strong>Browser Request</strong>: When you type <code>http://localhost</code> into your browser and hit enter, your browser sends a HTTP request to <code>localhost</code>, which is resolved to the IP address <code>127.0.0.1</code>.</p>
</li>
<li>
<p><strong>Port Forwarding</strong>: Since you've set up port forwarding with the command <code>kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 80:80</code>, the request to <code>localhost</code> on port 80 is forwarded to port 80 on the <code>ingress-nginx-controller</code> service.</p>
</li>
</ol>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code> k get svc <span class="token parameter variable">-n</span> ingress-nginx
    NAME                                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT<span class="token punctuation">(</span>S<span class="token punctuation">)</span>
        AGE
    ingress-nginx-controller             NodePort    <span class="token number">10.109</span>.183.14    <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>        <span class="token number">80</span>:31078/TCP,443:31420/TCP   6m17s
    ingress-nginx-controller-admission   ClusterIP   <span class="token number">10.110</span>.101.115   <span class="token operator">&lt;</span>none<span class="token operator">&gt;</span>        <span class="token number">443</span>/TCP                      6m17s

<span class="token comment"># k port-forward deployment/fe-nginx-deployment 80</span>
<span class="token comment"># localhost:8080 -&gt; ingress controller on 80</span>
k port-forward <span class="token parameter variable">-n</span> ingress-nginx svc/ingress-nginx-controller <span class="token number">80</span>:80
</code></pre><p>The need for port-forwarding arises due to the way Kubernetes networking and Minikube are structured. Here's a breakdown of why you might need to use port-forwarding and why direct access might not work without it:</p>
<h3 id="why-direct-access-might-not-work">Why Direct Access Might Not Work </h3>
<p>2-1. <strong>Network Isolation:</strong></p>
<ul>
<li><strong>Kubernetes Networking:</strong> Kubernetes clusters are designed to have an isolated network. Services within the cluster communicate with each other via internal cluster IPs that are not accessible from the outside world directly.</li>
<li><strong>Minikube Networking:</strong> Minikube sets up a local virtual machine (VM) on your computer. This VM has its own network namespace, separate from your host machine's network. The services running inside Minikube are isolated from your host machine by default.</li>
</ul>
<p>2-2. <strong>ClusterIP Services:</strong></p>
<ul>
<li><strong>ClusterIP Type:</strong> The services you've listed (<code>be-go-service</code>, <code>be-py-service</code>, <code>fe-nginx-service</code>, and <code>kubernetes</code>) are of type <code>ClusterIP</code>. This means they are only accessible within the cluster. External traffic from your host machine cannot reach these services directly.</li>
</ul>
<p>2-3. <strong>Minikube IP Address:</strong></p>
<ul>
<li>Minikube typically runs on a virtual IP address, such as <code>192.168.49.2</code> in your case. Accessing this IP directly from your host might not be straightforward due to network isolation.</li>
</ul>
<h3 id="why-port-forwarding-is-needed">Why Port-Forwarding is Needed </h3>
<p>Port-forwarding provides a bridge between your host machine and the Kubernetes cluster, allowing you to access cluster services from your local machine as if they were running locally.</p>
<ul>
<li>
<p><strong>Accessing Cluster Services:</strong></p>
<ul>
<li>Port-forwarding allows you to map a port on your local machine to a port on a pod or service within the cluster. This makes it possible to access cluster services using <code>localhost</code> on your host machine.</li>
</ul>
</li>
<li>
<p><strong>Bypassing Network Isolation:</strong></p>
<ul>
<li>By forwarding a port, you bypass the network isolation of the cluster, making it possible to communicate with services running inside Minikube directly from your host.</li>
</ul>
</li>
</ul>
<h3 id="alternative-approaches">Alternative Approaches </h3>
<p>If you prefer not to use port-forwarding, there are other approaches you can consider:</p>
<ul>
<li>
<p><strong>Minikube Tunnel:</strong></p>
<ul>
<li>Minikube provides a <code>minikube tunnel</code> command that can create a network tunnel to your cluster, making services of type <code>LoadBalancer</code> accessible from your host machine.</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>minikube tunnel
</code></pre></li>
<li>
<p><strong>NodePort Services:</strong></p>
<ul>
<li>Change the service type to <code>NodePort</code>, which exposes the service on a port on each node of the cluster. You can then access the service using the Minikube IP and the NodePort.</li>
</ul>
<p>Example of changing a service to NodePort:</p>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token key atrule">apiVersion</span><span class="token punctuation">:</span> v1
<span class="token key atrule">kind</span><span class="token punctuation">:</span> Service
<span class="token key atrule">metadata</span><span class="token punctuation">:</span>
  <span class="token key atrule">name</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx<span class="token punctuation">-</span>service
<span class="token key atrule">spec</span><span class="token punctuation">:</span>
  <span class="token key atrule">type</span><span class="token punctuation">:</span> NodePort
  <span class="token key atrule">ports</span><span class="token punctuation">:</span>
    <span class="token punctuation">-</span> <span class="token key atrule">port</span><span class="token punctuation">:</span> <span class="token number">8080</span>
      <span class="token key atrule">targetPort</span><span class="token punctuation">:</span> <span class="token number">8080</span>
      <span class="token key atrule">nodePort</span><span class="token punctuation">:</span> <span class="token number">30080</span>  <span class="token comment"># Example NodePort</span>
  <span class="token key atrule">selector</span><span class="token punctuation">:</span>
    <span class="token key atrule">app</span><span class="token punctuation">:</span> fe<span class="token punctuation">-</span>nginx
</code></pre></li>
<li>
<p><strong>Ingress with Minikube IP:</strong></p>
<ul>
<li>You can use the Minikube IP address and configure your <code>/etc/hosts</code> file to point <code>localhost</code> to the Minikube IP.</li>
</ul>
</li>
</ul>
<h3 id="summary">Summary </h3>
<p>Using <code>kubectl port-forward</code> is a convenient and straightforward way to access your services without altering service types or cluster configurations. It helps bridge the network isolation between your host machine and the Kubernetes cluster set up by Minikube.</p>
<ol start="3">
<li>
<p><strong>Ingress Controller</strong>: The Ingress Controller, which is part of the <code>ingress-nginx-controller</code> service, receives the request. The Ingress Controller is responsible for routing the request based on the rules defined in your Ingress resource.</p>
</li>
<li>
<p><strong>Ingress Rules</strong>: In your case, you've set up an Ingress rule to route traffic to the <code>nginx-service</code> service on port 80 when the host is <code>simple-app.com</code>. However, since you're accessing <code>localhost</code> and not <code>simple-app.com</code>, this rule does not apply.</p>
</li>
<li>
<p><strong>Service</strong>: If there were a matching Ingress rule, the Ingress Controller would forward the request to the <code>nginx-service</code> service on port 80.</p>
</li>
<li>
<p><strong>Pod</strong>: The service then load balances the request to one of the pods that match its selector. In your case, this would be the pod running the Nginx application.</p>
</li>
</ol>
<p>Please note that since you're accessing <code>localhost</code> and not <code>simple-app.com</code>, the Ingress rule does not apply, and the request will not be routed to your Nginx application. To access your application, you need to either use <code>simple-app.com</code> as the host or modify your Ingress rule to match <code>localhost</code>.</p>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="microk8s-implemntation">Microk8s implemntation </h3>
<ul>
<li>install microk8s (Ubuntu)</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token comment"># 1.27/stable version ERROR -&gt; install --classic</span>
<span class="token function">sudo</span> snap <span class="token function">install</span> microk8s <span class="token parameter variable">--classic</span>

<span class="token comment"># 일반유저에게 microk8s 커맨드 권한 부여</span>
<span class="token comment"># NOTE: root유저로만 microk8s 커맨드 사용시 아래 커맨드 필요 X</span>
<span class="token function">sudo</span> <span class="token function">usermod</span> <span class="token parameter variable">-a</span> <span class="token parameter variable">-G</span> microk8s <span class="token environment constant">$USER</span>
<span class="token function">sudo</span> <span class="token function">chown</span> <span class="token parameter variable">-f</span> <span class="token parameter variable">-R</span> <span class="token environment constant">$USER</span> ~/.kube

microk8s.status --wait-ready
microk8s kubectl get no
microk8s kubectl get svc

<span class="token function">cat</span> <span class="token operator">&gt;&gt;</span> ~/.bashrc <span class="token operator">&lt;&lt;-</span><span class="token string">EOF

alias k='microk8s.kubectl'
EOF</span>

<span class="token builtin class-name">source</span> ~/.bashrc


microk8s start

<span class="token comment"># Join node (All 3 are master nodes)</span>
<span class="token function">sudo</span> <span class="token function">su</span> -
<span class="token function">vim</span> /etc/hosts

<span class="token function">cat</span> <span class="token operator">&gt;&gt;</span> /etc/hosts <span class="token operator">&lt;&lt;-</span><span class="token string">EOF

10.0.2.3 ubuntu-1
10.0.2.4 ubuntu-2
10.0.2.5 ubuntu-3
EOF</span>

<span class="token comment"># On each vms</span>
<span class="token function">ssh</span> foo@10.0.2.3
<span class="token function">ssh</span> foo@10.0.2.4
<span class="token function">ssh</span> foo@10.0.2.5


<span class="token comment"># in first node</span>
microk8s add-node

<span class="token comment"># in other 2 nodes</span>
microk8s <span class="token function">join</span> <span class="token punctuation">[</span>TOKEN<span class="token punctuation">]</span>

<span class="token comment"># Trouble shoot</span>
<span class="token comment"># https://microk8s.io/docs/restore-quorum</span>
<span class="token function">vim</span> /var/snap/microk8s/current/var/kubernetes/backend/cluster.yaml

- Address: <span class="token number">172.16</span>.9.201:19001
    ID: <span class="token number">3297041220608546238</span>
    Role: <span class="token number">0</span>
- Address: <span class="token number">172.16</span>.9.202:19001
    ID: <span class="token number">13629670026737620399</span>
    Role: <span class="token number">0</span>
- Address: <span class="token number">172.16</span>.9.203:19001
    ID: <span class="token number">10602814967080190144</span>
    Role: <span class="token number">0</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>Trouble-shooting
<ul>
<li>diagnosis:
<ul>
<li>deployed pods with count of 2 replicas, one on node1 and another on node3</li>
<li>calling endpoint seems to have different result for each time of calling.</li>
</ul>
</li>
<li>cause:
<ul>
<li>microk8s ctr images import was done only one node1.</li>
<li>node3 tries to pull image from public docker hub instead of local repository.</li>
<li>in result, two pods have different images: one from local repository, another from public docker repository.</li>
</ul>
</li>
</ul>
</li>
</ul>
<table>
<thead>
<tr>
<th style="text-align:center"><img src="https://imgur.com/KAUbhcq.png" alt="pods" width="700"></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"><em>pod resources</em></td>
</tr>
</tbody>
</table>
<pre data-role="codeBlock" data-info="" class="language-text"><code>k describe pod fe-nginx-deployment-7b9c5bb8f8-xlrs2
        Containers:
            fe-nginx:
                Image:                    jnuho/fe-nginx:latest
                Image ID:             sha256:2544d68d372793a21b627c360def55e648ad2cfbbf330a65ba567dbced1985f2

k describe pod fe-nginx-deployment-7b9c5bb8f8-q6d6m
        Containers:
            fe-nginx:
                Image:                    jnuho/fe-nginx:latest
                Image ID:             docker.io/jnuho/fe-nginx@sha256:48e8995cc2c86a3759ac1156cd954d8f90a1c054ae1fcd67181a77df2ff5492f

</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>Local docker registory
<ul>
<li><a href="https://microk8s.io/docs/registry-images">https://microk8s.io/docs/registry-images</a></li>
</ul>
</li>
</ul>
<pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code><span class="token function">git</span> clone https://github.com/jnuho/simpledl.git

<span class="token builtin class-name">cd</span> simpledl/script
./1.build-image.sh
./1-1.import-microk8s.sh

<span class="token function">docker</span> save jnuho/fe-nginx <span class="token operator">&gt;</span> fe-nginx.tar
<span class="token function">docker</span> save jnuho/be-go <span class="token operator">&gt;</span> be-go.tar
<span class="token function">docker</span> save jnuho/be-py <span class="token operator">&gt;</span> be-py.tar

microk8s ctr image <span class="token function">import</span> fe-nginx.tar
microk8s ctr image <span class="token function">import</span> be-go.tar
microk8s ctr image <span class="token function">import</span> be-py.tar

<span class="token function">rm</span> fe-nginx.tar
<span class="token function">rm</span> be-go.tar
<span class="token function">rm</span> be-py.tar

microk8s ctr image <span class="token function">ls</span> <span class="token operator">|</span> <span class="token function">grep</span> jnuho
</code></pre><pre data-role="codeBlock" data-info="sh" class="language-bash sh"><code>microk8s kubectl get pods <span class="token parameter variable">-A</span> <span class="token operator">|</span> <span class="token function">grep</span> ingress


telnet localhost <span class="token number">8080</span>
telnet localhost <span class="token number">3001</span>
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>Port forwarding</li>
</ul>
<pre data-role="codeBlock" data-info="" class="language-text"><code>host -&gt; virtualbox vm
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<ul>
<li>ufw setting</li>
</ul>
<pre data-role="codeBlock" data-info="" class="language-text"><code>open port 3001
</code></pre><p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="golang-ini-setting">Golang ini setting </h3>
<p>In software development, managing configurations across different environments—such as development (dev), staging (stg), and production (prd)—is crucial.</p>
<p>Each environment often requires distinct settings, such as API endpoint URLs, database connections, and environment variables.</p>
<p>Hard-coding these values directly into the application code can lead to maintenance challenges and potential errors during deployment.</p>
<ul>
<li>
<h2>Environment-Specific Values Files</h2>
</li>
</ul>
<pre data-role="codeBlock" data-info="yaml" class="language-yaml yaml"><code><span class="token comment"># One can also set different namespace for each environment on values.xxx.yaml</span>

<span class="token comment"># 1. Development envionment</span>
helm install tst<span class="token punctuation">-</span>release ./tst<span class="token punctuation">-</span>chart <span class="token punctuation">-</span>f ./tst<span class="token punctuation">-</span>chart/values.dev.yaml

<span class="token comment"># 2. Stage envionment</span>
helm install tst<span class="token punctuation">-</span>release ./tst<span class="token punctuation">-</span>chart <span class="token punctuation">-</span>f ./tst<span class="token punctuation">-</span>chart/values.stg.yaml

<span class="token comment"># 3. Production envionment</span>
helm install tst<span class="token punctuation">-</span>release ./tst<span class="token punctuation">-</span>chart <span class="token punctuation">-</span>f ./tst<span class="token punctuation">-</span>chart/values.prd.yaml
</code></pre><h3 id="aws-loadbalancer-controller">AWS LoadBalancer Controller </h3>
<ul>
<li>
<p><a href="https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html"><code>AWS document</code></a></p>
</li>
<li>
<p><a href="https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.8/how-it-works/"><code>AWS LoadBalancer Controller</code></a></p>
</li>
<li>
<p>Controller</p>
<ul>
<li>In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed.</li>
<li>Each controller tries to move the current cluster state closer to the desired state.</li>
<li>The Load Balancer Controller watches for Kubernetes Ingress or Service resources.</li>
</ul>
</li>
<li>
<p>The <code>AWS Load Balancer Controller</code> (pods in kube-system namespace) watches for changes in Kubernetes <code>Ingress</code> resources.</p>
<ul>
<li>When an Ingress resource is created or updated, the controller translates the Ingress resource into configurations for AWS ALBs or NLBs.</li>
<li>It ensures that the ALB/NLB is configured correctly to route traffic based on the rules specified in the Ingress resource.</li>
</ul>
</li>
<li>
<p>In order for this Kubernetes pod to be able to create AWS resources like ALBs(based on Kubernetes Ingress), and NLBs(based on Service resources),</p>
<ul>
<li>it needs <code>IAM Role</code> with proper policies attached to use AWS API to create and configure an ALB.</li>
<li>The AWS Load Balancer Controller, running as a pod in the <code>kube-system</code> namespace,</li>
<li>monitors for new or updated Ingress resources with the alb ingress class.</li>
</ul>
</li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>
<h3 id="references">References </h3>
<ul>
<li><a href="https://kubernetes.github.io/ingress-nginx/deploy">ingress-nginx doc 1</a></li>
<li><a href="https://docs.nginx.com/nginx-ingress-controller/overview/design/#the-nginx-ingress-controller-pod">ingress-nginx doc 2</a></li>
</ul>
<p><a href="#">↑ Back to top</a><br>
<br><br></p>

      </div>
      
      
    
    
    
    
    
    
  
    </body></html>