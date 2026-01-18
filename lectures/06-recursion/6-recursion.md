---
theme:
    override:
        code:
            theme_name: railsEnvy
        default:
            colors:
                background: "10141c"
---
![](./assets/incept3.gif)
<!-- alignment: center -->

# **Recursion** | Mitsiu Alejandro Carreño Sarabia
<!-- end_slide -->
Agenda
===
├── Recap   
├── Recursion      
├── Footnote on recursion     
├── Exercises     
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

# Our old ways
Remember how in imperative contexts we have:
<!-- column_layout: [3,4] -->
<!-- column: 0 -->
```java +line_numbers
int x = 0;
for (int i = 0; i < 5; i++){
    x = x + 1;  
}
```
<!-- column: 1 -->
- We agreed that x = x + 1 on line 3 is `no bueno` because we modify the value
<!-- pause -->
- By the same principle i++ (i = i + 1) on line 2 must be gone
<!-- reset_layout -->
<!-- pause -->
- Actually the whole concept of a for loop needs to be gone, so how is this done in functional programming?
<!-- end_slide -->
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
<!-- jump_to_middle -->
## Recursion
<!-- column: 1 -->
![](./assets/doll.png)
<!-- end_slide -->
## Recursion
> The definition of a concept or process depends on a `simpler or previous version of itself`.

Let's analyse factorial number for example:
```latex +render
\begin{align}
fact(5) &= 1 \times 2 \times 3 \times 4 \times 5 \equal 120 \\
fact(4) &= 1 \times 2 \times 3 \times 4 \equal 24 \\
fact(3) &= 1 \times 2 \times 3 \equal 6 \\
... \\
fact(1) &= 1 
\end{align} 
```
<!-- end_slide -->
## Recursion
Let's suppose we want to calculate fact(5), is there a simpler version of this problem?
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
\begin{align}
fact(5) &= 1 \times 2 \times 3 \times 4 \times 5 \equal 120 \\
fact(4) &= 1 \times 2 \times 3 \times 4 \equal 24 \\
fact(3) &= 1 \times 2 \times 3 \equal 6 \\
... \\
fact(1) &= 1 
\end{align} 
```
<!-- column: 1 -->
<!-- pause -->
There is! 
```latex +render 
\begin{align}
fact(5) &= fact(4) \times 5 \equal 120 \\
fact(4) &= 1 \times 2 \times 3 \times 4 \equal 24 \\
fact(3) &= 1 \times 2 \times 3 \equal 6 \\
... \\
fact(1) &= 1 
\end{align} 
```
<!-- end_slide -->
## Recursion
And we can keep reducing our problem until it's really trivial
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render 
\begin{align}
fact(5) &= fact(4) \times 5 \equal 120 \\
fact(4) &= fact(3) \times 4 \equal 24 \\
fact(3) &= fact(2) \times 3 \equal 6 \\
fact(2) &= fact(1) \times 2 \equal 2 \\
fact(1) &= 1 

\end{align} 
```
<!-- column: 1 -->
We can summarize this behaviour as, for all natural numbers n
```latex +render 
\begin{align}
\text{if n=1 then } \\
fact(1) &= 1 \\
\text{else} \\
fact(n) &= fact(n-1) \times n \\
\end{align}
```
<!-- end_slide -->
## Recursion
<!-- column_layout: [3,4] -->
<!-- column: 0 -->
We can summarize this behaviour as, for all natural numbers n
```latex +render 
\begin{align}
\text{if n=1 then } \\
fact(1) &= 1 \\
\text{else} \\
fact(n) &= fact(n-1) \times n \\
\end{align}
```
<!-- column: 1 -->
We can express this notion using case notation as:
```latex +render
$$
fact(n)=\begin{cases}
    1, & \text{if} n=1 \\
    n * fact(n-1), & \text{if } n > 0
   \end{cases}
$$
```
<!-- end_slide -->
## Coding factorial
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fact(n)=\begin{cases}
    1, & \text{if} n=1 \\
    n * fact(n-1), & \text{if } n > 0
   \end{cases}
$$
```
What's our function type?
<!-- pause -->
```elm
factorial : Int -> Int
```
<!-- column: 1 -->
What's our `base case`? (The simplest version of the problem)
<!-- pause -->
```elm
factorial : Int -> Int
factorial n =
    -- Requires n >= 0
    -- Ensures factorial of n
    case n of
        1 ->
            1
