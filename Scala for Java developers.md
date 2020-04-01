##### basics
```scala
//  reassign
val language = "Scala"
var lang = "Java" // can reassign
lang = "Java 13"

def min(x: Int, y:Int) : Int = if (x < y) x else y

// buggy
def min_buggy(x: Int, y:Int) : Int = {
    if(x < y)
      x
    y
} // always return y

// invisible .
20+10 
20.+(10)
//also
20 + 10
"aBC".replace("a", "A")
//same as
"aBC" replace("a", "A") 

//
```