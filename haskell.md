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

## Pattern Matching

Pattern matching is a method to define a function that handles different types of variables gracefully without if/else chains

	lucky :: Int -> String
	lucky 7 = "LUCKY NUMBER 7!!"
	lucky n = "Not so lucky."
	
Patterns are matched in the order declared

	lucky 9 
		# => "Not so lucky."
	
	lucky 7 
		# => "LUCKY NUMBER 7!!"
		
Patterns using a variable instead of a value serve as catch-all patterns and should be left as the last pattern. Not using a catch-all will result in a run-time error when a pattern isn't matched

### With Recursion

	factorial :: Integer -> Integer
	factorial 0 = 1
	factorial n = factorial (n - 1)

### With Tuples

	addVectors :: (Double,Double) -> (Double,Double) -> (Double,Double)
	addVectors a b = (fst a + fst b, snd a + snd b)

A more idiomatic and readable approach can be written like this

	addVectors :: (Double,Double) -> (Double,Double) -> (Double,Double)
	addVectors (x1,y1) (x2,y2) = (x1 + x2, y1 + y2)
	
#### With List Comprehensions

	[a+b | (a, b) <- [(1,2), (4,3), (5,6), (7,8)]]
		# => [3,7,11,15]
		
If pattern matching fails in a list comprehension, that element is discarded and the next element is examined

### With Lists

`[1,2,3,4]` is just syntactic sugar for `1:2:3:4:[]` which means lists can be matched as patterns like so

	head' :: [a] -> a
	head' [] = error "Can't call head on an empty list"
	head' (x:_) = x
	
Binding to several variables must be wrapped in `()` so Haskell can parse correctly.

	tell :: (Show a) => [a] -> String
	tell [] = "The list is empty"
	tell (x:[]) = "The list has one element: " ++ show x
		# can be written as [x]
	tell (x:y:[]) = "The list has two elements: " ++ show x ++ " and " ++ show y
		# can be written as [x,y]
	tell (x:y:_) = "The list is long, the first two elements are: " ++ show x ++ " and " ++ show y
	
	tell [1]
		# => "The list has one element: 1"
	tell [True,False]
		# => "The list has two elements: True and False"
	tell [1,2,3,4]
		# => "This list is long. The first two elements are: 1 and 2"
	tell []
		# => "The list is empty"
		
### As-Patterns

As-patterns allow you to break up a pattern and still keep a reference to the original item

	firstLetter :: String -> String
	firstLetter "" = "Empty String"
	firstLetter all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x] # ++ only works with lists!
	
	firstLetter "Dracula"
		# => "The first letter of Dracula is D"
		
## Guards

Guards check if parameters passed to your function meet certain conditions, they are similar to if chains in an imperative language. Guards are indicated by the vertical pipe followed by a boolean expression.

	bmiTell :: Double -> String
	bmiTell weight height
		| bmi <= 18.5 = "You're underweight"
		| bmi <= 25.0 = "You're normal"
		| bmi <= 30.0 = "You're fat"
		| otherwise = "You're a whale"
		where bmi = weight / height ^ 2
		      skinny = 18.5
		      normal = 25.0
		      fat = 30.0

## Where blocks

`otherwise` is the catch-all line for guards. `where` is used to define local variables or functions that live in the function's scope and must be indented from the function body, multiple variable declarations must be lined up vertically to avoid Haskell confusion. An important note about `where` scope is that the variables defined are not shared between patterns but are shared among guards.

`where` can also utilize pattern matching.

	where (skinny,normal,fat) = (18.5,25.0,30.0)
	
	initials :: String -> String -> String
	initials firstname lastname = [f] ++ ". " ++ [l] ++ "."
		where (f:_) = firstname
		      (l:_) = lastname
		
### With functions

The following uses the `where` created `bmi` function in the list comprehension in the function body.

	calcBmis :: [(Double,Double)] -> Double
	calcBmis xs = [bmi w h | (w,h) <- xs] 
		where bmi weight height = weight / height ^ 2
		

## Let Expressions

`let` expressions are similar to `where` in that `let` expressions let you bind variables anywhere and are expressions themselves, but they are more local and aren't shared among guards. `let` syntax follows the convention `let <bindings> in <expression>`. The values of the bindings are only visible in the whole `let` expression.

	cylinder :: Double -> Double -> Double
	cylinder r h = 
		let sideArea = 2 * pi * r * h
		    topArea = pi * r ^ 2
		in sideArea + 2 * topArea
		
