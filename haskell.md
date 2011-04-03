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

## Scripts

Haskell scripts end in `.hs` and can be loaded with the `:l <script-name>` command

	:l script # note no extension

