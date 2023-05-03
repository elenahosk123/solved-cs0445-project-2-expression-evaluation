Download Link: https://assignmentchef.com/product/solved-cs0445-project-2-expression-evaluation
<br>
In this assignment, you’ll be implementing the “infix-to-postfix” and “postfix evaluation” algorithms simultaneously. You will then improve upon this by implementing error detection to give error messages about inputs, rather than just crashing.

Starting point

Download and extract these materials. Contained are:

<ul>

 <li>ArrayStack.java, a stack implementation using an array.</li>

 <li>StackInterface.java, the interface ArrayStack implements.</li>

 <li>ExpressionError.java, an exception type.</li>

 <li>InfixExpressionEvaluator.java. <strong>This is the file you will modify.</strong></li>

</ul>

<em>Do not modify anything other than </em><em>InfixExpressionEvaluator.java</em><em>.</em> We will be testing it with unmodified versions of the other files.

InfixExpressionEvaluator contains a good bit of code already. <strong>You do not need to change any of the methods we wrote.</strong> Instead, you will be filling in the methods which implement the “meat” of the algorithm. Basically, search for TODO: and do those things.

There is a main in InfixExpressionEvaluator so you can run it like java InfixExpressionEvaluator. It does nothing when you first download it, but it does run.

Implementing the TODO methods

If you don’t have the book… ask your classmates.

Check out sections <strong>5.16</strong> and <strong>5.18</strong> in the book (4th ed.). Those outline what you are doing. We already did the switch-case for you; the methods you implement are the code inside those cases.

You’re going to “squish” those two algorithms into one. Rather than having an “output”, you will <strong>push the operands as you encounter them</strong> and <strong>evaluate the operators as you pop them.</strong> We’ve already given you two stacks to hold these things.

Here are the methods you must fill in. They are all called by evaluate() as it finds tokens in the input.

<ul>

 <li>handleOperand(double) – called when a number is encountered.

  <ul>

   <li>For example, 3, 900, 6.28 etc.</li>

  </ul></li>

 <li>handleName(String) – called when a name is encountered.

  <ul>

   <li>A name is a special kind of <strong>operand.</strong></li>

   <li>You must handle pi and e.

    <ul>

     <li>You can use the Java Math.PI and Math.E constants.</li>

     <li><strong>Don’t duplicate effort!</strong> You already have a method to handle an operand.</li>

    </ul></li>

   <li>For any other name, throw an ExpressionError with a descriptive message.</li>

  </ul></li>

 <li>handleOperator(char) – called when an operator is encountered.</li>

</ul>

<ul>

 <li>You must handle the following operands:</li>

</ul>

<table>

 <thead>

  <tr>

   <td><strong>Symbol</strong></td>

   <td><strong>Operation</strong></td>

   <td><strong>Precedence</strong></td>

   <td><strong>Associativity</strong></td>

  </tr>

 </thead>

 <tbody>

  <tr>

   <td>+</td>

   <td>Addition</td>

   <td>Lowest</td>

   <td>Left</td>

  </tr>

  <tr>

   <td>–</td>

   <td>Subtraction</td>

   <td>Lowest</td>

   <td>Left</td>

  </tr>

  <tr>

   <td>*</td>

   <td>Multiplication</td>

   <td>Middle</td>

   <td>Left</td>

  </tr>

  <tr>

   <td>/</td>

   <td>Division</td>

   <td>Middle</td>

   <td>Left</td>

  </tr>

  <tr>

   <td>^</td>

   <td>Exponentiation</td>

   <td>Highest</td>

   <td>Right</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Java has no exponentiation operator. You can type a ^ b in Java but it means something VERY different! Look it up. Use the pow() method instead.</li>

 <li>The ^ operator is handled a little differently from the rest. The code in section <strong>16</strong> shows this.</li>

</ul>

<ul>

 <li style="list-style-type: none;">

  <ul>

   <li style="list-style-type: none;">

    <ul>

     <li>Basically, right-associative operators are super easy to deal with.</li>

    </ul></li>

  </ul></li>

 <li>handleOpenBracket(char) – called when an open bracket is encountered.

  <ul>

   <li>You must allow (, {, and [.</li>

  </ul></li>

 <li>handleCloseBracket(char) – called when a close bracket is encountered.

  <ul>

   <li>You must allow ), }, and ].</li>

  </ul></li>

 <li>handleRemainingOperators() – called at the end of parsing.

  <ul>

   <li>After all tokens have been parsed, this is called to allow you to evaluate any operators still on the stack.</li>

  </ul></li>

</ul>

