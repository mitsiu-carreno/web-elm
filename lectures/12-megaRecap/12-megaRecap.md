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
# Recap
Our next tests:
- 2nd Partial = 30%
- - Class exercise / Homework = 10%
- - Theorical evaluation = 40%
- - Practical evaluation (paper based, NO computer!) = 50%

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
<!-- end_slide -->
# Recap (Unit 1) - Html
- What's the difference between html elements and attributes?
<!-- pause -->
- - Html elements are visual and compose the screen, they exist for the user to see and interact, html attributes are metadata to the elements, allowing to group, modify the behaviour, or specify interaction between the user and the elements.
<!-- new_line -->
- Which html tags have opening and closing tags?
<!-- pause -->
- - \<p>\</p> | \<h1>\</h1> | \<a>\</a> | \<ul>\</ul> | \<li>\</li> | \<div>\</div>
<!-- new_line -->
- Which html tags `don't` have opening and closing tags (void elements)?
<!-- pause -->
- - \<br> | \<img>
<!-- new_line -->
- In an Html element where do we place the content? 
<!-- pause -->
- - Between the opening and closing tags \<p>`content`\</p>
<!-- end_slide -->
# Recap (Unit 1) - Html
- In an Html element where do we place the attributes
<!-- pause -->
- - In the opening tag \<p `class="value"`>content\</p>
<!-- new_line -->
- All html elements have the following type annotation, what does it means?
```elm
<function> : List (Html.Attribute msg) -> List (Html.Html msg) -> Html.Html msg
```
<!-- pause -->
- - It says that the function (h1, p, div, a, ...) expect's two parameters, a list of html attributes (class, id, href, ...) and a list of child html elements (h1, p, div, a, ...)
<!-- end_slide -->
# Recap (Unit 1) - Html
- Given the previous type annotation, which data type has main if I declare:
```elm
<function> : List (Html.Attribute msg) -> List (Html.Html msg) -> Html.Html msg
```
```elm
main = Html.h1 [] [] 
```
<!-- pause -->
- - main : Html.Html msg


