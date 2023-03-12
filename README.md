<!DOCTYPE html>


</head>

<body class="fullcontent">

<div id="quarto-content" class="page-columns page-rows-contents page-layout-article">

<main class="content" id="quarto-document-content">

<header id="title-block-header" class="quarto-title-block default">
<div class="quarto-title">
<h1 class="title">HW 4</h1>
</div>



<div class="quarto-title-meta">

    
  
    
  </div>
  

</header>

<section id="homework-4" class="level2">
<h2 class="anchored" data-anchor-id="homework-4">Homework 4</h2>
<section id="question-1" class="level3">
<h3 class="anchored" data-anchor-id="question-1">Question 1</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb1"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a>d <span class="ot">&lt;-</span> <span class="fu">read.csv</span>(<span class="st">"sipp1991.csv"</span>)</span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="co">#regress net financial assets on coavriates</span></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a>nfa_reg <span class="ot">&lt;-</span> <span class="fu">glm</span>(net_tfa <span class="sc">~</span> age <span class="sc">+</span> inc <span class="sc">+</span> e401, <span class="at">data =</span> d)</span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a><span class="fu">summary</span>(nfa_reg)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>
Call:
glm(formula = net_tfa ~ age + inc + e401, data = d)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-513824   -17908    -3978     9917  1306418  

Coefficients:
              Estimate Std. Error t value Pr(&gt;|t|)    
(Intercept) -5.551e+04  3.404e+03 -16.310  &lt; 2e-16 ***
age          9.417e+02  7.781e+01  12.103  &lt; 2e-16 ***
inc          8.748e-01  3.505e-02  24.959  &lt; 2e-16 ***
e401         5.135e+03  1.754e+03   2.927  0.00343 ** 
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for gaussian family taken to be 3236949127)

    Null deviance: 1.9335e+13  on 4999  degrees of freedom
Residual deviance: 1.6172e+13  on 4996  degrees of freedom
AIC: 123685

