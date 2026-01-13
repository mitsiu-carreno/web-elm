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
├── List      
├── First project      
├── If    
├── Case    
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
- Create an elm project?
<!-- pause -->
- Start an elm repl session?
<!-- pause -->
- Stage changes in git?
<!-- pause -->
- Commit changes in git?
<!-- pause -->
- Push to remote repo in git?
<!-- pause -->
- Verify elm code compilation? 
<!-- pause -->
<!-- column: 1 -->
elm init     
elm repl     
git add \<file\>    
git commit -m'description'      
git push origin main      
elm make src/*       
<!-- reset_layout -->
<!-- end_slide -->
```latex +render
$$
1+(-1)^n=\begin{cases}
			0, & \text{if $n$ odd}\\
            2, & \text{otherwise}
		 \end{cases}
$$
```
---./assets/gviz/dataTypes.png)

