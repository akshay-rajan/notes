# Haskell

Haskell is a purely functional programming language.

Features of haskell include
1. All variables are constants - their values cannot be changed
2. Functions have no side effects
3. Referential transparency - a function always returns the same value(s), when called with the same argument(s)
4. Lazy evaluation - defers actually computing results as long as possible

5. Statically Typed - Compiler knows the datatype of each piece of code
6. Type Inference - The datatype is determined by the value stored in a variable

## Index

1. [Start](#1-start)
2. [Function Calls](#2-function-calls)
3. [Function Definition](#3-function-definition)
4. [Lists Introduction](#4-lists-introduction)
5. [Range](#5-range)
6. [List Comprehension](#6-list-comprehension)
7. [Tuples](#7-tuples)
8. [Data Types](#8-data-types)
9. [Function Syntax](#9-function-syntax)
10. [Recursion](#10-recursion)
11. [Higher Order Functions](#11-higher-order-functions)
12. [User-Defined Data Types](#12-user-defined-data-types)

## 1. Start

Open GHC's interactive mode

```haskell
$ghci
ghci> 2 + 3
5
ghci> not (True && False)
True
ghci> 5 /= 5 -- Not equal
False
```

## 2. Function Calls

Type | Call
---|---
Infix Function | \<operand> \<operator> \<operand>
Prefix Function | \<operator> \<operand> \<operand>

```haskell
ghci> 5 * 2
10
ghci> succ 8
9
ghci> min 4 5
4
```

Function application has the highest precedence in Haskell

```haskell
ghci> succ 9 * 10
100
ghci> succ (9 * 10)
91
```
Any prefix function taking 2 arguments can be converted to an infix by using \`

```haskell
ghci> div 5 2
2
ghci> 5 `div` 2
2
```

## 3. Function Definition

Create a file with the extension `hs`
    
    touch filename.hs

We can define a function using

```haskell
doubleMe x = x + x
```

Often, we include **type signatures** along with the function statement

```haskell
doubleMe :: Integer -> Integer
doubleMe x = x + x
```

Open ghci and load the file

    ghci> :l filename.hs

Call the function
```haskell
ghci> doubleMe 3
6
```
If the file is updated we can reload the current file using `:r`

```haskell
-- `If` in haskell must always return something
doubleSmallNo x = if x > 100
                  then x
                  else x * 2
```
We use a `'` to denote a strict version of a fuction by appending it to the end of the function name (since it has no special meaning).
```haskell
hello' = "Hello, World!"
```

## 4. Lists Introduction

Lists are homogeneous data structures.

```haskell
-- In ghci, we use 'let' to denote a name
ghci> let nums = [1, 2, 3]
ghci> nums
[1,2,3]
```
We can concatenate lists using `++`
```haskell
l = [1, 2, 3] ++ [4, 5]
s = "hello" + " " + "world" -- Strings are just lists of characters
```
The `cons` operator (`:`) is used to add something to the beginning of a list

```haskell
ghci> 1:[2,3]
[1,2,3]
```

We can get an element at an index using `!!` operator

```haskell
-- Index starts at 0
ghci> "hello, world" !! 5
','
```

Nested lists are also possible. The lists can be of different lengths, but can only be of the same type.

We can compare lists using `==`, `<`, `>` etc. which compare the elements in lexicographical order.

We have functions `head`, `tail`, `init`, `last` which returns the first element, everything except the first element, everything except the last element and the last element respectively.

```haskell
ghci> head [1,2,3]
1
ghci> tail [1,2,3]
[2,3]
ghci> init [1,2,3]
[1,2]
ghci> last [1,2,3]
3
```
`length` returns the length of a list
```haskell
ghci> length [1,2,3]
3
```

`null` returns True if a list is empty and False otherwise
```haskell
ghci> null []
True
```

`reverse` does what it says

```haskell
ghci> reverse [1,2,3]
[3,2,1]
```

`take` extracts a specified number of elements from the front, meanwhile `drop` drops it
```haskell
ghci> take 3 [1,2,3,4,5]
[1,2,3]
ghci> take 3 [1,2] -- If the length is smaller, it returns the entire list
[1,2]
ghci> drop 2 [1,2,3,4]
[3,4]
ghci> drop 10 [1,2,3,4] -- If the length is smaller, it returns an empty list
[]
```

`maximum` and `minimum` are also functions in lists
```haskell
ghci> maximum [1,2,3]
3
ghci> minimum [1,2,3]
1
```

We can sum up a list using `sum`, and `product` returns their product
```haskell
ghci> sum [1, 2, 3, 4]
10
ghci> product [1, 2, 3, 4]
24
```

## 5. Range

Ranges are used to make lists composed of elements that can be enumerated.

```haskell
ghci> [1..10]
[1,2,3,4,5,6,7,8,9,10]
ghci> ['a'..'z']
"abcdefghijklmnopqrstuvwxyz"
ghci> [2,4..10] -- [first,second..limit]
[2,4,6,8,10]
```

We can define an infinite list using `[first,last..]`
```haskell
ghci> sum (take 100 [2,4..]) -- Sum of first 100 even numbers
10100
```

`cycle` generates an infinite repetition of a list, meanwhile `repeat` generates an infinite repetition of an element

```haskell
ghci> take 20 (cycle "abc")
"abcabcabcabcabcabcab"
ghci> take 20 (repeat 10)
[10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10]
```

`replicate` is a similar function that works like

```haskell
ghci> replicate 3 20
[20,20,20]
```
## 6. List Comprehension

```haskell
ghci> [2 * x | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
```

In the above example, we say that we *draw* our elements from the list `[1..10]`, and we bind each of those elements to `x`. `2 * x` represents how we want the elements that we have drawn to be reflected in the resulting list.

We can easily add a condition / **predicate** to our comprehension.

```haskell
ghci> [2 * x | x <- [1..10], x `mod` 4 == 0]
[8,16]
```
The process of weeding out elements from a list using predicates is called *filtering*.

```haskell
ghci> boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]
ghci> boomBangs [5..20]
["BOOM!","BOOM!","BOOM!","BANG!","BANG!","BANG!","BANG!","BANG!"]
ghci> [x+y | x <- [1,2,3], y <- [10,100,1000]] -- Multiple lists
[11,101,1001,12,102,1002,13,103,1003]   
ghci> let onlyCapital xs = [ c | c <- xs, c `elem` ['A'..'Z']]
ghci> onlyCapital "heLLO, worLd"
"LLOL"
```

## 7. Tuples

Tuples are used to store several heterogeneous elements as a single value.

```haskell
ghci> (1, 3)
(1,3)
ghci> (3, 'a', "hello")
(3,'a',"hello")
```

A tuple of size 2 (*pair*) and a tuple of size 3 (*triple*) are treated as two distinct types, and they cannot be mixed. Also, tuples with elements having different datatypes are also treated as different.

A tuple must atleast have 2 elements.

Functions on pairs include `fst` and `snd`

```haskell
ghci> fst (1,2)
1
ghci> snd (1,2)
2
```

`zip` takes two lists, produces a list of pairs

```haskell
ghci> zip [1,2,3,4,5] [5,5,5,5,5]
[(1,5),(2,5),(3,5),(4,5),(5,5)]
```

## 8. Data Types

To check the type of a variable, use `:t`

```haskell
ghci> :t 'a'
'a' :: Char
-- '::' is read as "has type of"

ghci> :t (True, '5')
(True, '5') :: (Bool, Char)

-- Type of a function
ghci> :t onlyCapital
onlyCapital :: [Char] -> [Char]
```

| Data Type | Description | Example |
|-----------|-------------|---------|
| `Int`     | Integral numbers, fixed precision | `123` |
| `Integer` | Integral numbers, arbitrary precision | `123456789101112131415` |
| `Float`   | Single precision floating point numbers | `123.45` |
| `Double`  | Double precision floating point numbers | `123.4567891011` |
| `Bool`    | Boolean values | `True`, `False` |
| `Char`    | Single characters | `'a'` |
| `String`  | List of characters | `"Hello"` |
| `Tuple`   | Fixed size collection of values, can be of different types | `(True, 'a')` |
| `List`    | Variable size collection of values, must be of same type | `[1, 2, 3, 4, 5]` |
<!-- | `Maybe`   | Optional values, can be `Nothing` or `Just` something | `Just "Hello"`, `Nothing` | -->
<!-- | `Either`  | Represents a value that can be one of two types | `Left "Error"`, `Right 123` | -->
<!-- | `IO`      | Represents a computation which performs I/O and returns a value of type a | `getLine`, `putStrLn "Hello"` | -->


```haskell
-- `a` is a **type variable**, which means it can be of any type
ghci> :t head
head :: [a] -> a
-- Type Variables are given names a,b,c...
ghci> :t fst
fst :: (a,b) -> a
```

Functions that use type variables are called **polymorphic functions**.

### Type Class
Type class is an interface that defines some behaviour. If a type is an instance of a type class, then it supports and implements the behaviour the type class describes.

Equality function takes any two values that are of the same type and returns a bool.
```haskell
-- Eq type class provides an interface for testing equality
-- Almost all types are an instance of Eq
ghci> :t (==)
(==) :: Eq a => a -> a -> Bool
```
`=>` is the 'Class Constraint'

```haskell
-- Ord is a type class for types whose values can be put in some order
ghci> :t (>)
(>) :: Ord a => a -> a -> Bool

-- Values of type class 'Show' can be represented as strings
ghci> :t show
show :: Show a => a -> String
ghci> show 3
"3"

-- 'Read' takes a string and returns an object of type 'read' (opposite of show)
ghci> :t read
read :: Read a => String -> a
ghci> read "True" || False
True
ghci> read "5" :: Float
5.0

-- 'Enum' is for sequentially ordered types; that can be enumerated
ghci> :t succ
succ :: Enum a => a -> a

-- Instances of 'Bounded' have an upper and lower bound
ghci> minBound :: Int
-9223372036854775808
ghci> maxBound :: Char
'\1114111'

-- 'Num' is for numeric
ghci> :t 20
20 :: Num a => a

-- sin, cos, sqrt etc. return 'Floating' type

-- 'Integral' includes only whole numbers
```

## 9. Function Syntax

**Pattern matching** is used to specify patterns to which
some data should conform and to deconstruct the
data according to those patterns.

```haskell
lucky :: Int -> String
lucky 7 = "You've won!"
lucky x = "Better luck next time!"
```

```haskell
ghci> lucky 4
"Better luck next time!"
ghci> lucky 7
"You've won!"
```

**Guards** are used when some property of passed values is satisfied.

```haskell
greatest x y
    | x > y = x
    | otherwise = y
```

`where` keyword is used to store the results of intermediate computation results to avoid repetition.

```haskell
parity n
    | x == 0 = "Even"
    | x == 1 = "Odd"
    where x = n mod 2
```

`let` allows us to bind to variables anywhere in the function, unlike `where` which can only be used at the end. 
`let` is an expression (has a value), meanwhile *while* is just a binding.

```haskell
let <bindings> in <expression>
```

```haskell
circle r =
    let area = pi * r ^ 2
        perimeter = 2 * pi * r
    in (area, perimeter) -- return value
```

`case` expressions allow us to execute blocks of code for specific values of a variable.

```haskell
case expression of pattern -> result
pattern -> result
pattern -> result
...
```
```haskell
head' xs = case xs of [] -> error "No head for empty lists!"
(x:_) -> x
```

## 10. Recursion

* *maximum*

    ```haskell
    max' :: (Ord a) => [a] -> a -- Takes any instance of Ord typeclass -> with ordering
    max' [] = error "Invalid operation!"
    max' [x] = x
    max' (x:xs) = max x (max' xs)
    ```

* *replicate*
    
    ```haskell
    -- replicate 3 's' = "sss"
    replicate' :: Int -> a -> [a]
    replicate' n x 
    | n <= 0 = []
    | otherwise = x: replicate' (n - 1) x
    ```

* *take*

    ```haskell
    take' :: (Num i, Ord i) => i -> [a] -> [a]
    take' n _
        | n <= 0 = []
    take' _ [] = []
    take' n (x:xs) = x : take' (n-1) xs
    ```

* *reverse*

    ```haskell
    reverse' :: [a] -> [a]
    reverse' [] = []
    reverse' (x:xs) = reverse' xs ++ [x]
    ```

* *repeat*

    ```haskell
    -- Returns an infinite list
    repeat' :: a -> [a]
    repeat' x = x:repeat' x
    ```

* *zip*

    ```haskell
    zip' :: [a] -> [b] -> [(a,b)]
    zip' _ [] = []
    zip' [] _ = []
    zip' (x:xs) (y:ys) = (x,y):zip' xs ys
    ```

* *elem*

    ```haskell
    -- Checks whether an element is in a list
    elem' :: (Eq a) => a -> [a] -> Bool
    elem' a [] = False
    elem' a (x:xs)
        | a == x = True
        | otherwise = a `elem'` xs
    ```

* `quicksort`
    
    *Algorithm:*
    ```
    function quicksort(list)
        if list is empty
            return empty list
        select a pivot element (first one here)
        create two lists, 'lesser' and 'bigger'
        for each element in list excluding the pivot
            if element is less than pivot
                add element to 'lesser' list
            else
                add element to 'greater' list
        return concatenation of (quicksort of 'lesser', pivot, quicksort of 'greater')
    ```
    *Code:*
    ```haskell
    quicksort :: (Ord a) => [a] -> [a]
    quicksort [] = []
    quicksort (x:xs) =
        let smaller = [a | a <- xs, a <= x]
            bigger = [a | a <- xs, a > x]
        in quicksort smaller ++ [x] ++ quicksort bigger
    ```

## 11. Higher Order Functions

A function which takes functions as arguments or returns functions as return values are called higher order functions.

```haskell
-- Applies any function twice
applyTwice :: (a -> a) -> a -> a 
applyTwice f x = f (f x)
```
```haskell
-- Takes a function and two lists as parameters
-- Joins the lists by applying the function between corresponding elements
zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]
zipWith' _ [] _ = []
zipWith' _ _ [] = []
zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys
```

* **Map**: takes a function and a list, and applies that function to every element in the list, producing a new list.

    ```haskell
    map :: (a -> b) -> [a] -> [b]
    map _ [] = []
    map f (x:xs) = f x : map f xs
    ```
* **Filter**: takes a predicate and a list, and returns the list of elements that satisfy that predicate.

    ```haskell
    filter :: (a -> Bool) -> [a] -> [a]
    filter _ [] = []
    filter p (x:xs)
        | p x = x : filter p xs
        | otherwise = filter p xs
    ```
    A predicate is a function that returns a Boolean value.

    ```haskell
    ghci> let listOfFuns = map (*) [0..]
    ghci> (listOfFuns !! 4) 5
    20
    ```

* **List Comprehension**: a way to filter, transform and combine lists. List comprehensions combine map and filter functions.

        [ expression | pattern <- list, condition ]

    ```haskell
    ghci> [x*2 | x <- [1..10]]
    [2,4,6,8,10,12,14,16,18,20]
    -- Draw our elements from [1..10]
    -- Bind each element to x
    -- x*2 is the output
    -- Output specifies how the drawn elements are to be reflected in the resulting list. ~ Map
    
    ghci> [x*2 | x <- [1..10], x*2 >= 12]
    [12,14,16,18,20]
    -- Predicates are separated from the rest using a comma. ~ Filtering    
    
    ghci> let lessThan10 xs = [ if x < 10 then True else False | x <- xs, odd x]
    ghci> lessThan10 [7..13]
    [True, True, False, False]
    ```

## 12. User-Defined Data Types

We use the `data` keyword to define new types.

```haskell
data Bool = True | False
       ↑       ^ ^ ^
      type  value_constructors
```
We can read this as, *Bool type can have a value of True **or** False*.

Value constructors are actually functions that returns a value of a datatype

```haskell
ghci> data Shape = Circle Float Float Float | Rectangle Float Float Float Float
ghci> :t Circle
Circle :: Float -> Float -> Float -> Shape
```
Here, the `Circle` value constructor can take 3 floats, meanwhile `Rectangle` has four fields.

To print out a User-defined type, we need to add `deriving Show` at the end, which makes the type part of the *Show* type class.

```haskell
data Shape = Circle Float Float Float | Rectangle Float Float Float Float 
    deriving Show
```
Introducing a new type `Point`, 
```haskell
data Point = Point Float Float deriving Show

data Shape = Circle Point Float | Rectangle Point Point deriving Show

-- Calculate the area of a Shape
area :: Shape -> Float
area (Circle _ r) = pi * r ^ 2
area (Rectangle (Point x1 y1) (Point x2 y2)) = abs (x2 - x1) * abs (y2 - y1)
```

We can use **Record Syntax** to write datatypes, with a name corresponding to each field types.

```haskell
data Person = Person {
    fname :: String,
    lname :: String,
    age :: Int,
    height :: Float,
    phone :: String
} deriving Show

ghci> let me = Person "Akshay" "Rajan" 21 180 "9440000000"
ghci> me
Person {fname = "Akshay", lname = "Rajan", age = 21, height = 180.0, phone = "9440000000"}
```

#### Type Constructors

A type constructor, like a value constructor can take types as parameters to produce new types.

```haskell
        type_parameter
           ↓
data Maybe a = Nothing | Just a
       ↑   
type_constructor
```
In the above example, if we pass a `char` as a type parameter, we get a type of `Maybe char`.

*Recursive data structures* can be created using type constructors, where one value of some type contains values of that type, which in turn contains more values of that type and so on.

### 1. Lists

A list is either an empty list, or an element joined together with a ':' with another list.

```haskell
data List a = Empty | Cons a (List a) deriving (Show, Read, Eq, Ord)
```
*Cons* is another word for ':'.

### 2. Queues

We can implement queue using a list.

```haskell
data Queue = Queue [Int] deriving Show

empty :: Queue
empty = Queue []

isEmpty :: Queue -> Bool
isEmpty (Queue []) = True
isEmpty _ = False

enqueue :: Queue -> Int -> Queue
enqueue (Queue q) x = Queue (q ++ [x])

dequeue :: Queue -> (Int, Queue)
dequeue (Queue []) = error "Queue empty!"
dequeue (Queue (x:xs)) = (x, Queue xs)

peek :: Queue -> Int
peek (Queue []) = error "Queue empty!"
peek (Queue (x:_)) = x
```

The most efficient approach is using two lists.
```haskell
data Queue a = Queue [a] [a] deriving Show

empty :: Queue a
empty = Queue [] []

isEmpty :: Queue a -> Bool
isEmpty (Queue ins outs) = null ins && null outs

enqueue :: a -> Queue a -> Queue a
enqueue x (Queue ins outs) = Queue (x:ins) outs

dequeue :: Queue a -> (a, Queue a)
dequeue (Queue [] []) = error "Queue empty!"
dequeue (Queue ins (x:outs)) = (x, Queue ins outs)
dequeue (Queue ins []) = dequeue (Queue [] (reverse ins))
```

### 3. Binary Search Trees

A tree is either an empty tree, or it is an element that contains some value and two other trees.

```haskell
data Tree a = EmptyTree | Node a (Tree a) (Tree a) deriving Show

-- Create a tree
singleton :: a -> Tree a
singleton x = Node x EmptyTree EmptyTree

-- Insertion
treeInsert :: (Ord a) => a -> Tree a -> Tree a
treeInsert x EmptyTree = singleton x
treeInsert x (Node a left right)
    | x == a = Node x left right
    | x < a = Node a (treeInsert x left) right
    | x > a = Node a left (treeInsert x right)

-- Check if an element is present
treeElem :: (Ord a) => a -> Tree a -> Bool
treeElem x EmptyTree = False
treeElem x (Node a left right)
    | x == a = True
    | x < a = treeElem x left
    | x > a = treeElem x right
```

```haskell
-- Creating a Binary Tree from a list
ghci> let nums = [8,6,4,1,7,3,5]
ghci> let numsTree = foldr treeInsert EmptyTree nums
ghci> numsTree
Node 5 
    (Node 3 
        (Node 1 EmptyTree EmptyTree) 
        (Node 4 EmptyTree EmptyTree)
    )
    (Node 7 
        (Node 6 EmptyTree EmptyTree) 
        (Node 8 EmptyTree EmptyTree)
    )
```