Number of Fisher Scoring iterations: 2</code></pre>
</div>
<div class="sourceCode cell-code" id="cb3"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb3-1"><a href="#cb3-1" aria-hidden="true" tabindex="-1"></a><span class="co">#coefficient on offered enrollment</span></span>
<span id="cb3-2"><a href="#cb3-2" aria-hidden="true" tabindex="-1"></a>initial_e401 <span class="ot">&lt;-</span> <span class="fu">coef</span>(<span class="fu">summary</span>(nfa_reg))[<span class="st">"e401"</span>,]</span>
<span id="cb3-3"><a href="#cb3-3" aria-hidden="true" tabindex="-1"></a>initial_e401</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>    Estimate   Std. Error      t value     Pr(&gt;|t|) 
5.135374e+03 1.754192e+03 2.927487e+00 3.432553e-03 </code></pre>
</div>
</div>
<p>A) The fact the coefficient in front of e401 is positive tells us that if someone is working for a company that offers a 401k plan, then they are likely to have higher net total assets (NTA) compared to someone that works at a company that doesn’t offer a 401k plan. Specifically, they are expected to have $5134.74 more in NTA compared to someone who’s job does not offer a 401k plan, all other things equal.</p>
<p>B) However, this estimate cannot be interpreted causally because there are countless omitted variables that effect both someones wealth as well as the type of companies that offer 401k plans. For example, larger companies are more likely to offer 401k plans to their employees though they are also more likely to pay their employees more. Therefore the difference in NTA that we observe could be due to the fact that people that work at larger companies are getting paid more and thus have higher NTA irregardless of whether they do or don’t use their companies 401k plan.</p>
<p>C) If it is true that people primarily choose their job based on salary, then this would support the previous argument that the correlation of NTA and companies offering 401k plans is not causally driven but rather a correlation of circumstance. People are choosing jobs that pay them more and thus have a higher NTA, however they are also being offered a 401k. Since we can safely assume that being offered an employee 401k is positively correlated with both the amount someone is paid and their NTA, we can see that the magnitude of this coefficient is likely driven by correlation and not causation.</p>
</section>
<section id="question-2" class="level3">
<h3 class="anchored" data-anchor-id="question-2">Question 2</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb5"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb5-1"><a href="#cb5-1" aria-hidden="true" tabindex="-1"></a><span class="co">#coef on age</span></span>
<span id="cb5-2"><a href="#cb5-2" aria-hidden="true" tabindex="-1"></a>nfa_reg<span class="sc">$</span>coefficients[<span class="st">"age"</span>]</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>    age 
941.713 </code></pre>
</div>
</div>
<p>A) The coefficient on age argues that an additional year of age leads to an increase of $941.71 in NTA, ceterus paribus. This is likely not the case in reality because the amount of someones NTA varies nonlinearly over the course of someones life. A kid going from 9 to 10 is not likely to add $941 to their net total wealth and a 55 year-old person who is deep in their career may add a significantly larger amount than $941 to their NTA as they save for retirement and pay the mortgage on their house.</p>
<p>B)</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb7"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb7-1"><a href="#cb7-1" aria-hidden="true" tabindex="-1"></a><span class="co">#convert to factors</span></span>
<span id="cb7-2"><a href="#cb7-2" aria-hidden="true" tabindex="-1"></a>d<span class="sc">$</span>age <span class="ot">&lt;-</span> <span class="fu">factor</span>(d<span class="sc">$</span>age) </span>
<span id="cb7-3"><a href="#cb7-3" aria-hidden="true" tabindex="-1"></a>d<span class="sc">$</span>educ <span class="ot">&lt;-</span> <span class="fu">factor</span>(d<span class="sc">$</span>educ)</span>
<span id="cb7-4"><a href="#cb7-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-5"><a href="#cb7-5" aria-hidden="true" tabindex="-1"></a><span class="co">#creates df without our Y and D for post-lasso</span></span>
<span id="cb7-6"><a href="#cb7-6" aria-hidden="true" tabindex="-1"></a>d_sub <span class="ot">&lt;-</span> <span class="fu">subset</span>(d, <span class="at">select =</span> <span class="sc">-</span><span class="fu">c</span>(net_tfa, e401))</span>
<span id="cb7-7"><a href="#cb7-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-8"><a href="#cb7-8" aria-hidden="true" tabindex="-1"></a><span class="co">#covariate matrix</span></span>
<span id="cb7-9"><a href="#cb7-9" aria-hidden="true" tabindex="-1"></a><span class="co">#Let us try the following set of controls for our problem: indicators for age (i.e. #convert to a factor), indicators for education, an 8th-order polynomial of income, #an 8th-order polynomial of family size, all remaining variables in the dataset, and #finally, interactions between all of the above (use (X1+X2+X3)^2 to include all #interactions between X1, X2, and X3).</span></span>
<span id="cb7-10"><a href="#cb7-10" aria-hidden="true" tabindex="-1"></a>adv_poly <span class="ot">&lt;-</span> <span class="fu">model.matrix</span>( <span class="sc">~</span> (<span class="fu">poly</span>(inc, <span class="dv">8</span>, <span class="at">raw =</span> <span class="cn">TRUE</span>) <span class="sc">+</span> <span class="fu">poly</span>(fsize, <span class="dv">8</span>, <span class="at">raw =</span> <span class="cn">TRUE</span>) <span class="sc">+</span> .)<span class="sc">^</span><span class="dv">2</span>, <span class="at">data =</span> d_sub)[,<span class="sc">-</span><span class="dv">1</span>]</span>
<span id="cb7-11"><a href="#cb7-11" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-12"><a href="#cb7-12" aria-hidden="true" tabindex="-1"></a><span class="co">#dimensions of matrix</span></span>
<span id="cb7-13"><a href="#cb7-13" aria-hidden="true" tabindex="-1"></a><span class="fu">cat</span>(<span class="st">"There are"</span>, <span class="fu">dim</span>(adv_poly)[<span class="dv">2</span>], <span class="st">"columns and"</span>, <span class="fu">dim</span>(adv_poly)[<span class="dv">1</span>], </span>
<span id="cb7-14"><a href="#cb7-14" aria-hidden="true" tabindex="-1"></a>    <span class="st">"observations in the model matrix"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>There are 2307 columns and 5000 observations in the model matrix</code></pre>
</div>
</div>
<p>C)</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb9"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb9-1"><a href="#cb9-1" aria-hidden="true" tabindex="-1"></a><span class="fu">library</span>(gamlr)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>Loading required package: Matrix</code></pre>
</div>
<div class="sourceCode cell-code" id="cb11"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb11-1"><a href="#cb11-1" aria-hidden="true" tabindex="-1"></a><span class="fu">set.seed</span>(<span class="dv">0</span>)</span>
<span id="cb11-2"><a href="#cb11-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-3"><a href="#cb11-3" aria-hidden="true" tabindex="-1"></a>y_model <span class="ot">&lt;-</span> <span class="fu">cv.gamlr</span>(adv_poly, d<span class="sc">$</span>net_tfa) <span class="co"># X on Y(savings)</span></span>
<span id="cb11-4"><a href="#cb11-4" aria-hidden="true" tabindex="-1"></a>d_model <span class="ot">&lt;-</span> <span class="fu">cv.gamlr</span>(adv_poly, d<span class="sc">$</span>e401) <span class="co"># X on D(offered 401k)</span></span>
<span id="cb11-5"><a href="#cb11-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-6"><a href="#cb11-6" aria-hidden="true" tabindex="-1"></a><span class="co">#get nonzero coeffs from both</span></span>
<span id="cb11-7"><a href="#cb11-7" aria-hidden="true" tabindex="-1"></a>d_nonzero_coef_ind <span class="ot">&lt;-</span> <span class="fu">which</span>(<span class="fu">coef</span>(d_model, <span class="at">select =</span> <span class="st">"min"</span>)[<span class="sc">-</span><span class="dv">1</span>] <span class="sc">!=</span> <span class="dv">0</span>) <span class="co"># -1 omits the intercept</span></span>
<span id="cb11-8"><a href="#cb11-8" aria-hidden="true" tabindex="-1"></a>y_nonzero_coef_ind <span class="ot">&lt;-</span> <span class="fu">which</span>(<span class="fu">coef</span>(y_model, <span class="at">select =</span> <span class="st">"min"</span>)[<span class="sc">-</span><span class="dv">1</span>] <span class="sc">!=</span> <span class="dv">0</span>)</span>
<span id="cb11-9"><a href="#cb11-9" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-10"><a href="#cb11-10" aria-hidden="true" tabindex="-1"></a><span class="co">#vector of nonzero columns</span></span>
<span id="cb11-11"><a href="#cb11-11" aria-hidden="true" tabindex="-1"></a>nonzero_coef_ind <span class="ot">&lt;-</span> <span class="fu">union</span>(y_nonzero_coef_ind, d_nonzero_coef_ind)</span>
<span id="cb11-12"><a href="#cb11-12" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-13"><a href="#cb11-13" aria-hidden="true" tabindex="-1"></a><span class="co">#create new df of our Y(savings), D(being offered a 401k), and all selected controls</span></span>
<span id="cb11-14"><a href="#cb11-14" aria-hidden="true" tabindex="-1"></a>d_select <span class="ot">&lt;-</span> <span class="fu">data.frame</span>(<span class="at">net_tfa =</span> d<span class="sc">$</span>net_tfa, <span class="at">e401 =</span> d<span class="sc">$</span>e401, <span class="fu">as.matrix</span>(adv_poly[,nonzero_coef_ind]))</span>
<span id="cb11-15"><a href="#cb11-15" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-16"><a href="#cb11-16" aria-hidden="true" tabindex="-1"></a><span class="co">#OLS post-lasso reg</span></span>
<span id="cb11-17"><a href="#cb11-17" aria-hidden="true" tabindex="-1"></a>ols_post_lasso <span class="ot">&lt;-</span> <span class="fu">glm</span>(net_tfa <span class="sc">~</span> ., <span class="at">data =</span> d_select)</span>
<span id="cb11-18"><a href="#cb11-18" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-19"><a href="#cb11-19" aria-hidden="true" tabindex="-1"></a><span class="co">#number of covariates used</span></span>
<span id="cb11-20"><a href="#cb11-20" aria-hidden="true" tabindex="-1"></a><span class="fu">cat</span>(<span class="st">"The total number of covariates used in our Post-Lasso OLS regression is"</span>, <span class="fu">length</span>(nonzero_coef_ind))</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>The total number of covariates used in our Post-Lasso OLS regression is 18</code></pre>
</div>
<div class="sourceCode cell-code" id="cb13"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb13-1"><a href="#cb13-1" aria-hidden="true" tabindex="-1"></a><span class="co">#get summary for e401 using post lasso</span></span>
<span id="cb13-2"><a href="#cb13-2" aria-hidden="true" tabindex="-1"></a>post_e401 <span class="ot">&lt;-</span> <span class="fu">coef</span>(<span class="fu">summary</span>(ols_post_lasso))[<span class="st">"e401"</span>,]</span>
<span id="cb13-3"><a href="#cb13-3" aria-hidden="true" tabindex="-1"></a>post_e401</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>     Estimate    Std. Error       t value      Pr(&gt;|t|) 
-3272.6806158  2419.2721594    -1.3527542     0.1761956 </code></pre>
</div>
<div class="sourceCode cell-code" id="cb15"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb15-1"><a href="#cb15-1" aria-hidden="true" tabindex="-1"></a>compare <span class="ot">&lt;-</span> <span class="fu">data.frame</span>(initial_e401, post_e401)</span>
<span id="cb15-2"><a href="#cb15-2" aria-hidden="true" tabindex="-1"></a>compare</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>           initial_e401     post_e401
Estimate   5.135374e+03 -3272.6806158
Std. Error 1.754192e+03  2419.2721594
t value    2.927487e+00    -1.3527542
Pr(&gt;|t|)   3.432553e-03     0.1761956</code></pre>
</div>
</div>
<p>After running our Post-Lasso regression we get a coefficient on the effect of a company offering a 401k plan that is vastly different than our initial estimate. The sign has completely changed and estimate is no longer statistically significant.</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb17"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb17-1"><a href="#cb17-1" aria-hidden="true" tabindex="-1"></a><span class="co">#create a copy of our initial dataset</span></span>
<span id="cb17-2"><a href="#cb17-2" aria-hidden="true" tabindex="-1"></a>d_TREAT <span class="ot">&lt;-</span> d</span>
<span id="cb17-3"><a href="#cb17-3" aria-hidden="true" tabindex="-1"></a><span class="co">#convert the treatment vars all to 1</span></span>
<span id="cb17-4"><a href="#cb17-4" aria-hidden="true" tabindex="-1"></a>d_TREAT<span class="sc">$</span>e401 <span class="ot">&lt;-</span> <span class="dv">1</span></span>
<span id="cb17-5"><a href="#cb17-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-6"><a href="#cb17-6" aria-hidden="true" tabindex="-1"></a><span class="co">#create another model matrix for prediction using our new d_TREAT df</span></span>
<span id="cb17-7"><a href="#cb17-7" aria-hidden="true" tabindex="-1"></a>adv_poly_TREAT <span class="ot">&lt;-</span> <span class="fu">model.matrix</span>( <span class="sc">~</span> (<span class="fu">poly</span>(inc, <span class="dv">8</span>, <span class="at">raw =</span> <span class="cn">TRUE</span>) <span class="sc">+</span> <span class="fu">poly</span>(fsize, <span class="dv">8</span>, <span class="at">raw =</span> <span class="cn">TRUE</span>) <span class="sc">+</span> .)<span class="sc">^</span><span class="dv">2</span>, <span class="at">data =</span> d_TREAT)[,<span class="sc">-</span><span class="dv">1</span>]</span>
<span id="cb17-8"><a href="#cb17-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-9"><a href="#cb17-9" aria-hidden="true" tabindex="-1"></a><span class="co">#turns matrix into df for predict command</span></span>
<span id="cb17-10"><a href="#cb17-10" aria-hidden="true" tabindex="-1"></a>adv_poly_TREAT <span class="ot">&lt;-</span> <span class="fu">data.frame</span>(adv_poly_TREAT)</span>
<span id="cb17-11"><a href="#cb17-11" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-12"><a href="#cb17-12" aria-hidden="true" tabindex="-1"></a><span class="co">#avg savings for all if everyone was offered 401k</span></span>
<span id="cb17-13"><a href="#cb17-13" aria-hidden="true" tabindex="-1"></a>cfact_avg_sav <span class="ot">&lt;-</span> <span class="fu">sprintf</span>(<span class="st">"$%.2f"</span>, <span class="fu">mean</span>(<span class="fu">predict</span>(ols_post_lasso, adv_poly_TREAT)))</span>
<span id="cb17-14"><a href="#cb17-14" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-15"><a href="#cb17-15" aria-hidden="true" tabindex="-1"></a><span class="co">#avg savings for reality</span></span>
<span id="cb17-16"><a href="#cb17-16" aria-hidden="true" tabindex="-1"></a>act_sav <span class="ot">&lt;-</span> <span class="fu">sprintf</span>(<span class="st">"$%.2f"</span>, <span class="fu">mean</span>(d<span class="sc">$</span>net_tfa))</span>
<span id="cb17-17"><a href="#cb17-17" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-18"><a href="#cb17-18" aria-hidden="true" tabindex="-1"></a><span class="fu">cat</span>(<span class="st">"Our post-lasso OLS model predicts that if everyone in our sample had been offered an employee 401k program the average savings would have been"</span>, cfact_avg_sav, <span class="st">". However in reality, the average savings of everyone in our sample was"</span>, act_sav, <span class="st">". This then argues that being offered an employee 401k plan actually lowers peoples total savings as opposed to increase them."</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Our post-lasso OLS model predicts that if everyone in our sample had been offered an employee 401k program the average savings would have been $15229.70 . However in reality, the average savings of everyone in our sample was $17282.32 . This then argues that being offered an employee 401k plan actually lowers peoples total savings as opposed to increase them.</code></pre>
</div>
</div>
<p>E) If the controls from B-D were not valid for a causal interpretation then we could not pin decreased savings discovered in part D as being wholly due to someone being offered a 401k. As we discussed earlier, being offered a 401k can be correlated with a range of other variables that may themselves be a factor in determining ones savings. While we have isolated this effect in the previous question, under the assumption that our controls are not valid, we could not specifically say that being offered a 401k plan lowers someones savings. Taking a step back, that idea itself is clearly flawed. If you’re offered something that will theoretically help you save, but its predicted to actually lower your savings then there is clearly something that is being missed in the prediction.</p>
</section>
</section>

