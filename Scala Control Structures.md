"##### Scala control structures
```scala
// in scala, it is expression rather than a statement

object Customer {
    def create(name : String, age : Int) = Customer {
        val cust = if (age > 60) {
                new SeniorCustomer("name")
            } else {
                new NormalCustomer("name")
            }
        cust
    }
}

// match case
object Switch {
    val month = "August"
    var quarter = ""

    month match {
        case "January" => quarter = "first"
        case "August" | "September" =>
        case "December" => quarter = "last"
        case _ => quarter = "unknown quarter"
    }
    println(month + " is in " + quarter)
}
// above returns "August is in "


// match case with case checked for detail
object Switch {
    val month = "August"
    var quarter = ""

    month match {
        case "January" => quarter = "first"
        case "August" | "September" => quarter = "mid"
        case "December" => quarter = "last"
        case _ => quarter = "unknown quarter"
    }
    println(month + " is in " + quarter)
}
// above returns "August is mid"

// match case, assigned to val , ( not var, since not changed)
object Switch {
    val month = "August"
    val quarter = month match {
        case "January" => "first"
        case "August" | "September" => "mid"
        case "December" =>  "last"
        case _ =>  "unknown quarter"
    }
    println(month + " is in " + quarter)
}

// for loop with infix notation ( 0 to 10)
for(i <- 0 to 10) {
    println(i)
}

(0 to 9).foreach(i => println(i))

(0 to 9).foreach(println(_))

// breakable
import scala.util.control.Breaks._
breakable {
    for(i <- 0 to 10) {
        System.out.println(i)
        if (i == 5) {
            break()
        }
    }
}

```