Multivariable `let` expressions require the variables to be in the same column much like `where` blocks.

	[let square x = x * x in (square 5, square 3, square 6)]
		# => [(25,9,36)]
	
	(let a = 100; b = 200; c = 300 in a*b*c, let foo="Hey "; bar = "there!" in foo ++ bar)
		# => (6000000,"Hey there!")
		
	(let (a, b, c) = (1, 2, 3) in a+b+c) * 100
		# => 600

### In List Comprehensions

	calcBmis :: [(Double, Double)] -> [Double] 
	calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2]
	
Each time the list comprehension binds a Tuple from the original list and binds its components to w and h, the let expression binds `w / h ^ 2` to the name bmi which is used as the output of the list comprehension, resulting in a list of bmis.

### Let in the REPL

Let is used to declare functions and variables in the REPL but if an added `in <>` expression is added it will make the name bound to that scope and not reusable in the REPL.

	ghci> let zoot x y z = x * y + z
	ghci> zoot 3 9 2
		# => 29
	ghci> let boot x y z = x * y + z in boot 3 4 2
		# => 14
	ghci> boot
		# => not in scope
		
## Case Expressions

Case Expressions are essentially pattern matching that is usable anywhere in code and similar to case statements in imperative languages.

	head' :: [a] -> a
	head' xs = case xs of [] -> error "Empty list"
	                      (x:_) -> x
	
Pattern matching on function parameters can be done only when defining functions, but case expressions can be used anywhere.

	describeList :: [a] -> String
	describeList lst = "The list is " ++ case lst of [] -> "empty."
	                                                 [x] -> "a singleton list."
	                                                 xs -> "a longer list."

## Recursion

	maximum' :: (Ord a) => [a] -> a
	maximum' [] = "Empty list"
	maximum' [x] = x
	maximum' (x:xs) = max x (maximum' xs)
	
	replicate' :: Int -> a -> [a]
	replicate' n x
		| n <= 0    = []
		| otherwise = x : replicate' (n-1) x
		
	take' :: (Num i, Ord i) => i -> [a] -> [a]
	take' n _ 
		| n <= 0 = []
	take' _ [] = []
	take' n (x:xs) = x : take' (n-1) xs
	
Infinite recursion

	repeat' :: a -> [a]
	repeat' x = x:repeat' x
	
	zip' :: [a] -> [b] -> [(a,b)]
	zip' _ [] = []
	zip' [] _ = []
	zip' (x:xs) (y:ys) = (x,y):zip' xs ys
	
	elem' :: (Eq a) => a -> [a] -> Bool
	elem' a [] = False
	elem' a (x:xs)
		|	a == x = True
		| otherwise elem' a xs
		
### Quicksort

	quicksort :: (Ord a) => [a] -> [a]
	quicksort [] = []
	quicksort (x:xs) =
		let smallerOrEqual = [a | a <- xs, a <= x]
		    larger = [a | a <- xs, a > x]
		in quicksort smallerOrEqual ++ [x] ++ quicksort larger
		
## High Order Functions

All functions in Haskell only take on argument, function definitions like this

	max :: (Ord a) => a -> a -> a
	
means the same as this

	max :: (Ord a) => a -> (a -> a)
	
essentially all functions with more than one argument are high order, as they return a function that takes the additional parameter and returns a value from that, also known as `curried functions`. The `->` means you are defining a function that takes whatever is on its left side and returns a value of the type on its right side. Using the following function definition

	multThree :: Int -> Int -> Int -> Int
	# aka multThree :: Int -> (Int -> (Int -> Int))
	multThree x y z = x * y * z

When called like so `multThree 3 5 9` the function is applied like this `((multThree 3) 5) 9`. First, `multThree` is applied to 3, because they’re separated by a space. That creates a function that takes one parameter and returns a function. Then that function is applied to 5, which creates a function that will take one parameter, multiply 3 and 5 together, and then multiply that by the parameter. That function is applied to 9, and the result is 135.

	let multThreeWithNine = multThree 9
	multThreeWithNine 2 3
		# => 54
		
### Sections