And last, you must fill in the return value of evaluate(). Right now it returns null. That’s bad. You want it to return the result of the expression evaluation.

<h3>Example inputs/outputs</h3>

Here are examples.

<h3>Suggestions</h3>

<ul>

 <li>Try just printing the arguments in each method at first.

  <ul>

   <li>That will give you an idea of what methods are called, and in what order.</li>

  </ul></li>

 <li>Then work on doing the infix-to-postfix algorithm.

  <ul>

   <li>You don’t have to do it “right” at first. Maybe just start by <em>printing</em> the output instead of evaluating.</li>

   <li>Check it against examples that you know the output for.</li>

   <li>Abstract your precedence-checking into a function like boolean isLowerPrecedence(char a, char b).

    <ul>

     <li>That way, you can print out isLowerPrecedence(‘+’, ‘*’) and make sure it’s true, etc.</li>

    </ul></li>

  </ul></li>

 <li><em>Then</em> work on evaluation.

  <ul>

   <li>Getting it to evaluate instead of printing is honestly not a lot of code.</li>

   <li>Start by testing it with simple cases like 3 + 4. Don’t go for the gold at first.</li>

  </ul></li>

</ul>

Finish this first section <em>before</em> moving onto error checking. Programs are like houses: you need a good foundation. Don’t skip steps if you run into trouble. It’s better to get a solid understanding of the algorithm and get a 70 than try to attempt everything, do poorly, and get a 50.

<h2>Error checking [30 points]</h2>

Now, your program should be able to evaluate <em>correctly-formatted</em> expressions, but people make mistakes. Right now, your program might crash if you write something like 4 + . That’s no good!

Change your code to detect problems like this and throw ExpressionError with <strong>descriptive error messages.</strong> Try everything! Try giving your expression evaluator complete garbage and see what it does! <strong>It should never crash.</strong>

<h3>Hints</h3>

<ul>

 <li><strong>Some stack operations can throw an exception.</strong> Don’t let them.

  <ul>

   <li>Avoid these by checking if the stack is empty first, and throwing an ExpressionError instead.</li>

  </ul></li>

 <li><strong>Keep track of the “last seen token”.</strong>

  <ul>

   <li>You’ll have to add a variable to the class, and set it at the end of your handle methods.</li>

   <li>Then whenever you handle a new token, you can make sure that it’s OK.</li>

   <li>This will let you detect things like:

    <ul>

     <li>two operators in a row</li>

     <li>two operands in a row</li>

     <li>empty brackets</li>

     <li>an operator right before or after a bracket</li>

     <li>etc.</li>

    </ul></li>

  </ul></li>

 <li><strong>Be sure to test all possible bracket issues.</strong>

  <ul>

   <li>Missing open brackets…</li>

   <li>Missing close brackets…</li>

   <li>Mismatched brackets…</li>

   <li>Think about <em>when</em> each of these things will occur.</li>

  </ul></li>

</ul>

<h2>Extra credit [+10 points]</h2>

You can earn <em>up to</em> 10 points of extra credit. <strong>If you do any extra credit, please follow the submission instructions for it below.</strong>

Here are some suggestions:

<ul>

 <li>Support more names by allowing the user to define names on the command line, like:</li>

</ul>

·           &gt; java InfixExpressionEvaluator beef=10·           Enter infix expression: beef * 2·           20.0

<ul>

 <li style="list-style-type: none;">

  <ul>

   <li>They should be able to define as many names as they want.</li>

   <li>Look into Map.</li>

  </ul></li>

 <li>Detect semantic errors – errors in <em>meaning.</em>

  <ul>

   <li>Divide-by-zero?</li>

   <li>Results that are too big to be represented (infinities)?</li>

  </ul></li>

 <li>Allow more features.

  <ul>

   <li>Hexadecimal numbers, like 0xDC04?</li>

   <li>More operators?

    <ul>

     <li>Check precedence/associativity tables for e.g. Java to get the right precedences.</li>

    </ul></li>

   <li>Trig functions, like sin(pi)?</li>

   <li>Negation, like -(4 * 5)?</li>

  </ul></li>

</ul>

<h2>Testing</h2>

<strong>We will be testing your code on the command line.</strong> You are welcome to use an IDE, but before submitting, please test that your Java files can be compiled and run on the command line without it.

<strong>DO NOT TURN IN CODE THAT DOES NOT COMPILE.</strong>

This is not acceptable in this class or in your following classes. Comment out the code that doesn’t compile and put comments at the top of your Java files for the grader. You may receive some partial credit for such code.

Code that crashes may also receive partial credit.