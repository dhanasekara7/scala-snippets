##### scala for the impatient
```scala
val xmax, ymax = 100 // Sets xmax and ymax to 100

// greeting and message are both strings, initialized with null
var greeting, message: String = null
 
1.to(10) // Yields Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)1.to(10)
// Yields Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// StringOps (hundreds of methods)
"Hello".intersect("World") // "lo"
//Use `s.toSeq.intersect(...).unwrap` instead of `s.intersect(...)`
"Hello".toSeq.intersect("World")

/***
// String augments with StringOps
// like that
RichInt, RichDouble, RichChar
***
```