```
<!-- end_slide -->

## Coding factorial
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fact(n)=\begin{cases}
    1, & \text{if} n=1 \\
    n * fact(n-1), & \text{if } n > 0
   \end{cases}
$$
```
Current progress:
```elm
factorial : Int -> Int
factorial n =
    -- Requires n >= 0
    -- Ensures factorial of n
    case n of
        1 ->
            1
```
<!-- column: 1 -->
Let's assume that the function `already works` on a "smaller" input.
<!-- new_line -->
You dont have to think about all the computation and subcomputations, remember that:
```latex +render 
\begin{align}
fact(5) &= fact(4) \times 5 \equal 120 \\
\end{align}
```
<!-- end_slide -->

## Coding factorial
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fact(n)=\begin{cases}
    1, & \text{if} n=1 \\
    n * fact(n-1), & \text{if } n > 0
   \end{cases}
$$
```
Let's assume that the function `already works` on a "smaller" input.
<!-- new_line -->
You dont have to think about all the computation, remember that:
```latex +render 
\begin{align}
fact(5) &= fact(4) \times 5 \equal 120 \\
\end{align}
```
<!-- column: 1 -->
Let's take the recursive leap of faith:
<!-- pause -->
```elm
factorial : Int -> Int
factorial n =
    -- Requires n >= 0
    -- Ensures factorial of n
    case n of
        1 ->
            1
        _ ->
            factorial(n-1) * n
```
<!-- end_slide -->

## Coding factorial
<!-- column_layout: [3,4] -->
<!-- column: 0 -->
```elm
factorial : Int -> Int
factorial n =
    -- Requires n >= 0
    -- Ensures factorial of n
    case n of
        1 ->
            1
        _ ->
            factorial(n-1) * n
```
Let's trace the factorial 5 application:
<!-- column: 1 -->
<!-- pause -->
```latex +render +width:61%
\begin{align}
fact(5) &= fact(4) \times 5
\end{align} 
```
<!-- pause -->
```latex +render +width:61%
\begin{align}
fact(4) &= fact(3) \times 4 
\end{align} 
```
<!-- pause -->
```latex +render 
\begin{align}
fact(3) &= fact(2) \times 3 \\ 
fact(2) &= fact(1) \times 2 \\
fact(1) &= 1 
\end{align} 
```
<!-- end_slide -->

## Coding factorial
<!-- column_layout: [3,4] -->
<!-- column: 0 -->
```latex +render 
\begin{align}
fact(5) &= fact(4) \times 5 \\
fact(4) &= fact(3) \times 4 \\
fact(3) &= fact(2) \times 3 \\ 
fact(2) &= fact(1) \times 2 \\
fact(1) &= 1 
\end{align} 
```
<!-- column: 1 -->
<!-- pause -->
```latex +render 
\begin{align}
fact(2) = 1 \times 2 \\
fact(3) = 1 \times 2 \times 3 \\
fact(4) = 1 \times 2 \times 3 \times 4 \\
fact(5) = 1 \times 2 \times 3 \times 4 \times 5 \\
fact(5) \Longrightarrow 120
\end{align} 
```

<!-- end_slide -->

## Fibonacci
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/fib.jpg)
<!-- column: 1 -->
![](./assets/fib-exampl.png)
<!-- end_slide -->
## Fibonacci
![](./assets/fib.jpg)
To calculate the next number we have to add the two previous numbers
<!-- end_slide -->
## Fibonacci
Let's suppose we want to calculate fib(6), is there a simpler version of this problem?
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
\begin{align}
fib(6) &= 0 + 1 + 1 + 2 + 3 + 5 \equal 8 \\
fib(5) &= 0 + 1 + 1 + 2 + 3 \equal 5 \\
fib(4) &= 0 + 1 + 1 + 2  \equal 3 \\
fib(3) &= 0 + 1 + 1 \equal 2 \\
fib(2) &= 0 + 1  = 1 \\
fib(1) &= 1 \\
fib(0) &= 0 
\end{align} 
```
<!-- column: 1 -->
<!-- pause -->
```latex +render +width:100%
\begin{align}
fib(6) &= fib(5) + fib(4) \equal 8 \\
fib(5) &= 0 + 1 + 1 + 2 + 3 \equal 5 \\
fib(4) &= 0 + 1 + 1 + 2  \equal 3 \\
fib(3) &= 0 + 1 + 1 \equal 2 \\
fib(2) &= 0 + 1  = 1 \\
fib(1) &= 1 \\
fib(0) &= 0 
\end{align} 
```
<!-- end_slide -->
## Fibonacci
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
We can continue simplifing all the way down
```latex +render 
\begin{align}
fib(6) &= fib(5) + fib(4) \equal 8 \\
fib(5) &= fib(4) + fib(3) \equal 5 \\
fib(4) &= fib(3) + fib(2) \equal 3 \\
fib(3) &= fib(2) + fib(1) \equal 2 \\
fib(2) &= fib(1) + fib(0)  = 1 \\
fib(1) &= 1 \\
fib(0) &= 0 
\end{align} 
```
<!-- column: 1 -->
We can express this notion using case notation as:
```latex +render
$$
fib(n)=\begin{cases}
    0, & \text{if} n=0 \\
    1, & \text{if} n=1 \\
    fib(n-1) + fib(n-2), & \text{if } n > 1
   \end{cases}
$$
```
<!-- reset_layout -->
<!-- end_slide -->
## Coding Fibonacci
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fib(n)=\begin{cases}
    0, & \text{if} n=0 \\
    1, & \text{if} n=1 \\
    fib(n-1) + fib(n-2), & \text{if } n > 1
   \end{cases}
