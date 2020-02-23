---
title: SPLash
---

The <a href="http://www.php.net/manual/en/intro.spl.php">Standard PHP Library (SPL)</a> provides various utility classes and interfaces to address common problems. Some of the most visible solutions center around the <a href="http://www.php.net/manual/en/spl.iterators.php">SPL Iterators</a>. The ability to iterate over a non-array collection and then to iterate over that iterator creates an interesting design pattern for building with PHP. However, the iterators deprioritize conciseness and therefore (to some degree) readability.

<a href="https://github.com/wittiws/splash"><img alt="Fork me on GitHub" src="https://s3.amazonaws.com/github/ribbons/forkme_right_red_aa0000.png" style="position: absolute; top: 0; right: 0; border: 0;" /></a>

## Example Default SPL Iterator Usage

This example is extracted from the <a href="http://www.php.net/manual/en/class.recursivedirectoryiterator.php">PHP manual</a>.

```php 
$objects = new RegexIterator(new RecursiveIteratorIterator(
  new RecursiveDirectoryIterator($path), RecursiveIteratorIterator::SELF_FIRST),
  '/^.+\.php$/i');
foreach ($objects as $object) {}
```

As with any non-chainable procedural code, you have to read this from the inside out in an unnatural and error-prone way.

## Example Splash Alternative

<pre class="brush:php">
\Splash\Splash::mount();
$objects = splash($path)-&gt;recursiveDirectory()
  -&gt;recursiveIterator(RecursiveIteratorIterator::SELF_FIRST)
  -&gt;regex('/^.+\.php$/i');
foreach ($objects as $object) {}</pre>
<p>The value of $object should be identical within the foreach loop compared to the approach above. However, the layers of iterators and their corresponding constructor values are now organized linearly and with less code to improve readability. Ultimately, that is the singular purpose of Splash - to leverage the benefits of chaining in the context of Iterators.</p>
<h2>
	Getting Started</h2>
<ol><li>
		Install using composer: <a href="https://packagist.org/packages/wittiws/splash">wittiws/splash</a>.</li>
	<li>
		Create splash objects via one of these methods:
		<ol><li>
				$splash = new \Splash\Splash();<br />
				This is a basic approach.</li>
			<li>
				$splash = \Splash\Splash::go();<br />
				This returns a Splash object that allows you to immediately chain.</li>
			<li>
				\Splash\Splash::mount();<br />
				This makes the \splash() global function available for you to use for even more succinct coding. It creates a Splash object, and any arguments are added to an ArrayIterator that is thrown into the initial object via the push() method.</li>
		</ol></li>
	<li>
		Equivalent examples:
		<ol><li>
				use Splash\Splash;<br />
				$test = new Splash();<br />
				$test-&gt;push(1)-&gt;push(2)-&gt;push(3);</li>
			<li>
				use Splash\Splash;<br />
				$test = Splash::go()-&gt;push(1)-&gt;push(2)-&gt;push(3);</li>
			<li>
				use Splash\Splash;<br />
				$test = Splash::go()-&gt;push(1, 2, 3);</li>
			<li>
				\Splash\Splash::mount();<br />
				$test = splash(1, 2, 3);</li>
		</ol></li>
</ol><p><a href="https://github.com/wittiws/splash/tree/master/src/Tests">For more examples, take a look at the unit tests.</a></p>
</div></div></div>  </div>
</div>