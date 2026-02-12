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
# Components
Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
<!-- new_line -->
<!-- new_line -->
<!-- new_line -->
![](./assets/components.png)

<!-- end_slide -->
Agenda
===
├── Recap   
├── Components     
├── Avoid repetition      
└── Putting it all together 

<!-- end_slide -->
<!-- jump_to_middle -->
# Recap
<!-- end_slide -->
# Html recap
Can you help me describe the following html elements?
- \<div>\</div>
<!-- pause -->
It's a content `div`ision element, allows us to contain and group other elements and structure our page.
- \<h1>\</h1> | \<h2>\</h2> | \<h3>\</h3>
<!-- pause -->
Are several `h`eaders, to display, titles, subtitles, subsubtitles...
- \<p>\</p>   
<!-- pause -->
It's the `p`aragraph element, allows us to display text blocks
<!-- end_slide -->
# Html recap
Can you help me describe the following html elements?
- \<a>\</a>
<!-- pause -->
The `a`nchor element, allows to hiperlink pages, emails, locations via URL's
- \<ul> \<li>\</li> \</ul>
<!-- pause -->
The parent element is for `u`nordered `l`ists (ul), to display categorical information, (all elements are equally different).      
Inside we find `l`ist `i`tems (li), representing each possible category.
- \<br>
<!-- pause -->
Marks a point in html to produce a line `br`eak
<!-- end_slide -->
# Previously on...
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
Let's define a record named "Computer" with:
- ram: String
- model: String
- brand: String
- screenSize: String

And create a variable "myLaptop" of type Computer
<!-- column: 1 -->
Finally, let's make a variable "main" that reduces to:
```html
<div>
  <h1>My laptop<h1>
  <div>
    <ul>
      <li>Ram: {{.ram myLaptop}}</li>
      <li>Modelo: {{.model myLaptop}}</li>
      <li>Marca: {{.brand myLaptop}}</li>
      <li>Pulgadas: {{.screenSize myLaptop}}</li>
    </ul>
  </div>
</div>
```
<!-- end_slide -->
# Previously on...
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
Let's define a record named "Computer" with:
- ram: String
- model: String
- brand: String
- screenSize: String

And create a variable "myLaptop" of type Computer
<!-- pause -->
<!-- column: 1 -->
```elm
type alias Computer =
    { ram : String
    , model : String
    , brand : String
    , screenSize : String
    }
```
<!-- pause -->
```elm
myLaptop : Computer
myLaptop =
    { ram = "32"
    , model = "Thinkpad x1"
    , brand = "Lenovo"
    , screenSize = "13.5"
    }
```
<!-- reset_layout -->
<!-- end_slide -->
# Previously on...
<!-- column_layout: [1,2] -->
<!-- column: 0 -->
Finally, let's make a variable "main" that reduces to:     
div     
├── h1     
└── div    
&nbsp;&nbsp;&nbsp;&nbsp;└── ul    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── li    
<!-- column: 1 -->
```html
<div>
  <h1>My laptop<h1>
  <div>
    <ul>
      <li>Ram: {{.ram myLaptop}}</li>
      <li>Modelo: {{.model myLaptop}}</li>
      <li>Marca: {{.brand myLaptop}}</li>
      <li>Pulgadas: {{.screenSize myLaptop}}</li>
    </ul>
  </div>
</div>
```
<!-- end_slide -->
# Previously on...
<!-- column_layout: [2,4] -->
<!-- column: 0 -->
Finally, let's make a variable "main" that reduces to:     
div     
├── h1     
└── div    
&nbsp;&nbsp;&nbsp;&nbsp;└── ul    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── li    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── li    
<!-- column: 1 -->
```elm
main : Html.Html msg
main =
    Html.div
        []
        [ Html.h1 [] [ Html.text "My laptop" ]
        , Html.div
            []
            [ Html.ul
                []
                [ Html.li
                    []
                    [ Html.text "Some info" ]
                ]
            ]
        ]
```
<!-- end_slide -->
<!-- jump_to_middle -->
## Components
<!-- pause -->
> A part that combines with other parts to form something bigger
-> https://dictionary.cambridge.org
<!-- end_slide -->
## Components 
> A React component is a JavaScript `function` that you can sprinkle with `markup`.
-> https://react.dev/learn/your-first-component

(Hyper Text Markup Language)
<!-- pause -->
<!-- new_line -->
<!-- new_line -->
`Components = Html + Functions`
<!-- new_line -->
Let's build our first component
<!-- end_slide -->
## Components = Html + Functions
Let's focus on a specific Html section:
<!-- column_layout: [2,3] -->
<!-- column: 0 -->
```html
<ul>
  <li>Some content</li>
</ul>
```
We are going to begin really simple
<!-- column: 1 -->
```elm
aList : Html.Html msg
aList = 
    Html.ul 
        [] 
        [ Html.li 
            []
            [ Html.text "Some content"]
        ]
```
<!-- end_slide -->
## Components = Html + Functions
Let's start by making the content more flexible i want to change the string literal "Some content" to be a parameter
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```elm
aList : Html.Html msg
aList = 
    Html.ul 
        [] 
        [ Html.li 
            []
            [ Html.text "Some content"]
        ]
```
<!-- column: 1 -->
<!-- pause -->
```elm
aList : String -> Html.Html msg
```
<!-- pause -->
```elm
aList content = 
    Html.ul 
        [] 
        [ Html.li 
            []
            [ Html.text content ]
        ]
```
<!-- end_slide -->
## Components = Html + Functions
Let's suppose we have three `l`ist `i`tem elements 
```elm
aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 = 
    Html.ul [] 
        [ Html.li []
            [ Html.text content1 ]
        , Html.li []
            [ Html.text content2 ]
        , Html.li []
            [ Html.text content3 ]
        ]
```
<!-- end_slide -->
<!-- jump_to_middle -->
### Avoid repetition!
<!-- end_slide -->
### Avoid repetition!
<!-- column_layout: [1,1] -->
<!-- column: 0 -->

