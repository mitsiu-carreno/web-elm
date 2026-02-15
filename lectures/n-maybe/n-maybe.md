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


