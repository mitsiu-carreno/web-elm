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
├── Types     
├── Types vs Values      
├── Custom types      
├── Maybe      
└── Homework

<!-- end_slide -->
<!-- jump_to_middle -->
# Recap
<!-- end_slide -->
# Recap
Before I forget, I want to introduce a brand new tool:
![](./assets/askqueue.png)
<!-- end_slide -->
# Recap
Maybe you notice but I have a horrible memory, I forget to give tokens, I forget names, I forget which lecture we are at.

But I really want to encourage you to ask questions, so:
<!-- pause -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
I am offering two free tokens:
- To the person that remind's me to setup askqueue and share the link
<!-- pause -->
- To the person that remind's me to check askqueue if an hour has passed and I havent checked
<!-- column: 1 -->
![](./assets/free_state.gif)
<!-- end_slide -->
# Recap
Ok on our last lecture we learn that:
<!-- column_layout: [1,1] -->
<!-- column: 0 -->

```elm
anItem : Html.Html msg
```
In this case anItem is a variable of type Html.Html msg
<!-- column: 1 -->
```elm
anItem : String -> Html.Html msg
```
In this case anItem is a function that receives a String and returns an Html.Html msg
<!-- reset_layout -->
<!-- pause -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```elm
anItem = Html.li [] 
        [ Html.text "Static" ]
```
<!-- column: 1 -->
```elm
anItem str = Html.li []
        [ Html.text str ]
```
<!-- reset_layout -->
<!-- end_slide-->
# Recap
We also learned that List.map is pretty powerfull
```elm
List.map (a -> b) -> List a -> List b
```
If we replace
- a => String
- b => Html.Html msg    

```elm
List.map (String -> Html.Html msg) -> List String -> List (Html.Html msg)
```
<!-- end_slide -->
# Recap
```elm
List.map (String -> Html.Html msg) -> List String -> List (Html.Html msg)
```

We can turn a String into an Html (1st parameter) with:
```elm
anItem : String -> Html.Html msg
anItem str = Html.li []
        [ Html.text str ]
```

So given an arbitrary list of strings we can:
```elm
                                [ Html.li [] [ Html.text "1" ]
List.map anItem ["1", "2"]   => , Html.li [] [ Html.text "2" ]
                                ]
```
<!-- end_slide -->
# Recap
```elm
Html.ul []                      Html.ul [] 
                                  [ Html.li [] [ Html.text "1" ]
List.map anItem ["1", "2"]   =>   , Html.li [] [ Html.text "2" ]
                                  ]
```

We can use the List.map result => `List (Html.Html msg)` as the second parameter of any Html element
<!-- end_slide -->
<!-- jump_to_middle -->
#### Types
<!-- end_slide -->
#### Types
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
#### Types
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
## Types vs values
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/traffic_l.png)
<!-- column: 1 -->
Which values does a trafic light might have?
<!-- pause -->
- Green
- Yellow
- Red
<!-- reset_layout -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/gviz/traffic_light.png)
<!-- column: 1 -->
Even though 
- There are more colors (Purple, Brown, Blue)
- There are more strings ("Apple", "Car", "Traffic")
<!-- end_slide -->
## Types vs values
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/traffic_l.png)
<!-- column: 1 -->
Which values does a trafic light might have?
<!-- pause -->
```elm
type TrafficLight
    = Green
    | Yellow
    | Red
```
<!-- reset_layout -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/gviz/traffic_light.png)
<!-- column: 1 -->
Even though 
- There are more colors (Purple, Brown, Blue)
- There are more strings ("Apple", "Car", "Traffic")
<!-- end_slide -->
## Custom type
> Types: Is a collection or grouping of data values, usually specified by a `set of possible values`, a set of allowed operations on these values, and/or a representation of these values as machine types.

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
A `traffic light` can have the values: 
- Red 
- Green
- Yellow
<!-- column: 1 -->
```elm
type TrafficLight
    = Green
    | Yellow
    | Red
```
<!-- reset_layout -->
<!-- end_slide -->
## Custom type
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
A `Bool` can have the values: 
- True
- False
<!-- column: 1 -->
```elm
type TrafficLight
    = Green
    | Yellow
    | Red
```
<!-- pause -->
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
We can create a `myBool` of type `Bool` and bind the value `True`, because True is a possible value of type Bool
```elm
myBool : Bool
myBool = True
```
<!-- pause -->
<!-- column: 1 -->
We can create a `myTrafficLight` of type `TrafficLight` and bind the value `Green`, because Green is a possible value of type TrafficLight
```elm
myTrafficLight : TrafficLight
myTrafficLight = Green
```
<!-- reset_layout -->
<!-- end_slide -->
#### Custom types
Let's come back to our initial problem, we want to track if a student passed or failed the course or if the grade is still "Pending", Bool is to constrained, String is to loose, let's make a new type (collection of values) that fit this specific problem
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
2.1 Create a type "AirplaneStatus" (OnTime | Boarding | Delayed | Cancelled)

2.2 Create a function "airplaneScheduleAction" that maps as follows:     

2.3 Create a function "airportAction" that given a list of AirplaneStatus transform it into a list of strings with airplaneScheduleActions
<!-- column: 1 -->
![](./assets/gviz/plainSchedule.png)
<!-- end_slide -->
// piggiback type with payload?
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
##### Challenge
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
- Create a function like:
```elm
myLaptopToStrings : Computer -> List String
myLaptopToStrings laptopInfo =
    -- Your definition here
```
So that an input like:
<!-- column: 1 -->
```elm
myLaptop : Computer
myLaptop =
    { ram = "32"
    , model = "Thinkpad x1"
    , brand = "Lenovo"
    , screenSize = "13.5"
    }

myLaptopToStrings myLaptop 
    Reduces to =>
    [ "Ram: 32"
    , "Modelo: Thinkpad x1"
    , "Marca: Lenovo"
    , "Pulgadas: 13.5"
    ]
```

