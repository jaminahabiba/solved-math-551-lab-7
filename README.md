Download Link: https://assignmentchef.com/product/solved-math-551-lab-7
<br>
<strong>Goal: </strong>In many practical applications it is necessary to approximate a function <em>f</em>(<em>x</em>) given only a finite set of function values {(<em>x</em><sub>1</sub><em>,f</em>(<em>x</em><sub>1</sub>))<em>,</em>(<em>x</em><sub>2</sub><em>,f</em>(<em>x</em><sub>2</sub>))<em>,…,</em>(<em>x<sub>n</sub>,f</em>(<em>x<sub>n</sub></em>))}. In this lab, you will learn how to do this first by fitting a polynomial through the given data points and then by using Matlab’s interp1 command. During the lab session, your lab instructor will teach you the necessary Matlab code to complete the assignment.

<strong>What you have to submit: </strong>An M-file containing all of the commands necessary to perform the tasks described below.

<h1>Reminders About the Grading Software</h1>

Remember, the labs are graded with the help of software tools. If you do not follow the instructions, you will lose points. If the instructions ask you to assign a value to a variable, you must <strong>use the variable name given in the instructions</strong>. If the instructions ask you to make a variable named x1 and instead you make a variable named x or X or X1 or any name other than x1, the grading software will not find your variable and you <em>will </em>lose points. Required variables are listed in the lab instructions in a gray box like this:

<h2>Variables: x1, A, q</h2>

At times you will also be asked to answer questions in a comment in your M-file. You must <strong>format your text answers correctly</strong>. Questions that you must answer are shown in gray boxes in the lab. For example, if you see the instruction

Q7: What does the Matlab command lu do? your file must contain a line similar to the following somewhere

% Q7: It computes the LU decomposition of a matrix.

The important points about the formatting are

<ul>

 <li>The answer is on a single line.</li>

 <li>The first characters on the line is the comment character %.</li>

 <li>The answer is labeled in the form Q<em>n</em>:, where <em>n </em>stands for the question number from the gray box.</li>

</ul>

If you do not format your answers correctly, the grading software will not find them and you <em>will </em>lose points. <strong>Polynomials in Matlab</strong>

In Matlab, we represent polynomials through the vectors of their coefficients ordered by decreasing power. That is, a polynomial of the form

<em>p</em>(<em>x</em>) = <em>a<sub>n</sub>x<sup>n </sup></em>+ <em>a<sub>n</sub></em>−<sub>1</sub><em>x<sup>n</sup></em><sup>−1 </sup>+ ··· + <em>a</em><sub>1</sub><em>x </em>+ <em>a</em><sub>0</sub>

is represented as the vector [<em>a<sub>n</sub>,a<sub>n</sub></em><sub>−1</sub><em>,…,a</em><sub>1</sub><em>,a</em><sub>0</sub>]. (Matlab doesn’t care if this is a row or column vector.) The Matlab function polyval can be used to efficiently evaluate a polynomial <em>p</em>(<em>x</em>) at a particular value (or many values) of <em>x</em>. For example, to represent the polynomial <em>p</em>(<em>x</em>) = 3<em>x</em><sup>5 </sup>− 4<em>x</em><sup>3 </sup>+ 2<em>x </em>+ 1, we would create a

vector

&gt;&gt; p = [3, 0, -4, 0, 2, 1];

Notice the zeros in the second and fourth entries of the vector. Those indicate that the coefficients for the <em>x</em><sup>4 </sup>and <em>x</em><sup>2 </sup>terms are 0. Be careful about this point. If you ignore zero coefficients you will get the wrong polynomial.

In order to evaluate this polynomial at the point <em>x </em>= −2, we use the polyval function.

&gt;&gt; polyval(p,-2) ans =

-67

polyval also provides an efficient way to evaluate a polynomial at many points simultaneously. See if you can interpret the output of the following command. &gt;&gt; polyval( [1, 0, -1], [ 2, -1; 1, 0] ) ans =

3             0

0           -1

<h1>Tasks</h1>

Consider the following set of data points on the <em>xy</em>-plane:

(−2<em>.</em>1<em>,</em>2<em>.</em>2)<em>,</em>(−1<em>.</em>3<em>,</em>5<em>.</em>1)<em>,</em>(0<em>.</em>1<em>,</em>−1)<em>,</em>(0<em>.</em>5<em>,</em>0<em>.</em>1)<em>,</em>(1<em>.</em>4<em>,</em>0<em>.</em>6)<em>,</em>(2<em>.</em>0<em>,</em>1<em>.</em>8)<em>.                     </em>(<em>?</em>)

