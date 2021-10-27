Advanced Text-Fu


# Advanced Text-Fu

### 1. regex (Regular Expressions)
* We'll go through a couple of the most common regular expressions, these are almost universal with any programming language.
* example we are gonna use
> sally sells seashells <br> 
> by the seashore

1. Beginning of a line with **^**
> ^by </br>
> ans: by the seashore
2. End of a line with **$**
> seashore$ </br>
> ans: by the seashore
3. Matching any single character with **.**
> b. </br>
>ans: by
4. Bracket notation with **[ ]**

	* brackets allow us to specify characters found within the bracket. 
	> d\[iou]g </br>
	> dig, dog, dug
	* The previous anchor tag ^ when used in a bracket means anything except the characters within the bracket. 
	> d\[\^i]g </br>
	> dog dug
	* Brackets can also use ranges to increase the amount of characters you want to use. 
	> d\[a-c]g </br>
	> dag, dbg, and dcg
	* Be careful though as brackets are case sensitive
	> d\[A-C]g </br>
	> dAg, dBg and dCg

