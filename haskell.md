# Haskell

## Arithmetic Operations
	
	2 + 15 		
		# => 17
	49 * 100 	
		# => 4900
	10 - 5		
		# => 5
	5 / 2		
		# => 2.5
	
## Boolean Expressions

	True && False
		# => False
	True || False
		# => True
	not False	
		# => True
	not (True && False) 	
		# => True
	
## Equality Comparisons

	5 == 5
		# => True
	5 /= 5		
		# => False, /= NOT equal to
	"h" == "g" 	
		# => False
	"h" == "h" 	
		# => True
	
## Functions

### Calling

	succ 8			
		# => 9
	min 9 10 		
		# => 9
	max 9 10 		
		# => 10
	(succ 9) + (max 5 4)	
		# => 16
	succ 9 * 10 		
		# => 100
	succ (9 * 10) 		
		# => 91
	div 92 10		
		# => 9
	92 `div` 10		
		# => 9, infix notation with backticks(`)
	
### Definition

Function declaration order is not important in a script 

	let doubleMe x = x + x	
		# in REPL, need to use let
	doubleMe x = x + x	
		# in a script file
	doubleMe 5		
		# => 10
	doubleMe 5.5		
		# => 11.0
	doubleUs x y = x * 2 + y * 2
	doubleUs x y = doubleMe x + doubleMe y 
		# alternative, bottom up approach
	
## Conditionals

Important to note that the else part of the if statement is important

	if x > 100
	  then x
	  else x * 2
	
	let doubleSmallNumber' x = (if x > 100 then x else x*2) + 1

	doubleSmallNumber' 55
		# => 111

## Comparisons

Haskell supports the standard comparison operators `>, >=, <, <=, ==, /=`

	5 > 5
		# => False
	
	5 >= 5
		# => True
		
	5 /= 5
		# => False
		
	[1,2,3] > [1,2,1]
		# => True
	
	[1,2,3] > [1,2,4]
		# => False
		
Lists are compared in lexicographical order, each item is taken in turn and compared until a difference is found and that result is returned.

## Scripts

Haskell scripts end in `.hs` and can be loaded with the `:l <script-name>` command

	:l script # note no extension

## Lists

	[1,2,3,4,5]
		# => [1,2,3,4,5]
		
List literal syntax is just syntactic sugar for this

	1:2:3:4:5:[]
	
Index based access, starting at 0 

	[1,2,3,4] !! 2
		# => 3
		
	"Hello" !! 1
		# => 'e'
		
Nested lists

	[[1,2],[3,4]]
	
Lists can only contain elements of the same type

	[1,'e']
		# => errors
		
### List Operations

	head [5,4,3,2,1]
		# => 5
		
	tail [5,4,3,2,1]
		# => [4,3,2,1]
		
	tail [1]
		# => []
		
Head always returns an individual element and tail returns a list of elements, both raise an exception when faced with an empty list.

	last [5,4,3,2,1]
		# => 1
		
	init [5,4,3,2,1]
		# => [5,4,3,2]

	length [1,2,3]
		# => 3
		
	null [1,2,3]
		# => False
		
	null []
		# => True

	reverse [1,2,3]
		# => [3,2,1]
		
	take 1 [5,4,3]
		# => [5]
	
	take 5 [1,2,3]
		# => [1,2,3]
		
	take 0 [1,2,3]
		# => []
		
	drop 1 [5,4,3]
		# => [4,3]
	
	drop 5 [5,4,3]
		# => []
	
	drop 0 [5,4,3]
		# => [5,4,3]
		
	minimum [5,4,3]
		# => 3
		
	sum [5,4,3]
		# => 12
	
	product [5,5,5]
		# => 125
		
	elem 4 [1,2,3,4] # tests for presence within list
		# => True
	
	elem 5 [1,2,3,4]
		# => False
		
### Ranges
	
	[1..10]
		# => [1,2,3,4,5,6,7,8,9,10]
		
	['a'..'d']
		# => ['a','b','c','d']
		
	[1,3..10]
		# => [1,3,5,7,9]
	
	[3,6..20]
		# => [3,6,9,12,15,18]

	[10,9..1]
		# => [10,9,8,7,6,5,4,3,2,1]
		
#### Infinite Ranges

	[1..]
		# => [1,2,3,4,5.....]
	
	take 5 [1..]
		# => [1,2,3,4,5]
		
	take 5 (cycle [1,2,3])
		# => [1,2,3,1,2]

	take 5 (repeat 3)
		# => [3,3,3,3,3]
		
	replicate 3 10
		# => [10,10,10]
		
### List Comprehensions
		
## Concatenation

The concatenation operator is `++` and works on list type elements, avoid concatenating long lists, as the first list has to be walked to the end before the second can be appended. 

	[1,2,3] ++ [4,5,6]
		# => [1,2,3,4,5,6]
	
	"Hello" ++ " " ++ "World"
		# => "Hello World"
		
	['H','e','l'] ++ ['l','o']
		# => "Hello"
		
The `++` always takes lists as it's parameters

	[1,2,3] ++ 1
		# => errors
	
	[1,2,3] ++ [1]
		# => [1,2,3,1]
		
The `:` operator appends a non-list element to the head of a list.

	'A':" SMALL CAT"
		# => "A SMALL CAT"
	
	5:[4,3,2,1]
		# => [5,4,3,2,1]
		
	[1]:[1,2,3]
		# => errors

## Strings

Strings in Haskell are just lists of single characters.

	"Hello" == ['H','e','l','l','o']
		# => True