You will need to find a polynomial of degree at most 5 that passes through these 6 points. (Does this polynomial exist? Is it unique?) Please, complete the following steps:

<ol>

 <li>Create two row vectors x and y, containing respectively the <em>x </em>and <em>y </em>coordinates of the data points in</li>

</ol>

(<em>?</em>).

<table>

 <tbody>

  <tr>

   <td width="127"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<h2>Variables: <em>x,y</em></h2>

<ol start="2">

 <li>Assuming there exits a degree 5 polynomial which passes through the points in (<em>?</em>), write down the system of 6 linear equations representing this information, i.e. each equation in the system shows that one of the (<em>x,y</em>) pairs in (<em>?</em>) solves a certain degree 5 polynomial. (You don’t need to submit this task.)</li>

 <li>Create a variable holding the coefficient matrix <em>A </em>of the system in Task 2. Do not enter the matrix entries by hand. Instead, initialize a zero matrix of the appropriate dimension using zeros and then fill in the coefficients using a pair of for So your code will look something like this</li>

</ol>

n = length(x); A = zeros(n,n); for i=1:n for j=1:n

A(i,j) = … &lt;—- this is the part you figure out end

end

<h2>Variables: A</h2>

<ol start="4">

 <li>If you have completed the previous tasks correctly, you will have generated the coefficient matrix A for your linear system from Task 2. Notice that the constants from the right-hand side are just the entries in the row vector y. Solve the system using Matlab’s backslash operator. (You’ll need to use y’ as your constant vector, since y is a row vector.) Name the solution p (a good name for a variable holding polynomial coefficients). Variables: p</li>

 <li>At this point, it would be a good idea to compare the values of polyval(p,x) with the vector y to make sure you got the right answer. To do this, add the following commands to your script.</li>

</ol>

% error check err = max( abs( polyval(p,x) – y ) ); fprintf( ’max error in polyval = %e
’, err );

Now, when you run your script, Matlab will report the largest absolute difference between the vector y and the vector polyval(p,x). Due to errors introduced internally by rounding, this value will almost certainly not be zero, but it should be a very small number like 4.884981e-15, which is Matlab’s representation of the number 4<em>.</em>884981 × 10<sup>−15</sup>. (This step helps you check your work. There are no required output variables.)

<ol start="6">

 <li>Divide the interval [−2<em>.</em>1<em>,</em>2<em>.</em>0] into 100 equal intervals using the linspace command and store it to the variable x1 (x1 should have 101 entries). If you haven’t worked with linspace before, see if you can figure out what the following commands do: linspace(-1,3,2), linspace(-1,3,3) and linspace(-1,3,11). Variables: x1</li>

 <li>Evaluate the polynomial at the points of the array x1 and store the result to the variable y1. Variables: y1</li>

</ol>

In applications with many data points, polynomial fitting is often not practical for a number of reasons. In those cases, other methods of interpolation are used. There are several methods of interpolation available in Matlab. We will consider the most commonly used linear, cubic (piecewise cubic Hermite interpolation) and (cubic) spline interpolation. Your lab instructor will explain the difference between those three.

Matlab’s basic interpolation command is called interp1. Use the command doc interp1 to bring up its documentation and see if you can figure out how to use it. Don’t try to read every detail. It can help to scroll down to the examples and see the command in action.

<ol start="7">

 <li></li>

</ol>

<table>

 <tbody>

  <tr>

   <td width="127"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Use interp1 to compute the values y2 of the polynomial at the points x1 with ‘linear’ option. Variables: y2</li>

</ul>

<ol start="8">

 <li>Use interp1 to compute the values y3 of the polynomial at the points x1 with ‘cubic’ option. Variables: y3</li>

 <li>Use interp1 to compute the values y4 of the polynomial at the points x1 with ‘spline’ option. Variables: y4</li>

 <li>Plot y1, y2, y3, y4 as functions of x1 on the same graph using the plot Use black color for y1, blue for y2, green for y3 and red for y4. Mark the initial set of points stored in x and y on this graph using black circles. The result should look something like this:</li>

</ol>

Notice the differences in the results of using the various methods of interpolation.