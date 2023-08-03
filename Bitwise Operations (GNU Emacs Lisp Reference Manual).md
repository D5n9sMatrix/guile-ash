<!DOCTYPE html>
<!-- saved from url=(0081)https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html -->
<html><!-- Created by GNU Texinfo 7.0.3, https://www.gnu.org/software/texinfo/ --><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

<title>Bitwise Operations (GNU Emacs Lisp Reference Manual)</title>

<meta name="description" content="Bitwise Operations (GNU Emacs Lisp Reference Manual)">
<meta name="keywords" content="Bitwise Operations (GNU Emacs Lisp Reference Manual)">
<meta name="resource-type" content="document">
<meta name="distribution" content="global">
<meta name="Generator" content="makeinfo">
<meta name="viewport" content="width=device-width,initial-scale=1">

<link rev="made" href="mailto:bug-gnu-emacs@gnu.org">
<link rel="icon" type="image/png" href="https://www.gnu.org/graphics/gnu-head-mini.png">
<meta name="ICBM" content="42.256233,-71.006581">
<meta name="DC.title" content="gnu.org">
<style type="text/css">
@import url('/software/emacs/manual.css');
</style>
</head>

<body lang="en">
<div class="section-level-extent" id="Bitwise-Operations">
<div class="nav-panel">
<p>
Next: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Math-Functions.html" accesskey="n" rel="next">Standard Mathematical Functions</a>, Previous: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Rounding-Operations.html" accesskey="p" rel="prev">Rounding Operations</a>, Up: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Numbers.html" accesskey="u" rel="up">Numbers</a> &nbsp; [<a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/index.html#SEC_Contents" title="Table of contents" rel="contents">Contents</a>][<a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Index.html" title="Index" rel="index">Index</a>]</p>
</div>
<hr>
<h3 class="section" id="Bitwise-Operations-on-Integers">3.8 Bitwise Operations on Integers</h3>
<a class="index-entry-id" id="index-bitwise-arithmetic"></a>
<a class="index-entry-id" id="index-logical-arithmetic"></a>

<p>In a computer, an integer is represented as a binary number, a
sequence of <em class="dfn">bits</em> (digits which are either zero or one).
Conceptually the bit sequence is infinite on the left, with the
most-significant bits being all zeros or all ones.  A bitwise
operation acts on the individual bits of such a sequence.  For example,
<em class="dfn">shifting</em> moves the whole sequence left or right one or more places,
reproducing the same pattern moved over.
</p>
<p>The bitwise operations in Emacs Lisp apply only to integers.
</p>
<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-ash"><span class="category-def">Function: </span><span><strong class="def-name">ash</strong> <var class="def-var-arguments">integer1 count</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-ash"> ¶</a></span></dt>
<dd><a class="index-entry-id" id="index-arithmetic-shift"></a>
<p><code class="code">ash</code> (<em class="dfn">arithmetic shift</em>) shifts the bits in <var class="var">integer1</var>
to the left <var class="var">count</var> places, or to the right if <var class="var">count</var> is
negative.  Left shifts introduce zero bits on the right; right shifts
discard the rightmost bits.  Considered as an integer operation,
<code class="code">ash</code> multiplies <var class="var">integer1</var> by
2**<var class="var">count</var>,
and then converts the result to an integer by rounding downward, toward
minus infinity.
</p>
<p>Here are examples of <code class="code">ash</code>, shifting a pattern of bits one place
to the left and to the right.  These examples show only the low-order
bits of the binary pattern; leading bits all agree with the
highest-order bit shown.  As you can see, shifting left by one is
equivalent to multiplying by two, whereas shifting right by one is
equivalent to dividing by two and then rounding toward minus infinity.
</p>
<div class="example">
<div class="group"><pre class="example-preformatted">(ash 7 1) ⇒ 14
;; <span class="r">Decimal 7 becomes decimal 14.</span>
…000111
     ⇒
…001110
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(ash 7 -1) ⇒ 3
…000111
     ⇒
…000011
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(ash -7 1) ⇒ -14
…111001
     ⇒
…110010
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(ash -7 -1) ⇒ -4
…111001
     ⇒
…111100
</pre></div></div>

<p>Here are examples of shifting left or right by two bits:
</p>
<div class="example smallexample">
<div class="group"><pre class="example-preformatted">                  ;  <span class="r">       binary values</span>
(ash 5 2)         ;   5  =  <span class="r">…000101</span>
     ⇒ 20         ;      =  <span class="r">…010100</span>
(ash -5 2)        ;  -5  =  <span class="r">…111011</span>
     ⇒ -20        ;      =  <span class="r">…101100</span>
</pre></div><div class="group"><pre class="example-preformatted">(ash 5 -2)
     ⇒ 1          ;      =  <span class="r">…000001</span>
</pre></div><div class="group"><pre class="example-preformatted">(ash -5 -2)
     ⇒ -2         ;      =  <span class="r">…111110</span>
</pre></div></div>
</dd></dl>

<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-lsh"><span class="category-def">Function: </span><span><strong class="def-name">lsh</strong> <var class="def-var-arguments">integer1 count</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-lsh"> ¶</a></span></dt>
<dd><a class="index-entry-id" id="index-logical-shift"></a>
<p><code class="code">lsh</code>, which is an abbreviation for <em class="dfn">logical shift</em>, shifts the
bits in <var class="var">integer1</var> to the left <var class="var">count</var> places, or to the right
if <var class="var">count</var> is negative, bringing zeros into the vacated bits.  If
<var class="var">count</var> is negative, then <var class="var">integer1</var> must be either a fixnum
or a positive bignum, and <code class="code">lsh</code> treats a negative fixnum as if it
were unsigned by subtracting twice <code class="code">most-negative-fixnum</code> before
shifting, producing a nonnegative result.  This quirky behavior dates
back to when Emacs supported only fixnums; nowadays <code class="code">ash</code> is a
better choice.
</p>
<p>As <code class="code">lsh</code> behaves like <code class="code">ash</code> except when <var class="var">integer1</var> and
<var class="var">count1</var> are both negative, the following examples focus on these
exceptional cases.  These examples assume 30-bit fixnums.
</p>
<div class="example smallexample">
<div class="group"><pre class="example-preformatted">                 ; <span class="r">     binary values</span>
(ash -7 -1)      ; -7 = <span class="r">…111111111111111111111111111001</span>
     ⇒ -4        ;    = <span class="r">…111111111111111111111111111100</span>
(lsh -7 -1)
     ⇒ 536870908 ;    = <span class="r">…011111111111111111111111111100</span>
</pre></div><div class="group"><pre class="example-preformatted">(ash -5 -2)      ; -5 = <span class="r">…111111111111111111111111111011</span>
     ⇒ -2        ;    = <span class="r">…111111111111111111111111111110</span>
(lsh -5 -2)
     ⇒ 268435454 ;    = <span class="r">…001111111111111111111111111110</span>
</pre></div></div>
</dd></dl>

<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-logand"><span class="category-def">Function: </span><span><strong class="def-name">logand</strong> <var class="def-var-arguments">&amp;rest ints-or-markers</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-logand"> ¶</a></span></dt>
<dd><p>This function returns the bitwise AND of the arguments: the <var class="var">n</var>th
bit is 1 in the result if, and only if, the <var class="var">n</var>th bit is 1 in all
the arguments.
</p>
<p>For example, using 4-bit binary numbers, the bitwise AND of 13 and
12 is 12: 1101 combined with 1100 produces 1100.
In both the binary numbers, the leftmost two bits are both 1
so the leftmost two bits of the returned value are both 1.
However, for the rightmost two bits, each is 0 in at least one of
the arguments, so the rightmost two bits of the returned value are both 0.
</p>
<p>Therefore,
</p>
<div class="example">
<div class="group"><pre class="example-preformatted">(logand 13 12)
     ⇒ 12
</pre></div></div>

<p>If <code class="code">logand</code> is not passed any argument, it returns a value of
−1.  This number is an identity element for <code class="code">logand</code>
because its binary representation consists entirely of ones.  If
<code class="code">logand</code> is passed just one argument, it returns that argument.
</p>
<div class="example smallexample">
<div class="group"><pre class="example-preformatted">                   ; <span class="r">       binary values</span>

(logand 14 13)     ; 14  =  <span class="r">…001110</span>
                   ; 13  =  <span class="r">…001101</span>
     ⇒ 12         ; 12  =  <span class="r">…001100</span>
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(logand 14 13 4)   ; 14  =  <span class="r">…001110</span>
                   ; 13  =  <span class="r">…001101</span>
                   ;  4  =  <span class="r">…000100</span>
     ⇒ 4          ;  4  =  <span class="r">…000100</span>
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(logand)
     ⇒ -1         ; -1  =  <span class="r">…111111</span>
</pre></div></div>
</dd></dl>

<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-logior"><span class="category-def">Function: </span><span><strong class="def-name">logior</strong> <var class="def-var-arguments">&amp;rest ints-or-markers</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-logior"> ¶</a></span></dt>
<dd><p>This function returns the bitwise inclusive OR of its arguments: the <var class="var">n</var>th
bit is 1 in the result if, and only if, the <var class="var">n</var>th bit is 1 in at
least one of the arguments.  If there are no arguments, the result is 0,
which is an identity element for this operation.  If <code class="code">logior</code> is
passed just one argument, it returns that argument.
</p>
<div class="example smallexample">
<div class="group"><pre class="example-preformatted">                   ; <span class="r">       binary values</span>

(logior 12 5)      ; 12  =  <span class="r">…001100</span>
                   ;  5  =  <span class="r">…000101</span>
     ⇒ 13         ; 13  =  <span class="r">…001101</span>
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(logior 12 5 7)    ; 12  =  <span class="r">…001100</span>
                   ;  5  =  <span class="r">…000101</span>
                   ;  7  =  <span class="r">…000111</span>
     ⇒ 15         ; 15  =  <span class="r">…001111</span>
</pre></div></div>
</dd></dl>

<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-logxor"><span class="category-def">Function: </span><span><strong class="def-name">logxor</strong> <var class="def-var-arguments">&amp;rest ints-or-markers</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-logxor"> ¶</a></span></dt>
<dd><p>This function returns the bitwise exclusive OR of its arguments: the
<var class="var">n</var>th bit is 1 in the result if, and only if, the <var class="var">n</var>th bit is
1 in an odd number of the arguments.  If there are no arguments, the
result is 0, which is an identity element for this operation.  If
<code class="code">logxor</code> is passed just one argument, it returns that argument.
</p>
<div class="example smallexample">
<div class="group"><pre class="example-preformatted">                   ; <span class="r">       binary values</span>

(logxor 12 5)      ; 12  =  <span class="r">…001100</span>
                   ;  5  =  <span class="r">…000101</span>
     ⇒ 9          ;  9  =  <span class="r">…001001</span>
</pre></div><pre class="example-preformatted">
</pre><div class="group"><pre class="example-preformatted">(logxor 12 5 7)    ; 12  =  <span class="r">…001100</span>
                   ;  5  =  <span class="r">…000101</span>
                   ;  7  =  <span class="r">…000111</span>
     ⇒ 14         ; 14  =  <span class="r">…001110</span>
</pre></div></div>
</dd></dl>

<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-lognot"><span class="category-def">Function: </span><span><strong class="def-name">lognot</strong> <var class="def-var-arguments">integer</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-lognot"> ¶</a></span></dt>
<dd><p>This function returns the bitwise complement of its argument: the <var class="var">n</var>th
bit is one in the result if, and only if, the <var class="var">n</var>th bit is zero in
<var class="var">integer</var>, and vice-versa.  The result equals −1 −
<var class="var">integer</var>.
</p>
<div class="example">
<pre class="example-preformatted">(lognot 5)
     ⇒ -6
;;  5  =  <span class="r">…000101</span>
;; <span class="r">becomes</span>
;; -6  =  <span class="r">…111010</span>
</pre></div>
</dd></dl>

<a class="index-entry-id" id="index-popcount"></a>
<a class="index-entry-id" id="index-Hamming-weight"></a>
<a class="index-entry-id" id="index-counting-set-bits"></a>
<dl class="first-deffn first-defun-alias-first-deffn">
<dt class="deffn defun-alias-deffn" id="index-logcount"><span class="category-def">Function: </span><span><strong class="def-name">logcount</strong> <var class="def-var-arguments">integer</var><a class="copiable-link" href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Bitwise-Operations.html#index-logcount"> ¶</a></span></dt>
<dd><p>This function returns the <em class="dfn">Hamming weight</em> of <var class="var">integer</var>: the
number of ones in the binary representation of <var class="var">integer</var>.
If <var class="var">integer</var> is negative, it returns the number of zero bits in
its two’s complement binary representation.  The result is always
nonnegative.
</p>
<div class="example">
<pre class="example-preformatted">(logcount 43)     ;  43 = <span class="r">…000101011</span>
     ⇒ 4
(logcount -43)    ; -43 = <span class="r">…111010101</span>
     ⇒ 3
</pre></div>
</dd></dl>

</div>
<hr>
<div class="nav-panel">
<p>
Next: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Math-Functions.html">Standard Mathematical Functions</a>, Previous: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Rounding-Operations.html">Rounding Operations</a>, Up: <a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Numbers.html">Numbers</a> &nbsp; [<a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/index.html#SEC_Contents" title="Table of contents" rel="contents">Contents</a>][<a href="https://www.gnu.org/software/emacs/manual/html_node/elisp/Index.html" title="Index" rel="index">Index</a>]</p>
</div>





</body></html>