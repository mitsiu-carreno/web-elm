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
# **Data types**       

Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
<!-- jump_to_middle -->
![](./assets/shapes.jpg)

<!-- reset_layout -->
<!-- end_slide -->
Agenda
===
├── Recap   
├── Types      
└── Instalation

<!-- end_slide -->

<!-- jump_to_middle -->
# Recap
<!--end_slide -->

# Recap
- What is an expression?
<!-- pause -->
- What is a value?
<!-- pause -->
- What does this simbol means?
```latex +render
\[ \Longrightarrow \]
```
<!-- pause -->
- Values are expressions?
<!-- pause -->
- Expressions are values?
<!-- pause -->
- What is imperative programming?
<!-- pause -->
- What is state in computer science?

<!-- end_slide -->

# Homework
**1. Bring your computer next session**       
<!-- pause -->
**2. Master your terminal:**    
- Change to a specific directory
- Go to parent directory 
- Print current directory 
<!-- pause -->
**3. Master your code editor:**
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
- Search in a single file
- Search in multiple files
- Know filename and file path of open file
- Go to definition
<!-- column: 1 -->
- Split screen
- Go to a specific line in a file
- Find and replace in a single/multiple files
<!-- reset_layout -->
<!-- end_slide -->
# Homework
**4. Master your keyword**
- How to keypress () [] {}
- https://monkeytype.com/
- Practice PascalCase with shift key
<!-- end_slide -->

# Functional programming
Functional programming allows reasoning about programs and their subcomponents in the same way that you would reason about a mathematical expression.

We’re not just in the business of writing code, but correct code!
<!-- end_slide -->

<!-- jump_to_middle -->
## Types
<!--end_slide -->

## Types guide structure (shape)
Functional programming places a great emphasis on types, which serve the purpose of documenting the purpose of code, and restricting the range of behaviors that a program is allowed to exhibit.

In this way, `types guide the structure of a program`, by providing clean interfaces for how different parts should interact, and what it should be allowed to do.
<!--end_slide -->
## Data types
We will be using a functional programming language called **Elm** which support the following data types:
<!-- column_layout: [2,1] -->
<!-- column: 0 -->
![](./assets/gviz/dataTypes.png)
<!-- column: 1 -->
![](./assets/elmo-door.gif)
<!-- reset_layout -->
<!-- end_slide -->

## Data types
> Type: Is a specification of the behavior of a piece of code. It **predicts** what a program is allowed to do.

To say that an expression e has type t we write:
```latex +render
\[ e : t \]
```
For example:
```latex +render +width:30%
\[ (5 + 2) * 3 : number \]
```
We are communicating that the expression (5 + 2) * 3 must produce a value of type number (either Int or Float)

<!-- end_slide -->
## Data types
Tracing back our value definition:
> Value: The result of a calculation (a **final answer** that cannot be simplified further)      

We can exemplify **values** for each data type:
```latex +render
\begin{align}
True &: Bool \\
1 &: Int \\
3.14 &: Float \\ 
'a' &: Char \\
''abc'' &: String
\end{align}
```
<!-- end_slide -->

## Data types & operators
Elm is a `statically typed` language, meaning that all typing rules are applied `before the program is ever run`
Let's analyze how Elm enforces it's type rules:

```latex +render +width:20%
\[ (5 + 2) * 3 : number \]
```
<!-- column_layout: [1,1,1] -->
<!-- column: 0 -->
The typing rule for **+** is:
```latex +render
\begin{align}
e1 + e2 &: number \\
if \\
e1 &: number \\
and \\
e2 &: number
\end{align}
```
<!-- pause -->
<!-- column: 1 -->
We know
```latex +render
\begin{align}
5 &: Int \\
and \\
2 &: Int \\
so \\
5 + 2 &: Int
\end{align}
```
<!-- pause -->
<!-- column: 2 -->
The typing rule for **\*** is:
```latex +render
\begin{align}
e1 * e2 &: number \\
if \\
e1 &: number \\
and \\
e2 &: number
\end{align}
```
<!-- reset_layout -->
<!-- end_slide -->
## Data types & operators
Now lets learn a new operator **++** 
<!-- pause -->
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
The typing rule for **++** is:
```latex +render
\begin{align}
e1 ++  e2 &: appendable \\
if \\
e1 &: appendable \\
and \\
e2 &: appendable
\end{align}
```
<!-- column: 1 -->
![](./assets/gviz/dataTypes.png)
Anyone can figure out a valid expression with **++**?
<!-- reset_layout -->

<!-- end_slide -->
## Data types & operators
```latex +render
\begin{align}
''Hello''  : String++  ''world'' &: String \Longrightarrow \\
''Helloworld'' &: String 
\end{align}
```

<!-- end_slide -->

## Data types & operators
Finally let's analyze the expression:
```latex +render +width:35%
\begin{align}
''Hello'' ++ 2 \\
''Hello'' ++ 2 :& appendable \\
if \\
''Hello'' :& appendable ✅\\
and \\
2 :& appendable ❌
\end{align}
```
<!-- pause -->
So "Hello" ++ 2 does not have a type, and we say it's an `ill-typed expression`
**Ill-typed programs are not evaluated**
<!-- end_slide -->

<!-- jump_to_middle -->
### Installation
<!--end_slide -->
### NodeJs
You can download and install the prebuilt 
https://nodejs.org/en/download
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/node-install.png)
<!-- column: 1 -->
Verify your installation with these two commands:
```bash
node --version

npm --version
```
<!-- reset_layout -->
<!-- end_slide -->

### Elm
Choose your os from:
https://guide.elm-lang.org/install/elm

Verify your installation with the command:
```bash
elm
```
<!-- end_slide -->

### Editor integrarion
Choose your editor and follow the instructions at:
https://github.com/elm/editor-plugins
<!-- end_slide -->

### Elm tooling
Run the command:
```bash
npm install -g elm-test elm-format
```
