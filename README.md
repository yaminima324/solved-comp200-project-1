Download Link: https://assignmentchef.com/product/solved-comp200-project-1
<br>
The purpose of this project is for you to gain experience with writing and testing relatively simple procedures. You should read the project submission instructions in the Assignments section of the course website to find out how to retrieve the project file and submit your solutions. For each problem below, include your code (with identification of the problem number being solved), as well as comments and explanations of your code, and demonstrate your code’s functionality against a set of test cases. On occasion, we may provide some example test cases, but you should always create and include your own additional, meaningful test cases to ensure that your code works not only on typical inputs, but also on more difficult cases. Get in the habit of writing and running these test cases after every procedure you write — no matter how trivial the procedure may seem to you.

<h1>Scenario</h1>

Alyssa P. Hacker has just arrived in Cambridge, England, about to embark on a semester in the Cambridge exchange program. Suffering from severe culture shock, she is delighted to find that her favorite candy,

1

<em>M&amp;M’s</em>, comes in a British variant, <em>Smarties</em>. Even better, she finds that <em>Smarties </em>come in a variety of colors (colours?), and that her favorite color, orange, is well represented. Thrilled by this unexpected turn of events, she decides that she needs to develop software in an effort to optimize the number of orange smarties she can consume over the next three months.

The key to this project will be to model the way that packets of Smarties are produced. Throughout the project, we’ll assume that each Smarties packet is produced by the manufacturer, in the following random process. Each Smarties packet will contain some number, <em>n</em>, of smarties (e.g., <em>n </em>= 100). The value for <em>n </em>will be chosen by Alyssa or the manufacturer. The colors of these <em>n </em>Smarties are then chosen at random. More specifically, the probability that a randomly chosen Smartie is orange is <em>p</em>, where <em>p </em>is some value between 0 and 1. If <em>p </em>is high, there’s a good chance that there will be a large number of orange Smarties in the packet. If <em>p </em>is low, there will a good chance that there will be very few Smarties that are orange, and Alyssa will be disappointed.

<h1>Problem 1: Some Simple Probability Theory</h1>

The first thing that Alyssa would like to do is model the probability of seeing exactly <em>b </em>orange Smarties in a Smarties packet. This probability will vary depending on the number of smarties in a packet, <em>n</em>, and the probability of any one Smartie being orange, <em>p</em>. In general, the probability of seeing exactly <em>b </em>smarties is given by the following formula:

where  is defined as the binomial coefficient

!

