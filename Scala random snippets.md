```scala

scala> var evenList = for { i <- 1 to 20
     | if (i%2 == 0) }
     | yield i
evenList: IndexedSeq[Int] = Vector(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)

```