It sucks to write code like this! 
```elm
aList : Html.Html msg
aList = 
    Html.ul 
        [] 
        [ Html.li [][]
        , Html.li [][]
        , Html.li [][]
        ]
```
<!-- column: 1 -->
<!-- pause -->
- It's redundant
- I can make typos if i write each
- I can copy/paste but what if we want to change something? (I would have to do it three times!)

---
We should aim to write less code because it means directly less posible bugs.
<!-- end_slide -->

### Avoiding repetition
Ok I want to tell how all \<li>\<li/> elements in my list are going to be `but only once!`
```elm
aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 = 
    Html.ul [] 
        [ Html.li []
            [ Html.text content1 ]
        , Html.li []
            [ Html.text content2 ]
        , Html.li []
            [ Html.text content3 ]
        ]
```
<!-- end_slide -->
### Avoiding repetition
I want to write something like this:
```elm
aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 =
    Html.ul []
        [ anItem content1
        , anItem content2
        , anItem content3
        ]
``` 
Which typeAnnotation does anItem has to have?
<!-- pause -->
```elm
anItem : String -> Html.Html msg
```
<!-- end_slide -->
### Avoiding repetition
Which function body (definition) does anItem could have?
```elm
anItem : String -> Html.Html msg
```
<!-- pause -->
```elm
anItem content =
    Html.li [] [ Html.text content] 


aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 =
    Html.ul []
        [ anItem content1
        , anItem content2
        , anItem content3
        ]
``` 
<!-- end_slide -->
### Avoiding repetition
<!-- column_layout: [3,2] -->
<!-- column: 0 -->
```elm +line_numbers
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 


aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 =
    Html.ul []
        [ anItem content1
        , anItem content2
        , anItem content3
        ]
``` 
<!-- column: 1 -->
Now if my li element must change I only have to modify it in a single place (Line 3)
<!-- end_slide -->
### Hardcoded logic
This code is a good refactor but what if I want 4 items? Or 10? Or 1?
```elm +line_numbers {6,9-11}
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 


aList : String -> String -> String -> Html.Html msg
aList content1 content2 content3 =
    Html.ul []
        [ anItem content1
        , anItem content2
        , anItem content3
        ]
``` 
<!-- end_slide -->
### Hardcoded logic
We can change our aList inputs to a list of strings but something would break
```elm +line_numbers
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 


aList : List String -> Html.Html msg
aList contents =
    Html.ul []
        [ anItem content1 -- Now I cant access content1
        , anItem content2 -- or content2
        , anItem content3 -- or content3
        ]
``` 
<!-- end_slide -->

### Hardcoded logic
What a problem, let's try to see it in context:
```elm +line_numbers
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 

aList : List String -> Html.Html msg
aList contents =
    Html.ul [] 
        -- Generate a list of Html.Html msg with the <li> from anItem
``` 
- On L:9 I want to transform my List String (contents) into a List Html.Html msg (\<li>'s)
<!-- end_slide -->

### Hardcoded logic
Do we know anything that can help us transform from a List String -> List Html.Html msg?
<!-- pause -->
```elm 
List.map : (a -> b) -> List a -> List b
```
We know that `List a` is contents (List String) and `List b` is our \<li>'s (List Html.Html msg)
<!-- new_line -->
- a = String
- b = Html.Html msg
```elm 
List.map : (String -> Html.Html msg) -> List String -> (List Html.Html msg)
```
<!-- end_slide -->
### Hardcoded logic
Do we know anything that can help us transform from a List String -> List Html.Html msg?
```elm 
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 

aList : List String -> Html.Html msg
aList contents =
    Html.ul [] 
        List.map __________ contents
     -- List.map : (String -> Html.Html msg) -> List String -> (List Html.Html msg)
``` 
<!-- end_slide -->
### Hardcoded logic
Isn't this just beautiful!
```elm 
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 

aList : List String -> Html.Html msg
aList contents =
    Html.ul [] 
        List.map anItem contents
``` 
<!-- end_slide -->
<!-- jump_to_middle -->
#### Putting it all together
<!-- end_slide -->
#### Putting it all together
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```elm
main : Html.Html msg
main =
    Html.div
        []
        [ Html.h1 
            [] 
            [ Html.text "My laptop"]
        , Html.div
            []
            [ 
                aList 
                    ["Some text"
                    , "Other text"
                    , "Final text"
                    ] 
            ]
        ]
```
<!-- column: 1 -->
```elm 
anItem : String -> Html.Html msg
anItem content =
    Html.li [] [ Html.text content] 

aList : List String -> Html.Html msg
aList contents =
    Html.ul [] 
        List.map anItem contents
```
- Notice I had to wrap aList on []
<!-- end_slide -->
<!-- jump_to_middle -->
##### Homework
<!-- end_slide -->
##### Homework
- Create a component "headers" that given a String parameter, generates the following html code:
```html
<div>
  <h1>{{param}}</h1>
  <h2>{{param}}</h2>
  <h3>{{param}}</h3>
  <h4>{{param}}</h4>
  <h5>{{param}}</h5>
  <h6>{{param}}</h6>
</div>
```
<!-- end_slide -->
##### Homework
- Create a component "hyperlink" that receives two Strings
- - The url
- - The text
That produces the following html:
```html
<a href="{{url}}">{{text}}</a>
```
