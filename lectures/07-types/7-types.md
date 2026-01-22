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
├── Loops      
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
something : (Bool -> Int) -> Bool -> Int
```
<!-- pause -->
What does this function application produce?
```elm
double : Int -> Int
double x =
    2 * x

List.map double [1,2,3,4,5]
```
<!-- column: 1 -->
What does this function calculate?
```elm
mystery : List Int -> Int -> Int
mystery l acc =
    case l of
        [] ->
            acc
        x :: xs ->
            mystery xs
                (if x > acc then
                    x
                 else
                    acc
                )
```

<!-- end_slide -->
# Commands recap
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Create an elm project?
<!-- pause -->
- elm init     
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
Enforce format rules on our code? 
<!-- pause -->
- elm-format src/        
<!-- reset_layout -->
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
```
We created a new data type (just like Int, Float, Bool) that have three possible values!
<!-- pause -->
<!-- column: 1 -->
We can create a variable of type GradeStatus
```elm
estatus : GradeStatus
estatus = Pending

falso : Bool
falso = False
```
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
1.0 Create a function "categoricalGrade" that given a list of grades return the category gradeStatus (Approved | Failed | Pending) where any negative number is Pending    
<!-- column_layout: [3,2] -->
<!-- column: 0 -->
2.1 Create a type "plainStatus" (On-time | Boarding | Delayed | Cancelled)

2.2 Create a function "plainScheduleAction" that maps as follows:     

2.3 Create a function "airportAction" that given a list of plainStatus transform it into a list of strings with plainScheduleActions
<!-- column: 1 -->
![](./assets/gviz/plainSchedule.png)
<!-- end_slide -->
<!-- jump_to_middle -->
##### Records 
<!-- end_slide -->
##### Records 
But sometimes primitives are not enough to express all the information we want.    
A person might be more complex than a simple String, we might want to add the age, and the email:
<!-- pause -->
```elm 
mit : { name : String, age : Int, email : String}
mit = 
    { name = "Mitsiu"
    , age = 32
    , email = "mitsiu.carreno@domain.com"
    }
```
<!-- end_slide -->
##### Records 
We can access the properties like `variable.property`
```elm 
mit : { name : String, age : Int, email : String}
mit = 
    { name = "Mitsiu"
    , age = 32
    , email = "mitsiu.carreno@domain.com"
    }

mit.name
```
Or we can treat the `property as a function`
```elm
.name mit
```
<!-- end_slide -->
##### Records 
How about this expression, what does it evaluate to?
```elm
List.map .age [mit, mit, mit] 
```
<!-- pause -->
Which is it's data type?
<!-- pause -->
Let's make a function that output's the person email:
```elm
getEmail : { name : String, age: Int, email : String } -> String
getEmail person =
    .email person
``` 
<!-- end_slide -->
##### Records 
Let's update our variable:
```elm 
mit : { name : String, age : Int, email : String}
mit = 
    { name = "Mitsiu"
    , age = 32
    , email = "mitsiu.carreno@domain.com"
    }


{ mit | email = "mitsiu.carreno@upa" }
```
We can read it out loud as "Create `a new record` that takes everything from mit, and update email to mitsiu.carreno@upa"
<!-- end_slide -->
##### Records 
```elm 
mit : { name : String, age : Int, email : String}
mit = 
    { name = "Mitsiu"
    , age = 32
    , email = "mitsiu.carreno@domain.com"
    }


{ mit | email = "mitsiu.carreno@upa" }
```
We can read it out loud as "Create `a new record` that takes everything from mit, and update email to mitsiu.carreno@upa"

What would `mit` evaluate to?

<!-- end_slide -->
##### Records 
mit `remains unchanged`!  Remember we don't modify the state.
```elm
{ age = 32, email = "mitsiu.carreno@domain.com", name = "Mitsiu" }
```

But we can bind the new value to a new variable.
```elm 
mit : { name : String, age : Int, email : String}
mit = 
    { name = "Mitsiu"
    , age = 32
    , email = "mitsiu.carreno@domain.com"
    }

mitV2 = { mit | email = "mitsiu.carreno@upa" }
```

<!-- end_slide -->
##### Records exercises
1.1 Create a record for programming languages with:
- name : String
- releaseYear : Int
- currentVersion: Float

1.2 Create a list with at least two programming languages       
1.3 Create a function that receives the list from point 1.2 and generates a String list with only the names eg:      
- Input : [{name="elm", releaseYear= 2012, currentVersion=0.19}]
- Output: ["elm"]


<!-- end_slide -->
##### Records exercises
2.1 Create a custom type UserType with the values (Student|Professor)     
2.2 Create a record for user with:
- name : String
- uType : UserType     

2.3 Create a list of users (both Students and Professors)      
2.4 Create a function that receives the list from point 2.3 and generates a String list with only the name of the students (professors names are emptied) eg:
- Input : [{name="Roberto", uType= Student}, {name="Mitsiu", uType=Professor}]
- Output: ["Roberto", ""]
<!-- end_slide -->

<!-- jump_to_middle -->
###### Aliases
<!-- end_slide -->
###### Aliases
As you might experience, writting a record type annotations can be exahusting:
```elm
getType : {name: String, uType: UserType} -> String
getType user =
    case .uType user of
        Student ->
            .name user ++ " es un estudiante"
        Professor ->
            .name user ++ " es un maestro"
```

Specially when we already defined that {name : String, uType: UserType} in the contex of our program is a user.

<!-- end_slide -->
###### Aliases
We can define a type alias which is simply `a shorter name for a type`

```elm
type alias User =
    {name: String, uType: UserType}

-- getType : {name: String, uType: UserType} -> String
getType : User -> String
getType user =
    case .uType user of
        Student ->
            .name user ++ " es un estudiante"
        Professor ->
            .name user ++ " es un maestro"
```
<!-- end_slide -->

<!-- jump_to_middle -->
##### Maybe
<!-- end_slide -->
##### Maybe
Previously we wrote a function:
> Make a function "head" that returns the first Int in a Int list, if the list is empty return -100.

And that is a horrible function, any idea why?
<!-- pause -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```latex +render
\begin{align}
head\text{ }[1,2,3] &\Longrightarrow  2 \\ 
head\text{ }[2,3,1] &\Longrightarrow  2 \\ 
head\text{ }[2,3] &\Longrightarrow  2 \\
head\text{ }[] &\Longrightarrow   -100
\end{align}
```
<!-- pause -->
<!-- column: 1 -->
```latex +render
\begin{align}
head\text{ }[-100,-101,-102]  \\ 
\end{align}
```
<!-- pause -->
```latex +render
\begin{align}
 &\Longrightarrow -100 \\ 
\end{align}
```
We have false positives
<!-- end_slide -->
##### Maybe
But given our current knowledge I had no other option...

Let's fix that.

What should our head function return if the input list it's empty?
```elm
head : List Int -> Int --?
```
