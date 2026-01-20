---
theme:
    override:
        code:
            theme_name: railsEnvy
        default:
            colors:
                background: "10141c"
---
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
<!-- jump_to_middle -->
# More types
Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
<!-- jump_to_middle -->
![](./assets/structure.png)

<!-- end_slide -->
Agenda
===
├── Recap   
├── Lists      
├── Map     
├── Custom types     
└── Homework

<!-- end_slide -->
<!-- jump_to_middle -->
# Recap
<!-- end_slide -->
# Code recap
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
What can we infer from the following type annotation?
```elm
something : Bool -> String
```
<!-- pause -->
What does this function do?
```elm
getIdByName : String -> Int
getIdByName name =
    case name of
        "Fernanda" ->1
        "Miguel" ->2
        "Juan" ->3
        _ ->0
```
<!-- pause -->
<!-- column: 1 -->
```elm
getGradeById : Int -> Float
getGradeById id =
    case id of
        1 ->9.4
        2 ->8.7
        3 ->9.3
        _ ->0

```
<!-- pause -->
```elm
getFinalGrade : String -> Float
getFinalGrade name =
    getGradeById (getIdByName name)
```
<!-- end_slide -->
# Commands recap
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Create an elm project?
<!-- pause -->
- elm init     
<!-- new_line -->
Start an elm repl session?
<!-- pause -->
- elm repl     
<!-- new_line -->
Track changes in git?
<!-- pause -->
- git add \<file\>    
<!-- column: 1 -->
Commit changes in git?
<!-- pause -->
- git commit -m'description'      
<!-- new_line -->
Push to remote repo in git?
<!-- pause -->
- git push origin main      
<!-- new_line -->
Verify elm code compilation? 
<!-- pause -->
- elm make src/*       
<!-- reset_layout -->
<!-- end_slide -->

<!-- jump_to_middle -->
## Lists
<!-- end_slide -->
## Lists
To write more interesting functions, we have to introduce the primitive `List`

> For `any type alpha`, there's a type List alpha, which `describes an ordered collection of 0 or more elements of type alpha`

```latex +render
$\text{[ ] : List }\alpha $
```
<!-- column_layout: [2,5] -->
<!-- column: 0 -->
So we have:
- List Int
<!-- pause -->
- List String
<!-- pause -->
- List List Int
<!-- column: 1 -->
For example: 
- [1,2,3]
<!-- pause -->
- ["Fernanda", "Juan", "Luis"]
<!-- pause -->
- \[\[1,2,3\]\]
<!-- end_slide -->
## Lists
A list is `two possible variants` (two possible things):
<!-- pause -->
- Nil: [] an empty list of type alpha
<!-- pause -->
- Cons: (::) An operator such that:
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
\begin{align}
x :: xs &: \text{List } \alpha \\
if \\
x &: \alpha \\
and \\
xs &: \text{List } \alpha
\end{align}
```
<!-- column: 1 -->
So we can say:
```elm
2 :: []  
```
Take take 2 and put it in this list as the first element
```latex +render +width:40%
$$ 2 :: [\text{ }] \cong [2]$$
```
<!-- end_slide -->
## Lists
In elm repl if we type (::) we get:
```elm
<function> : a -> List a -> List a
```
This is our first function with two parameters.
1. An element of type alpha
2. A list of type alpha
<!-- new_line -->
The output is of type List alpha (last arrow)
```elm
"Hi" :: [] : List String
```

<!-- end_slide -->
## Lists
We can cons multiple values:
```elm
1 :: 2 :: 3 :: [] : List Int
```
Which will be right-associative
```elm
1 :: (2 :: (3 :: [])) : List Int
```
Which is the same as:
```elm
[1, 2, 3] : List Int
```
<!-- end_slide -->
## Lists & Cases
We just saw how to construct Lists, now lets learn how to deconstruct them, with cases.     
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Remember that cases have the notation:
```latex +render
\begin{align}
\text{case } e1 &: \alpha \text{of} \\
pat1 &: \alpha \text{->} \\
& e2 : \beta
\\
pat2 &: \alpha \text{->} \\
& e3 : \beta
\end{align}
```
<!-- column: 1 -->
The pat stands for `pattern` which means we can `case on structures` rather than only on values:
```elm
case [1,2,3] of
    [] ->
        []
    x :: xs ->
        [x]
```

<!-- end_slide -->
## List
Let's make a quick function that uses the cons operator:
<!-- pause -->
```elm
headAdder : a -> List a -> List a
headAdder newElement list =
    newElement :: list

headAdder 1.1 [1.2, 1.3]
```
<!-- end_slide -->
## List exercises
1. Make a function "isEmpty" that returns if a given list is empty or not (Bool).
2. Make a function "head" that returns the first element in a non-empty list.

<!-- end_slide -->
<!-- jump_to_middle -->
### Map 
<!-- end_slide -->
### Map 
Map is our first higher order function, it's one powerfull function that allows us to make a transformation to each element in our list.
Let's start by analizing it's type:
```elm
List.map
<function> : (a -> b) -> List a -> List b
```
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
How many parameters does it have?
<!-- pause -->
- Anwser 2:
- 1. (a -> b) 
- 2. List a 
<!-- column: 1 -->
Which type is the output?
<!-- pause -->
- List b

What does the parameter `(a -> b)` mean?
<!-- end_slide -->
### Map 
Let's review our understanding with `(a -> b)`:
If I say
```elm
mystery : a -> b
```
What does it mean?
<!-- pause -->
It means a function with input a (alpha) and output b (beta)
Previously we used both alpha and beta as placeholder for a lot of types lets consider:
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```elm
always2 : a -> Int
always2 x =
    2
```
<!-- column: 1 -->
How do we apply always2?
<!-- pause -->
```elm
always2 1
always2 "1"
always2 'a'
always2 False
```
<!-- end_slide -->
### Map 
Let's track back into map.
```elm
List.map
<function> : (a -> b) -> List a -> List b
```
List.map is a function that receives a function and a list and returns other list.

This is a powerfull concept, functions are values, and as such we can pass them as parameters! 

This notion has been adopted by a lot of programming paradigms & languages because is quite usefull.
<!-- end_slide -->
### Map 
<!-- column_layout: [2,3] -->
<!-- column: 0 -->
Let's make a simple function `a->b` with two different types.

```elm
cBool in =
    case in of
        0 -> 
            False
        _ -> 
            True
```
What's the type annotation of this function?
<!-- pause -->
```elm
cBool : Int -> Bool
```
<!-- column: 1 -->
Now we have a type for `a -> b` let's replace on List.map:
- a => Int 
- b => Bool
```elm
List.map
<function> : (a -> b) -> List a -> List b
```
<!-- pause -->
```elm
List.map
<function> : (Int -> Bool) -> List Int -> List Bool
```
Any idea on what List.map may do?
<!-- end_slide -->
### Map
1. (a -> b) = Performs a transformation on input a's and produces b's
2. List a = The transformation will be applied to each element in a list
```elm
cBool : Int -> Bool
cBool inp =
    case inp of
        0 -> False
        _ -> True

listA : List Int
listA = [-2,-1,0,1,2]

List.map cBool listA -- => [True, True, False, True, True]
```
<!-- end_slide -->
### Map Exercises
1. Create a function "canBuyAlcohol" that given an array of ages return True or False if is able to buy alcohol
2. Create a function "allUpperCase" that given an array of names return the same names in uppercase (String.toUpper) 
3. Create a function "approveCourse" that given an array of grades (Float) return if it approve or not the course.
<!-- end_slide -->
<!-- jump_to_middle -->
#### Custom types
<!-- end_slide -->
#### Custom types
Let's say we want to track if a student passed or failed the course, which data type should we use?
<!-- pause -->
Did I guess your solution?
```elm
passed : Bool
```
There's a little issue with using Bool, it's more limited than what we need.
Right now did you pass this course? Should I register False?
```elm
passed : Bool
passed = False
```
That doesn't represent reallity, you haven't passed the course, yet you haven't failed the course either!
<!-- end_slide -->
#### Custom types
The current state about your grade is "pending" but a Bool only allows us two possible states.     
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Which data type should we use? 
<!-- pause -->
```elm
passed : String
passed = "Pending"

shouldPay : String -> Bool
shouldPay passed = 
    case passed of
        "approved" -> False
        "failed" -> True
        "pending" -> False
        _ -> False
```
<!-- pause -->
<!-- column: 1 -->
This solution has two big disadvantages:
1. We have to case on _ because there are many `other possible strings` even if they are not real passed values
2. This code outputs that `no one should pay!
<!-- end_slide -->
#### Custom types
Let's make our own data type:
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```elm
type GradeStatus 
    = Approved
    | Failed
    | Pending

passed : GradeStatus
passed = Pending
```
<!-- column: 1 -->
```elm
shouldPay : GradeStatus -> Bool
shouldPay passed = 
    case passed of
        Approved -> False
        Failed -> True
        Pending -> False
```
<!-- reset_layout -->
Approved is a posible value of the data type GradeStatus.    
Just like True is a possible value of the data type Bool.
<!-- end_slide -->

#### Custom types exercises
1.0 Create a function "categorialGrade" that given a list of grades return the category gradeStatus (Approved | Failed | Pending) where any negative number is Pending    
2.1 Create a type "plainStatus" (On-time | Boarding | Delayed | Cancelled)     
2.2 Create a function "plainScheduleAction" that maps as follows:     
![](./assets/gviz/plainSchedule.png)
2.3 Create a function "airportAction" that given a list of plainStatus transform it into a list of strings with plainScheduleActions

<!-- end_slide -->
<!-- jump_to_middle -->
##### Records 
##### Maybe 