<!-- end_slide -->
# Recap (Unit 1) - Html
In elm how do I produce the following html:
```html
<p></p>
```
<!-- pause -->
```elm
Html.p [] []
```
In elm how do I produce the following html:
```html
<p class="value"></p>
```
<!-- pause -->
```elm
Html.p [ Html.Attributes.class "value"] []
```
<!-- end_slide -->
# Recap (Unit 1) - Html
In elm how do I produce the following html:
```html
<p>content</p>
```
<!-- pause -->
```elm
Html.p [] [ Html.text "content"]
```
In elm how do I produce the following html:
```html
<p id="main">Content</p>
```
<!-- pause -->
```elm
Html.p [Html.Attributes.id "main"] [Html.text "Content"]
```
<!-- end_slide -->
# Recap (Unit 1) - Html
In elm how do I produce the following html:
```html
<p><strong></strong></p>
```
<!-- pause -->
```elm
Html.p [] [Html.strong [][]]
```
In elm how do I produce the following html:
```html
<p><strong>content</strong></p>
```
<!-- pause -->
```elm
Html.p [] [Html.strong [][Html.text "content"]]
```
<!-- end_slide -->
# Recap (Unit 1) - Html
In elm how do I produce the following html:
```html
<p>content<strong></strong></p>
```
<!-- pause -->
```elm
Html.p [] [Html.text "content", Html.strong [][]]
```
In elm how do I produce the following html:
```html
<p>content<strong>CONTENT</strong></p>
```
<!-- pause -->
```elm
Html.p [] [Html.text "content", Html.strong [][Html.text "CONTENT"]]
```
<!-- end_slide -->
# Recap (Unit 1) - Html
In elm how do I produce the following html:
```html
<p id="main">content<strong class="bold">SubContent</strong></p>
```
<!-- pause -->
```elm
Html.p [ Html.Attributes.id "main"] 
       [
          Html.text "content"
          , Html.strong [ Html.Attributes.class "bold"]
                        [
                            Html.text "SubContext"
                        ]
       ]
```
<!-- end_slide -->
# Recap (Unit 2)
- How are records usefull? What possibility they offer that List or other primitives dont?
<!-- pause -->
- - They allow us to group several fields to represent complex data (e.g. A person is more than just a name : String or an age: Int, or a role: UType, is the combination of all)
<!-- new_line -->
- Which simbol/character do we use to mark the begining and the end of a record?
<!-- pause -->
- - {} Curly braces
<!-- end_slide -->
# Recap (Unit 2)
- What's the meaning of the following expression?
```elm
mit : { age:Int }
mit = { age = 32 }
mit.age
```
<!-- pause -->
- - From the variable "mit" it returns the value of the property "age"
- What's the meaning of the following expression?
```elm
mit : { age:Int }
mit = { age = 32 }
.age mit
```
<!-- pause -->
- - There's a function ".age" that expect's a parameter of type record with at least the property age (we send mit as that parameter)
<!-- end_slide -->
# Recap (Unit 2)
- What's the type annotation of the function .age?
<!-- pause -->
```elm
{ b | age : a } -> a
```
<!-- new_line -->
- What does the following expression do:
```elm
{ mit | email = "mitsiu.carreno@upa" }
```
<!-- pause -->
- - Creates a `new record` based on all the properties in mit, except the email, which is bound to the value "mitsiu.carreno@upa".
- - As an important side note, mit remains unchaged (it's values aren't modified)
<!-- end_slide -->
# Recap (Unit 2)
- What does the following expression reduces to? 
```elm
List.map .age [mit, mit, mit, mit, mit]
```
<!-- pause -->
- - List.map will take each element (mit : { age : Int }) and apply .age to mit, remember that .age : { b | age : a } -> a which means that .age expects a record that has a property age of an unknown type, for mit : { age : Int } we can replace alpha to { mit | age : Int } -> Int, the result will be a List [32, 32, 32] 
<!-- new_line -->
- Which keywords does a alias use?
<!-- pause -->
- - `type alias`
<!-- new_line -->
- Exemplify a type alias of Int to Entero
<!-- pause -->
```elm
type alias Entero = Int
```
<!-- end_slide -->
# Recap (Unit 2)
- Exemplify a type alias of { color: String, weight: Float, type: String } to Apple
<!-- pause -->
```elm
type alias Apple = 
    { color : String
    , weight : Float
    , type : String
    }
```
Notice type alias only affect the type is not involved on values
<!-- new_line -->
- Which benefits does creating aliases has?
<!-- pause -->
- - Using records is easier because we refer to entities like Apple, User, Computer rather than describing the whole implementation which might risk interpretation. 
- - Updating records became instant and we can focus on updating values rather than types.
<!-- end_slide -->
# Recap (Unit 2)
- What is a component?
<!-- pause -->
- - A combination of functions and Html, which allows us to reuse our html in versatile ways.
<!-- new_line -->
- Why repetiton of code should be avoided?
<!-- pause -->
- - Code repetition makes maintainability harder, as there's more code that can be flawed. We should aim to write less code to reduce the surface of potential bugs.
<!-- new_line -->
- How do we turn a variable into a function?
<!-- pause -->
- - By adding an input and maintaining the previous type as output, also adding variables to catch the parameter values
```elm
anItem : Html.Html msg          anItem : String -> Html.Html msg
anItem = Html.li []         =>  anItem str = Html.li []
    [ Html.text "Static" ]          [ Html.text str ]    
```
<!-- end_slide -->
# Recap (Unit 2)
- Which are the keywords used to create a new custom data type?
<!-- pause -->
```elm
type ________ 
    = Invariant 1
    | Invariant 2
    | Invariant 3
```
<!-- new_line -->
- From the previous notation, what are the invariants?
<!-- pause -->
- - Are possible values of the type defined
<!-- new_line -->
- How can we define a data type?
<!-- pause -->
- - It's a collection of possible values (possible states) (e.g. the type TrafficLight can have the values Green, Red, Yellow)
<!-- end_slide -->
# Recap (Unit 2)
- What are some benefits from using custom types instead of primitives?
<!-- pause -->
- - Custom types allow us to fit the type and values to specific problems, primitive data types might be to constrained or flexible to adecuately represent one problem which leads to interpretation.
<!-- new_line -->
- What is a lambda expression?
<!-- pause -->
- - It's an alternative way to express a function
<!-- new_line -->
- What is the cost of lambda expressions?
<!-- pause -->
- - As it's anonymous, it can only be referenced in the place its created, preventing any kind of reuse.
<!-- end_slide -->
# Recap (Unit 2)
- What's the syntax for a lambda experssion? 
<!-- pause -->
```elm
(\ ____ -> _______)
^^  ^         ^   ^
||  |         |   |
|| Params   Body  |
||                |
||       Lambda end
Lambda start
```
<!-- end_slide -->
### Challenges
- Add to the back of a list
- Alternate strongs in li
- integrate myLaptop exer to the component aList
- List.map of a list of {url:String, content: String}

