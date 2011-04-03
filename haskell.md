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

List comprehensions are a succinct way to filter, transform and combine lists. Similar to mathematical set comprehensions.

Syntax
	
	[{what-to-collect} | {local-variable for each item in set} <- {collect to pull from}, {n predicates comma delimited}]
	
	[x*2 | x <- [1..10]]
		# => [2,4,6,8,10,12,14,16,18,20]
		
	[x*2 | x <- [1..10], x*2 >= 12]
		# => [12,14,16,18,20]
	
	[ x | x <- [50..100], x `mod` 7 == 3]
		# => [52,59,66,73,80,87,94]
		
	[ if x < 10 then "BOOM!" else "BANG!" | x <- [7..13], odd x]
		# => ["BOOM!", "BOOM!", "BANG!", "BANG!"]
	
	[ x | x <- [10..20], x /= 13, x /= 15, x /= 19]
		# => [10,11,12,14,16,17,18,20]
		
	[x+y | x <- [1,2,3], y <- [10,100,1000]]
		# => [11,101,1001,12,102,1002,13,103,1003]
		
	[ x*y | x <- [2,5,10], y <- [8,10,11], x*y > 50]
		# => [55,80,100,110]
		
	sum [1 | _ <- [1..10]] # _ ignores the value, get's the length of collection
		# => 10
		
	[ c | c <- ['a','B','c'], c `elem` ['A'..'Z']]
		# => ['B']
		
## Tuples

Tuples are fixed length lists with elements of different types and enclosed in parentheses

	(1,3)
		# => (1,3)
	
	(1,'a',3)
		# => (1,'a',3)
		
	[(1,3),(2,6),('a',2)]
		# => Error, lists can only contain elements of the same type, Tuples are typed to their elements and size
	
### Tuple Operations

	fst (1,3) # only works on pairs
		# => 1
	
	snd (1,3) # only works on pairs
		# => 3
		
`zip` takes two lists and returns a list of tuples containing an element of each list

	zip [1,2,3,4] [4,3,2,1]
		# => [(1,4),(2,3),(3,2),(4,1)]
		
	zip [1] [1,2,3]
		# => [(1,1)]
		
	zip [1..] ["one","two","three"]
		# => [(1,"one"),(2,"two"),(3,"three")]

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
		
## Types and Type Declarations

`::` is the 'has type of operator' and `:t` displays the type of an element

	:t True
		# => True :: Bool
		
	:t "Hello"
		# => "Hello" :: [Char] meaning a list of Char
		
Type declarations of functions, the following takes a list of `Char` and returns another list of `Char`

	removeNonUppercase :: [Char] -> [Char]
	removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z']]

The `->` separates the parameters and the return of a function, the final element in the declaration shows the function's return type.	

	addThree :: Int -> Int -> Int
	addThree x y z = x + y + z

`a` in a type declaration is an anonymous type

### Basic Types

* `Int` stands for Integer, and is used for whole numbers and is bounded meaning it has a minimum and maximum value as determined by the computer's CPU
* `Integer` is also used for Integers but is unbounded
* `Float` is a floating point number with single precision
* `Double` is also a floating point number but with double the precision
* `Bool` is a Boolean type with only two values `True` and `False`
* `Char` represents a unicode character, denoted by single quotes. A list of characters is a string
* Tuples are types in which their definition depends on their elements and size, empty tuple is its own distinct type

### Type Variables

Functions without explicit declaration of parameter types can operate on multiple types, this is called a type variable and is commonly represented by `a` in type declarations.

	:t head
		# => head :: [a] -> a
		
	:t fst
		# => fst :: (a, b) => a
		
	:t snd
		# => snd :: (a, b) => b
		
`head` takes a list of type `a` and returns a single `a` element, similarly `fst` takes a Tuple pair of type `(a,b)` and returns `a`, `a` and `b` can be of the same type, this just allows the function to operate on any type of pair Tuple.

### Type Classes

A type class is like an interface in OO languages like C# and Java, it encapsulates a bit of functionality and allows functions to operate on type variables that implement those type classes.

	:t (==)
		# => (==) :: (Eq a) => a -> a -> Bool
		
`(Eq a) => ` is called a *class constraint* which means all elements passed to `==` must be an instance of `Eq`. All standard Haskell types (minus IO) are instances of `Eq`

#### Common Type Classes

Types can be instances of many type classes and some type classes depend on being an instance of another type class. For example `Ord` has a dependency on `Eq`, if a type implements `Ord` it must also implement `Eq`.

* `Eq` is used for types that support equality testing
* `Ord` is used for types that support ordering
	* `:t (>) # => (>) :: (Ord a) => a -> a -> Bool`
	* `Ord` also supports `GT`, `LT`, and `EQ`
		* `compare 5 3 # => GT`
* `Show` is used to represent an element as a string, all types are instances of show except functions
	* `show 3 # => "3"`
* `Read` is the opposite of show, it reads a type from a String representation and must be supplied with additional arguments to allow type inference, or a type declaration
	* `read "3" + 5 # => 8`
	* `read "3" :: Int # => 3`
* `Enum` values are sequentially order types
* `Bounded` instances have an upper and lower bound
	* `minBound :: Int # => -2147483648`
	* `maxBound :: Int # => 2147483648`
* `Num` is a numeric type class whose instances can act like numbers, supported by all numeric types
* `Floating` includes the Float and Double types
* `Integral` is similar to the `Num` type but only includes Integral numbers