Allows the partial application of Infix functions, sectioning an infix function can be supplying one parameter and surrounding the function with parentheses.

	divideByTen :: (Floating a) => a -> a
	divideByTen = (/10)

	divideByTen 5
		# => 0.5
		
### Functions Taking Functions

	applyTwice :: (a -> a) -> a -> a
	applyTwice f x = f (f x)
	
	zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]
	zipWith' _ [] _ = []
	zipWith' _ _ [] = []
	zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys
	
	flip' :: (a -> b -> c) -> (b -> a -> c)
	flip' f = g
		where g x y = f y x
		
Could also be written as 
	
	flip' :: (a -> b -> c) -> b -> a -> c
	flip' f x y = f y x
	
	map' :: (a -> b) -> [a] -> [b]
	map' _ [] = []
	map' f (x:xs) = f x : map f xs
	
	filter' :: (a -> Bool) [a] -> [a]
	filter' _ [] = []
	filter' p (x:xs)
		| p x = x : filter p xs
		| otherwise = filter p xs
		
### Quicksort using filter

	quicksort :: (Ord a) => [a] -> [a]
	quicksort [] = []
	quicksort (x:xs) = 
		let smallerOrEqual = filter (<= x) xs
		    larger = filter (> x) xs
		in quicksort smallerOrEqual ++ [x] ++ larger
		
### Collatz chain

Length of collatz chain for numbers 1 through 100

	chain :: Integer -> [Integer]
	chain 1 = [1]
	chain n
		| even n = n : chain (div n 2)
		| odd n = n : chain (n * 3 + 1)
	
	numLongChains :: Int
	numLongChains = length (filter isLong (map chain [1..100]))
		where isLong xs = length xs > 15
		
### Lambdas

Lambdas are distinguished by the `\` character, their syntax is as follows:

	\ {parameter} -> {body}
	
	map (+3) [1,2,3]
		# => [4,5,6]
	
	map (/x -> x + 3) [1,2,3]
		# => [4,5,6]
		
Pattern matching is available in lambdas, although you can't define several patterns for one parameter

	map (\(a,b) -> a + b) [(1,2),(3,4)]
		# => [3,7]
	
### Folds

Folds are used to reduce a collection to a single value, they take a binary function and a list to fold up. Folds can done from the right or left or a collection. The type of the accumulator value and the type of the end result are always the same when dealing with folds.

	foldl (+) 0 [1,2,3,4,5]
		# => 15
		
	sum' :: (Num a) => [a] -> a
	sum' xs = foldl (+) 0 xs
	
`sum'` can be rewritten as the following because of currying

	sum' = foldl (+) 0
	
	foldr (+) 0 [1,2,3,4,5]
		# => 15
	
	map' :: (a -> b) -> [a] -> [b]
	map' f xs = foldr (\x acc -> f x : acc) [] xs
	
Or with a left fold

	map' :: (a -> b) -> [a] -> [b]
	map' f xs = foldl (\acc x -> acc ++ [f x]) [] xs
	
`++` is much slower than `:` as it must walk the entire list before concatenating so it is better to use `foldr` when building new lists

Also important to note that right folds work on infinite lists and left folds do not. `foldr` will work on infinite lists when the binary function that we’re pass- ing to it doesn’t always need to evaluate its second parameter to give us some sort of answer. For instance, && doesn’t care what its second parameter is if its first parameter is False.

	elem' :: (Eq a) => a -> [a] -> Bool
	elem' x xs = foldr (\x acc -> if x == y then True else acc) False ys
	
`foldl1` and `foldr1` are like `foldl` and `foldr` except that they don't need an explicit starting accumulator, they assume the first element passed is the accumulator and go from there.

	reverse' :: [a] -> [a]
	reverse' = foldl (\acc x -> x : acc) []
	
	product' :: (Num a) => [a] -> a
	product' = foldl (*) 1
	
	filter' :: (a -> Bool) -> [a] -> [a]
	filter' p = foldr (\x acc -> if p x then x : acc else acc) []
	
	last' :: [a] -> a
	last' = foldl1 (\_ x -> x)
	
### Scans

Scans are like fold except they report intermediate accumulator results

	scanl (+) 0 [3,4,5,6]
		# => [0,3,7,12,18]
		
	scanr (+) 0 [3,4,5,6]
		# => [18,15,11,6,0]
		
