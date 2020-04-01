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

// list
val list = List("a", "b", "c")

// map
val map = Map(1 -> "a", 2 -> "b")

// for each 
list.foreach(value => println(value))

list.foreach(println)

list.foreach(println(_))

// traditional for each
for ( value <- list) println(value)

// reverse
for ( value <- list.reverse ) println(value)

// new ArrayList
val list = new ArrayList[String]
list.add("this is")
list add "fun" // infix notation

// BigDecimal addition
val bd_add = BigDecimal(10) + BigDecimal(20)
val bd_add = new BigDecimal(10).add(new BigDecimal(20)) // <- java

// String methods

new String("A").eq(new String("A")) // false
// comparing fresh object always false

new String("A") == new String("A") // true

//java
new String("A").equals(new String("A")) // true
// BEHAVE as java since "equals" instead of "eq"

// var args
public void add(String... names) // java

def add(names: String*) // scala

// function as argument
def test(f : () => Boolean) : Boolean = ???
test(()=> if (!x) true else false )

```