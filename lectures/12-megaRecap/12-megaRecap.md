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
# Let's test our understanding
Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
<!-- new_line -->
<!-- new_line -->
<!-- new_line -->
![](./assets/memories.png)

<!-- end_slide -->
Agenda
===
├── Recap   
└── Exercises    

<!-- end_slide -->
# Recap
Before I forget 
![](./assets/askqueue.png)
<!-- end_slide -->
# Recap

I really want to encourage you to ask questions, so:
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
I am offering two free tokens:
- To the person that remind's me to setup askqueue and share the link
- To the person that remind's me to check askqueue if an hour has passed and I havent checked
<!-- column: 1 -->
![](./assets/free_state.gif)
<!-- end_slide -->
# Recap
Learning material:
1. This slides
2. https://www.youtube.com/watch?v=WgJ2FUW1miA&list=PLuGpJqnV9DXq_ItwwUoJOGk_uCr72Yvzb
3. https://elmprogramming.com/
4. (Official guide) https://guide.elm-lang.org/
5. (Official docs) https://package.elm-lang.org/packages/elm/core/latest/
6. (Advanced level - Standard ML) https://www.youtube.com/watch?v=jjX68oHAw-Y&list=PLsydD1kw8jng2t2G8USQNLz0faYZetPnH
<!-- end_slide -->

# Recap (Unit 1)
- Command to print current working directory
<!-- pause -->
- - pwd
<!-- new_line -->
- Command to change current terminal to the parent directory
<!-- pause -->
- - cd ..
<!-- new_line -->
- Command to change to the following path: C:\Users\Yo\Web-elm
<!-- pause -->
- - cd C:\\Users\Yo\Web-elm
<!-- new_line -->
- Command to create a new elm project
<!-- pause -->
- - elm init
<!-- new_line -->
- What is an expression?
<!-- pause -->
- - A set of one or many constants, variables, operators or functions
<!-- end_slide -->
# Recap (Unit 1)
- What is a value?
<!-- pause -->
- - A final answer, cannot be reduced any more
<!-- new_line -->
- What is computer state?
<!-- pause -->
- - The value of all variables in a program at a given time
<!-- new_line -->
- How does elm manage state during execution?
<!-- pause -->
- - State is inmutable, all variables remain binded to a single value
<!-- new_line -->
- Which primitives exists in elm?
<!-- pause -->
- - Float, Bool, Char, String, List a, Int, Tuples
<!-- end_slide -->
# Recap (Unit 1)
- Which data type structure must have the following expression:
```elm
e1 ++ e2
```
<!-- pause -->
```latex +render
\begin{align}
e1 ++  e2 &: appendable \\
if \\
e1 &: appendable \\
and \\
e2 &: appendable
\end{align}
```
<!-- end_slide -->
# Recap (Unit 1)
- Which data type structure must have the following expression:
```elm
case e1 of 
    e2 -> e3
```
<!-- pause -->
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
<!-- end_slide -->
# Recap (Unit 1)
- Which data type structure must have the following expression:
```elm
if e1 then 
    e2 
else
    e3
```
<!-- pause -->
```latex +render
\begin{align}
\text{if } e1 &: \text{Bool then} \\
e2 &: \alpha \\
\text{else} \\
e3 &: \alpha
\end{align}
```
<!-- end_slide -->
# Recap (Unit 1)
- Which data type structure must have the following expression:
```elm
e1 + e2
```
<!-- pause -->
```latex +render
\begin{align}
e1 + e2 &: number \\
if \\
e1 &: number \\
and \\
e2 &: number
\end{align}
```
<!-- end_slide -->
# Recap (Unit 1)
- Which data type structure must have the following expression:
```elm
e1 :: e2
```
<!-- pause -->
```latex +render
\begin{align}
x :: xs &: \text{List } \alpha \\
if \\
x &: \alpha \\
and \\
xs &: \text{List } \alpha
\end{align}
```
<!-- end_slide -->
# Recap (Unit 1)
- In elm what does semicolon (`:`) means?
<!-- pause -->
- - Has type
<!-- new_line -->
- Which command allows us to implement (modifying our source code) elm format rules?
<!-- pause -->
- - elm-format src/ 
<!-- new_line -->
- Which command allows us to verify if our code implements elm format rules?
<!-- pause -->
- - elm-format src/ --validate
<!-- new_line -->
- Which command allows us to verify if the content of any .elm file complies with elm syntax rules?
<!-- pause -->
- - elm-make src/*
<!-- new_line -->
- Command to start an interactive elm session
<!-- pause -->
- - elm repl
<!-- end_slide -->
# Recap (Unit 1)
- What's the difference between a function definition and a function application (invoke)?
<!-- pause -->
- - A function definition explains the transformation the function will do, but the actual transformation with concrete values happens until the function is applied.
<!-- new_line -->
- Which is another way to write the following expression:
```elm
'a' :: 'b' :: 'c' :: []
```
<!-- pause -->
- - ['a', 'b', 'c']
<!-- new_line -->
- In elm a list can be either one of two things which are they?
<!-- pause -->
- - Nil [] (an empty list)
- - Cons :: (something attached to a list)
<!-- end_slide -->
# Recap (Unit 1)
- What does this type annotation means:
```elm
List.map : (a -> b) -> List a -> List b
```
<!-- pause -->
- - List.map is a function with `2` parameters (inputs), the first parameter is a function that can transform some data type (alpha) to some other representation (beta), the second parameter is a list of alphas, List.map takes each single element in the input list, pass it to the function and store the output in a new list.
<!-- new_line -->
- What does High-order functions means?
<!-- pause -->
- - It means that functions receive the same treatment as variables, and can be pased to other functions or returned from other functions just like any other parameter.

<!-- end_slide -->
# Recap (Unit 1)
What does the following code means line by line?
```elm
multip : Int -> Int -> Int
multip x y = x * y
```
<!-- pause -->
- - The first line is the type annotation, it says that multip is a function (has arrows) that receives two Int values and return a Int value. The second line name the two variables as "x" and "y" and defines multip as the operation  "x * y"
<!-- end_slide -->
# Recap (Unit 1)
What does the following code means line by line?
```elm
foo : Bool -> List Float -> List Float -> List Float
foo a b c = 
    if a then
        3.5 :: b
    else
        c
```
<!-- pause -->
- -  The first line is the type annotation, it says that foo is a function (has arrows) that receives `3` parameters, the first is of type Bool, the second is of type List Float and the third is of type List Float, finaly the foo function retuns a List of Floats. The foo function name the three variables as "a", "b" and "c" it evaluates "a" of type Bool if it's true the value 3.5 is added at the front of the list b and returned, if "a" is false the list c is returned.
<!-- end_slide -->
# Recap (Unit 1)
```elm
flipper x =
    not x     – – Invierte un boolean True => False && False => True

flipAll funcTrans list =
    List.map funcTrans list

```
1. What's the type annotation of flipper?
<!-- pause -->
- - flipper : Bool -> Bool
2. What's the type annotation of flipAll?
<!-- pause -->
- - flipAll : (Bool -> Bool) -> List Bool
3. How do we apply flipAll to get the result [True, False, True]
<!-- pause -->
- - flipAll flipper [False, True, False]

### Challenges
Add to the back of a list
Alternate strongs in li
integrate myLaptop exer to the component aList