$$
```
What's our function type?
<!-- pause -->
```elm
fib: Int -> Int
```
<!-- column: 1 -->
What's our `base case`? (The simplest version of the problem)
<!-- pause -->
```elm
fib : Int -> Int
fib n =
    -- Requires n >= 0
    -- Ensures nth fibonacci number
    case n of
        0 ->
            0
        1 ->
            1
```
<!-- end_slide -->

## Coding Fibonacci
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fib(n)=\begin{cases}
    0, & \text{if} n=0 \\
    1, & \text{if} n=1 \\
    fib(n-1) + fib(n-2), & \text{if } n > 1
   \end{cases}
$$
```
Current progress:
```elm
fib : Int -> Int
fib n =
    -- Requires n >= 0
    -- Ensures nth fibonacci number
    case n of
        0 ->
            0
        1 ->
            1
```
<!-- column: 1 -->
Let's assume that the function `already works` on a "smaller" input.
<!-- new_line -->
You dont have to think about all the computation and subcomputations, remember that:
```latex +render 
\begin{align}
fib(6) &= fib(5) + fib(4) \equal 8 \\
\end{align}
```
<!-- end_slide -->

## Coding Fibonacci
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
$$
fib(n)=\begin{cases}
    0, & \text{if} n=0 \\
    1, & \text{if} n=1 \\
    fib(n-1) + fib(n-2), & \text{if } n > 1
   \end{cases}
$$
```
Let's assume that the function `already works` on a "smaller" input.
<!-- new_line -->
You dont have to think about all the computation, remember that:
```latex +render 
\begin{align}
fib(6) &= fib(5) + fib(4) \equal 8 \\
\end{align}
```
<!-- column: 1 -->
Let's take the recursive leap of faith:
<!-- pause -->
```elm
fib : Int -> Int
fib n =
    -- Requires n >= 0
    -- Ensures nth fibonacci number
    case n of
        0 ->
            0
        1 ->
            1
        _ -> 
            fib(n-1) + fib(n-2)
```
<!-- end_slide -->
<!-- jump_to_middle -->
### Footnote on recursion
<!-- end_slide -->
### Footnote on recursion
Be aware that recursion in the context of functional programming is usefull but it has some risks.
<!-- new_line -->
- Recursion can lead to `infinite loops` if our base case isn't set properlly.
<!-- end_slide -->

<!-- jump_to_middle -->
#### Exercises
<!-- end_slide -->
#### Exercise Padovan
![](./assets/padovan.png)
<!-- end_slide -->
#### Exercise Padovan
[1, 1, 1, 2, 2, 3, 4, 5, 7, 9, 12, 16, 21, 28, 37, 49, 65, 86, 114, 151, 200, 265,]
```latex +render
\begin{align}
P(n) = P(n-2) + P(n-3) \text{for} n\geq3, with \\
P(0) = P(1) = P(2) = 1
\end{align} 
```
<!-- end_slide -->
#### Exercise Pow
Create a function to calculate any:
```latex +render
n ^ p Given : \\
n ^ 3 = n * n * n
```
This will require two parameters:
```elm
powerOf : Int -> Int -> Int
powerOf number power =
    ...
```