(This result comes from the <em>binomial distribution</em>, if you’re interested in reading more about this you can see http:<em>//</em>mathworld.wolfram.com<em>/</em>BinomialDistribution.html.)

We want you to write a procedure that takes parameters <em>n </em>and <em>b </em>as input, and returns the binomial coefficient  in two different ways.

For the first method, you should be able to directly encode the formula above (i.e., write a procedure to compute factorial, and then use it to implement the formula):

(define factorial (lambda (n)

YOUR-CODE-HERE))

(define binomial (lambda (n b)

YOUR-CODE-HERE))

Test your code for at least the following cases:

(binomial 5 1) ; -&gt; 5

(binomial 5 2) ; -&gt; 10

(binomial 10 5) ; -&gt; 252

As a second method, you can take advantage of properties of factorial. In particular,

Write a second version of binomial that uses this idea as its basis and does not use factorial:

(define binomial-2 (lambda (n b)

YOUR-CODE-HERE))

Test your code to show that binomial-2 in fact gives the same answers as binomial.

Building on this code, write a procedure that takes parameters <em>n</em>, <em>b</em>, and <em>p </em>as input, and returns the probability that a packet of <em>n </em>smarties has exactly <em>b </em>orange smarties, given that <em>p </em>is the probability of any single Smartie being orange:

(define exactly-b-smarties (lambda (n b p)

YOUR-CODE-HERE))

Test your code for at least the following cases (you should be able to calculate the later cases directly using a calculator, to verify that your code is producing the correct answer):

(exactly-b-smarties 1 1 0.5)                                         ; -&gt; 0.5

(exactly-b-smarties 2 1 0.5)                                         ; -&gt; 0.5

(exactly-b-smarties 2 2 0.5)                                          ; -&gt; 0.25

(exactly-b-smarties 2 1 0.3)                                       ; -&gt;

(exactly-b-smarties 10 2 0.3) ; -&gt;

Note that you might think about what checks you want to put into your code to ensure that it handles the right set of parameters. For example, what if b is greater than n?

<h1>Problem 2: More Probability Theory</h1>

Alyssa would now like to calculate the probability that there will be <em>at least </em><em>b </em>orange smarties in a bag, given that it is generated with underlying parameters <em>n </em>and <em>p</em>. Note that the probability of seeing <em>at least </em><em>b </em>orange smarties in a bag can be calculated as the probability of seeing exactly <em>b </em>orange smarties, plus the probability of seeing exactly <em>b </em>+ 1 orange smarties, and so on, up to seeing exactly <em>n </em>smarties. This can be captured mathematically as: which uses the summation notation

which applies to any function <em>f</em>(<em>r</em>).

In other words, we’ve made use of the identity

<em>Probability</em>(at least <em>b </em>smarties) = <em>Probability</em>(exactly <em>b </em>smarties) + <em>Probability</em>(exactly <em>b </em>+ 1 smarties)


<em>Probability</em>(exactly <em>b </em>+ 2 smarties)


<em>…</em>

<em>Probability</em>(exactly <em>n </em>smarties)

Making use of your code for exactly-b-smarties, write code which takes as input parameters <em>n,b, </em>and <em>p</em>, and returns the probability that at least <em>b </em>orange Smarties are found in a bag:

(define atleast-b-smarties (lambda (n b p)

YOUR-CODE-HERE))

Write your code in two different ways. In the first method, use a recursive process (i.e., rely on the fact that getting at least b smarties is the same as either getting exactly b smarties or getting at least b+1 smarties). In the second method, use an iterative process, while relying on your code to get exactly b smarties.

Test your code for at least the following cases:

(atleast-b-smarties 9 5 0.5)                                                        ; -&gt; 0.5

(atleast-b-smarties 19 10 0.5)                                                   ; -&gt; 0.5

(atleast-b-smarties 10 5 0.6)                                                   ; -&gt;

(atleast-b-smarties 15 5 0.3)                                                   ; -&gt;

<h1>Problem 3: Choosing a Bag</h1>

Alyssa is now almost ready to go shopping for Smarties. To her delight, she finds that each Smarties bag has the parameters <em>n </em>and <em>p </em>printed on it; the values for <em>n </em>and <em>p </em>may vary bag by bag. A bag costs one pound (about 2 dollars), and she decides that a bag will be worth buying as long as there’s at least a 50% chance that it will have 8 or more orange Smarties.

Write a function good-bag which takes parameters <em>n </em>and <em>p </em>as input, and returns #t if the bag is worth buying, #f if it is not worth buying. Be careful of a special case, that if <em>n &lt; </em>8 there is no chance that the bag will have 8 or more Smarties.

(define good-bag (lambda (n p)

YOUR-CODE-HERE))

Test your code for at least the following cases:

<table width="244">

 <tbody>

  <tr>

   <td width="175">(good-bag 7 1)</td>

   <td width="70">; -&gt; #f</td>

  </tr>

  <tr>

   <td width="175">(good-bag 8 1)</td>

   <td width="70">; -&gt; #t</td>

  </tr>

  <tr>

   <td width="175">(good-bag 8 0.5)</td>

   <td width="70">; -&gt; #f</td>

  </tr>

  <tr>

   <td width="175">(good-bag 8 0.99)</td>

   <td width="70">; -&gt; #t</td>

  </tr>

  <tr>

   <td width="175">(good-bag 16 0.5)</td>

   <td width="70">; -&gt;</td>

  </tr>

  <tr>

   <td width="175">(good-bag 16 0.7)</td>

   <td width="70">; -&gt;</td>

  </tr>

  <tr>

   <td width="175">(good-bag 16 0.4)</td>

   <td width="70">; -&gt;</td>

  </tr>

 </tbody>

</table>

<h1>Problem 4: Choosing a Value for <em>p</em></h1>

After a couple of months in England, Alyssa has purchased so many bags of Smarties that she has the power to directly negotiate with the manufacturer. Whenever she wants a bag of Smarties, she can call up the company, which will produce a customized bag for her. They will tell her the number of Smarties, <em>n</em>, that will appear in the bag. You can assume that <em>n </em>will be at least 8. Alyssa then gets to choose a minimum value for the probability <em>p</em>. In particular, she wants to choose the minimum value of <em>p </em>such that the bag is a “good bag”, as defined in the previous problem.

Write a function minimum-p which takes a parameter <em>n </em>as input, and returns <em>p</em>, the minimum probability under which the bag will be acceptable to Alyssa. minimum-p should be a recursive procedure that tries different values for <em>p </em>ranging from 0 to 1, sampled at some specific increment size inc (i.e., tries <em>p </em>= 0, then <em>p </em>=inc, then <em>p </em>= 2 inc, and so on), and which makes use of good-bag. The value for the increment should be an additional parameter of the function, called inc:

(define minimum-p

(lambda (n inc)

YOUR-CODE-HERE))

Test your code for the following case:

(minimum-p 12 0.01)

You should get a value of 0<em>.</em>63. To check that this is correct, what do you get for the following applications of good-bag?:

(good-bag 12 0.63)                                                       ; -&gt;

(good-bag 12 (- 0.63 0.01))                                        ; -&gt;

Now try

(minimum-p 12 0.1)

(minimum-p 12 0.01)

(minimum-p 12 0.001)

(minimum-p 12 0.0001)

(minimum-p 12 0.00001)

Create 3 other test cases that are similar to the case above.

<h1>Problem 5: Choosing <em>p </em>More Efficiently</h1>

Alyssa discovers that her code for calculating minimum-p (in Problem 4) is too slow; her telephone bill for calls to the company is becoming so big that she’s running out of money for Smarties. She decides to try to make a more efficient version of the function.

First, though, you should implement a new version of minimum-p which displays (or prints out) the number of times that good-bag is called by the recursive search procedure. Call this procedure minimum-p-new. For example, it should show the following behavior:

(minimum-p-new 12 0.01)

Number of calls to good-bag: 63

0.63000000000003

(The procedure returns the value 0.63 (roughly), and also displays or prints out 63, i.e., the number of times good-bag was called, which is ironically very similar in this case.) You may find the procedures newline (with no arguments), and display (with one argument) convenient – the former outputs a blank line, and the latter will print out the value of its argument on the screen.

Try the following test cases:

(minimum-p-new 15 0.1)

(minimum-p-new 15 0.01)

(minimum-p-new 15 0.001)

(minimum-p-new 15 0.0001)

(minimum-p-new 15 0.00001)

Alyssa realises that there’s a more efficient way of calculating minimum-p. It is based on an idea called <em>binary search</em>. First, note that we know that the value for minimum-p is between 0 and 1. Suppose we try a value of 0<em>.</em>5 (halfway between). There are then two possible outcomes:

<ul>

 <li>If a value of <em>p </em>= 0<em>.</em>5 gives a good bag, we know that the minimum value for <em>p </em>is between 0 and 0<em>.</em>5. We can then search this range of values, by recursing, and testing a value of <em>p </em>= 0<em>.</em>25.</li>

 <li>If <em>p </em>= 0<em>.</em>5 does not give a good bag, we know the minimum value for <em>p </em>is between 0<em>.</em>5 and 1. We can then search this range of values, by recursing, and testing a value of <em>p </em>= 0<em>.</em>75.</li>

</ul>

To implement this procedure, fill in the following code:

(define minimum-p-binary

(lambda (n inc)

(minimum-p-binary-helper n inc 0 1 0)))

(define minimum-p-binary-helper

(lambda (n inc a b count)

YOUR-CODE-HERE))

The procedure (minimum-p-binary-helper n inc a b count) should implement binary search for the best value of <em>p </em>between <em>a </em>and <em>b</em>, up to a level of precision defined by inc. If (<em>b </em>− <em>a</em>) <em>&lt; inc</em>, then it should just return <em>b </em>as its final answer. Otherwise, it should test whether a value for <em>p </em>= (<em>a</em>+<em>b</em>)<em>/</em>2 leads to a good or bad bag, and make a recursive call to minimum-p-binary-helper with new values of <em>a </em>and/or <em>b </em>which depend on this answer. It should also keep track (using count) of how many times good-bag is called.

Test your code on the following cases:

(minimum-p-binary 12 0.1)

(minimum-p-binary 12 0.01)

(minimum-p-binary 12 0.001)

(minimum-p-binary 12 0.0001)

(minimum-p-binary 12 0.00001)

Your code should again print the number of times that good-bag is called when minimum-p-binary is used. You should find that it calls good-bag far fewer times than the number of times used by minimum-p-new, particularly when inc becomes small.

<h1>Problem 6: Monte-Carlo Simulations</h1>

Unfortunately, the company has a change in management, and while still willing to customize bags for Alyssa, they are slightly less flexible. The company will only produce bags in batches of some size <em>m </em>(e.g., <em>m </em>= 8) that they choose. Furthermore, they will specify the parameters <em>n </em>and <em>p </em>which are used to generate all of the bags in a given batch. Alyssa now wants to build a function (estimate-good-probability m n p) which returns the probability that at least one bag out of the <em>m </em>bags she receives will be a “good bag”, where a “good bag” is as defined before.

This is a more difficult problem, and Alyssa decides to abandon her existing code (you should too: don’t use the code developed in the previous problems!). Instead, she decides to develop an approach based on <em>Monte-Carlo </em>methods. (See http:<em>//</em>en.wikipedia.org<em>/</em>wiki<em>/</em>MonteCarlomethod for an overview of the history of Monte-Carlo methods. Monte-Carlo methods have had widespread use since their invention, one notable case being in the development of the hydrogen bomb. But Alyssa is delighted that they finally have a serious application, i.e., in orange-smartie-consumption-optimization.)

In the Monte-Carlo method we develop, the central idea will be to build a <em>simulator </em>that randomly generates batches of bags of Smarties. We can then see how often a randomly generated batch contains at least one good bag; we can use this to estimate the probability of there being at least one good bag under parameters <em>m,n,b</em>.

At the center of our approach is a function, random. Each time a call to (random) is made, it returns a value chosen <em>uniformly at random </em>from the interval between 0 and 1. Roughly speaking, this means that any real number between 0 and 1 will be returned with the same, equal probability. (Note that if you call random with an integer argument, it returns an integer selected uniformly at random from the integers between 0 and one less than the argument.)

Try calling (random) a few times in the read-eval-print loop: you should find a random value between 0 and 1 returned each time.

The first function you should write is (coin-toss p). This takes a parameter <em>p </em>which is between 0 and

<ol>

 <li>1. With probability <em>p </em>it returns #t, with probability (1 − <em>p</em>) it returns #f:</li>

</ol>

(define coin-toss (lambda (p)

YOUR-CODE-HERE))

Thus this is the simplest form of simulator: (coin-toss p) simulates a coin being tossed that has probability <em>p </em>of turning up heads, and probability (1−<em>p</em>) of turning up tails. It returns #t or #f for heads/tails respectively. (Hint: use (random) to generate a number between 0 and 1, and then test whether this number is ≥ <em>p</em>.)

Next, write a function random-bag which takes parameters <em>n </em>and <em>p </em>as input. The function should generate a bag of Smarties of size <em>n </em>where each Smartie has probability <em>p </em>of being orange. It returns a single value, which is the number of Smarties in the bag which were orange.

(define random-bag (lambda (n p)

YOUR-CODE-HERE))

Your code should make use of <em>n </em>calls to coin-toss.

Next, write a function get-m-bags which takes parameters <em>m</em>, <em>n </em>and <em>p </em>as input. It should generate <em>m </em>bags at random using the parameters <em>n </em>and <em>p</em>, and return #t if at least one of these bags is good, i.e. has 8 or more orange smarties.

(define get-m-bags (lambda (m n p)

YOUR-CODE-HERE))

Finally, write code estimate-good-probability which takes parameters <em>m</em>, <em>n</em>, <em>p </em>and <em>t </em>as input. As before, <em>m </em>is the number of bags in a batch; <em>n </em>is the number of Smarties in a bag; and <em>p </em>is the probability of any individual Smartie being orange. The function should make <em>t </em>calls to get-m-bags, and return  as its estimate, where <em>g </em>is the number of times get-m-bags returns true.

(define estimate-good-probability

(lambda (m n p t)

YOUR-CODE-HERE))

Give values that your code returns for the following cases:

(estimate-good-probability 24 12 0.5 1000)

(estimate-good-probability 24 16 0.5 1000)

(estimate-good-probability 24 16 0.3 1000)

(estimate-good-probability 24 16 0.2 1000)

Note: you should report numbers for 3 runs of each case. Note that because the procedure makes use of random sampling, you’ll almost certainly get slightly different answers in different runs with the same parameter values!

<h1>Problem 7: Monte-Carlo Again</h1>

Now write a new Monte-Carlo simulator for the following scenario. The company will again produce bags in batches of some size <em>m </em>that they choose; each bag will again have <em>n </em>Smarties. With probability <em>p</em>, each individual Smartie will be orange; with probability <em>q</em>, it will be blue; with probability 1 − <em>p </em>− <em>q </em>it will be some other color. Alyssa dislikes blue Smarties with a vengeance, and now defines a good bag to be any bag which has <em>more than half of the smarties of orange color and less than one-fifth of the smarties of blue color</em>. Alyssa now wants to build a function (estimate-good-probability-2 m n p q t) which returns the probability that at least one bag out of the <em>m </em>bags she receives will be a “good bag”, where a “good bag” now has the new definition. As before, <em>t </em>is a parameter specifying the number of batches which are generated at random during the Monte-Carlo simulation.

Hint: use the same logic to build up your solution as you did in problem 6. Note however that your solution may require new functions, or may require substantially new versions of the functions in problem 6.