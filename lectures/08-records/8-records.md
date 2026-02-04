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
# Records
Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
<!-- new_line -->
<!-- new_line -->
<!-- new_line -->
<!-- new_line -->
<!-- new_line -->
![](./assets/complexity.png)

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
What can we infer from the following type annotation?
```elm
mystery : Char -> (Char -> Int) -> (Int -> Bool) -> Bool
```
<!-- pause -->
Let's dig deeper into mystery how can we apply it?
<!-- pause -->
```elm
Char.toCode 'A' -- Reduces to 65
Char.toCode 'a' -- Reduces to 97

lesserThan97 : Int -> Bool
lesserThan97 x =
    x < 97
```
<!-- end_slide -->
# Code recap
```elm
Char.toCode 'A' -- Reduces to 65
Char.toCode 'a' -- Reduces to 97

lesserThan97 : Int -> Bool
lesserThan97 x =
    x < 97

mystery 'C' Char.toCode lesserThan97
mystery : Char -> (Char -> Int) -> (Int -> Bool) -> Bool
```
Does this type check?
<!-- end_slide -->
# Code recap
```elm
Char.toCode 'A' -- Reduces to 65
Char.toCode 'a' -- Reduces to 97

lesserThan97 : Int -> Bool
lesserThan97 x =
    x < 97

mystery : Char -> (Char -> Int) -> (Int -> Bool) -> Bool
mystery letter fun1 fun2 =
    fun2 (fun1 letter)


mystery 'C' Char.toCode lesserThan97
```
What does mystery do?
<!-- end_slide -->
# Commands recap
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Create an elm project?
<!-- pause -->
- elm init     
<!-- new_line -->
Check format (coding style convetions)?
<!-- pause -->
- elm-format src/    
<!-- column: 1 -->
Start an interactive session?
<!-- pause -->
- elm repl      
<!-- new_line -->
Validate the code is elm compliant code?
<!-- pause -->
- elm make src/*      
<!-- new_line -->
Enforce format rules on our code? 
<!-- pause -->
- elm-format src/        
<!-- reset_layout -->
<!-- end_slide -->

<!-- jump_to_middle -->
## Records 
<!-- end_slide -->
## Records 
Sometimes primitives are not enough to express all the information we want.    
A person might be more complex than a simple String, we might want to add the age, and the email, that's exactly why we have records:
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
## Records 
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
.name : { b | age : a} -> a
.name mit
```
<!-- end_slide -->
## Records 
Let's make a function that output's the person email:
```elm
getEmail : { name : String, age: Int, email : String } -> String
getEmail person =
    .email person
``` 
<!-- end_slide -->
## Records 
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
## Records 
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
## Records 
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
## Records
How about this expression, what does it evaluate to?
```elm
List.map : (a -> b) -> List a -> List b
List.map .age [mit, mit, mit] 
```
<!-- pause -->
Which is it's data type?
What does it output?
<!-- end_slide -->
## Records exercises
1.1 Create a record for programming languages with:
- name : String
- releaseYear : Int
- currentVersion: Float

1.2 Create a list with at least two programming languages       
1.3 Create a function "languageNames" that receives the list from point 1.2 and generates a String list with only the names eg:      
- Input : [{name="elm", releaseYear= 2012, currentVersion=0.19}]
- Output: ["elm"]


<!-- end_slide -->
## Records exercises
2.1 Create a record for user with:
- name : String
- uType : String     

2.3 Create a list of users (uType can be "Students" or "Professors")      
2.4 Create a function "onlyStudents" that receives the list from point 2.3 and generates a String list with only the name of the "Students" (professors names are emptied) eg:
- Input : [{name="Roberto", uType= "Student"}, {name="Mitsiu", uType="Professor"}]
- Output: ["Roberto", ""]
<!-- end_slide -->

<!-- jump_to_middle -->
### Aliases
<!-- end_slide -->
### Aliases
As you might experience, writting a record type annotations can be exahusting:
```elm
getType : {name: String, uType: String } -> String
getType user =
    case .uType user of
        "Student" ->
            .name user ++ " es un estudiante"
        "Professor" ->
            .name user ++ " es un maestro"
        _ ->
            .name user ++ " no es maestro ni estudiante"
```

Specially when we already defined that {name : String, uType: String } in the contex of our program is a user.

<!-- end_slide -->
### Aliases
We can define a type alias which is simply `a shorter name for a type`

```elm
type alias User =
    {name: String, uType: String }

-- getType : {name: String, uType: String} -> String
getType : User -> String
getType user =
    case .uType user of
        "Student" ->
            .name user ++ " es un estudiante"
        "Professor" ->
            .name user ++ " es un maestro"
        _ ->
            .name user ++ " no es maestro ni estudiante"
```
<!-- end_slide -->
#### Excersice
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
Let's define a Computer record with:
- ram: Int
- model: String
- brand: String
- screenSize: Float

Let's alias this record as "Computer"

<!-- column: 1 -->
Finally, let's make an html page that generates:
```html
<div>
    <h1>My computer<h1>
    <div>
        <ul>
            <li>Ram: {{Computer.ram}}</li>
            <li>Modelo: {{Computer.model}}</li>
            <li>Marca: {{Computer.brand}}</li>
            <li>Pulgadas: {{Computer.screenSize}}</li>
        </ul>
    </div>
</div>
```