</main>
<!-- /main column -->
<script id="quarto-html-after-body" type="application/javascript">
window.document.addEventListener("DOMContentLoaded", function (event) {
  const toggleBodyColorMode = (bsSheetEl) => {
    const mode = bsSheetEl.getAttribute("data-mode");
    const bodyEl = window.document.querySelector("body");
    if (mode === "dark") {
      bodyEl.classList.add("quarto-dark");
      bodyEl.classList.remove("quarto-light");
    } else {
      bodyEl.classList.add("quarto-light");
      bodyEl.classList.remove("quarto-dark");
    }
  }
  const toggleBodyColorPrimary = () => {
    const bsSheetEl = window.document.querySelector("link#quarto-bootstrap");
    if (bsSheetEl) {
      toggleBodyColorMode(bsSheetEl);
    }
  }
  toggleBodyColorPrimary();  
  const icon = "";
  const anchorJS = new window.AnchorJS();
  anchorJS.options = {
    placement: 'right',
    icon: icon
  };
  anchorJS.add('.anchored');
  const clipboard = new window.ClipboardJS('.code-copy-button', {
    target: function(trigger) {
      return trigger.previousElementSibling;
    }
  });
  clipboard.on('success', function(e) {
    // button target
    const button = e.trigger;
    // don't keep focus
    button.blur();
    // flash "checked"
    button.classList.add('code-copy-button-checked');
    var currentTitle = button.getAttribute("title");
    button.setAttribute("title", "Copied!");
    let tooltip;
    if (window.bootstrap) {
      button.setAttribute("data-bs-toggle", "tooltip");
      button.setAttribute("data-bs-placement", "left");
      button.setAttribute("data-bs-title", "Copied!");
      tooltip = new bootstrap.Tooltip(button, 
        { trigger: "manual", 
          customClass: "code-copy-button-tooltip",
          offset: [0, -8]});
      tooltip.show();    
    }
    setTimeout(function() {
      if (tooltip) {
        tooltip.hide();
        button.removeAttribute("data-bs-title");
        button.removeAttribute("data-bs-toggle");
        button.removeAttribute("data-bs-placement");
      }
      button.setAttribute("title", currentTitle);
      button.classList.remove('code-copy-button-checked');
    }, 1000);
    // clear code selection
    e.clearSelection();
  });
  function tippyHover(el, contentFn) {
    const config = {
      allowHTML: true,
      content: contentFn,
      maxWidth: 500,
      delay: 100,
      arrow: false,
      appendTo: function(el) {
          return el.parentElement;
      },
      interactive: true,
      interactiveBorder: 10,
      theme: 'quarto',
      placement: 'bottom-start'
    };
    window.tippy(el, config); 
  }
  const noterefs = window.document.querySelectorAll('a[role="doc-noteref"]');
  for (var i=0; i<noterefs.length; i++) {
    const ref = noterefs[i];
    tippyHover(ref, function() {
      // use id or data attribute instead here
      let href = ref.getAttribute('data-footnote-href') || ref.getAttribute('href');
      try { href = new URL(href).hash; } catch {}
      const id = href.replace(/^#\/?/, "");
      const note = window.document.getElementById(id);
      return note.innerHTML;
    });
  }
  const findCites = (el) => {
    const parentEl = el.parentElement;
    if (parentEl) {
      const cites = parentEl.dataset.cites;
      if (cites) {
        return {
          el,
          cites: cites.split(' ')
        };
      } else {
        return findCites(el.parentElement)
      }
    } else {
      return undefined;
    }
  };
  var bibliorefs = window.document.querySelectorAll('a[role="doc-biblioref"]');
  for (var i=0; i<bibliorefs.length; i++) {
    const ref = bibliorefs[i];
    const citeInfo = findCites(ref);
    if (citeInfo) {
      tippyHover(citeInfo.el, function() {
        var popup = window.document.createElement('div');
        citeInfo.cites.forEach(function(cite) {
          var citeDiv = window.document.createElement('div');
          citeDiv.classList.add('hanging-indent');
          citeDiv.classList.add('csl-entry');
          var biblioDiv = window.document.getElementById('ref-' + cite);
          if (biblioDiv) {
            citeDiv.innerHTML = biblioDiv.innerHTML;
          }
          popup.appendChild(citeDiv);
        });
        return popup.innerHTML;
      });
    }
  }
});
</script>
</div> <!-- /content -->



</body></html>
