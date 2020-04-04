### Fields within classes
```scala

// java
public class Counter {
  private int count = 0;
  public Counter() {
  }
  public void increment() {
    count++
  }
  public int getCount() {
     return count
  }
}

//scala
class Counter() {
  private var count = 0
  
  def increment() {
    count += 1 
  }
  
  def getCount = count
}

//2)*********************----------------------
// java with constructor
public class CustomerWithCons {
    private final String fullname;

    public CustomerWithCons(String forename, String initial, String surname) {
        if (initial != null && !initial.isEmpty()) {
            this.fullname = String.format("%s %s %s", forename, initial, surname);
        } else {
            this.fullname = String.format("%s %s", forename, surname);
        }
    }

    public CustomerWithCons(String forename, String surname) {
        this(forename, "", surname);
    }
}
//scala
class CustomerWithCons(forename : String, initial : String, surname : String ) {
  val fullname = String.format("%s %s %s", forename, initial, surname)
  
  def this(forename : String, surname : String) {
    this(forename, "", surname)
  }
}

// can be written with default supplied value "initial="" 
// but anyhow when calling need to supply 3 arguments
// or call with argument name as
// val cc = new CustomerWithCons(forename = "ab", surname = "cd")
class CustomerWithCons(forename : String, initial : String = "", surname : String ) {
  val fullname = if (initial!=null && !initial.isEmpty) {
    forename + " " + initial + ". " + surname
  } else {
    forename + " " + surname
  }
}

//not enough arguments with the following case
// 1) when default value is not given in the argument
// 2) and not all the arguments passed when calling constructor
// val cc = new CustomerWithCons(forename = "ab", surname = "cd")
class CustomerWithCons(forename : String, initial : String, surname : String ) {
  val fullname = if (initial!=null && !initial.isEmpty) {
    forename + " " + initial + ". " + surname
  } else {
    forename + " " + surname
  }
}

### Singleton class
// java
import java.util.logging.Level;

public final class JavaLogger {
    private static final JavaLogger INSTANCE = new JavaLogger();
    private JavaLogger() {}
    public static JavaLogger getLogger() {
        return INSTANCE;
    }
    public void logme(Level level, String string) {
        System.out.printf("%s %s%n", level, string);
    }
    public static void main(String... args) {
        JavaLogger.getLogger().logme(Level.INFO, "all is well");
    }
}

//Java enum instead of Singleton
import java.util.logging.Level;

public enum JavaLoggerEnum {
    JAVA_LOGGER;
    public void logme(Level level, String string) {
        System.out.printf("%s %s%n", level, string);
    }
}

// scala 
import java.util.logging.Level;
object Logger {
  def log(level: Level, string : String) = {
    // %n for newline ( Platform-specific line separator.)
    printf("%s %s%n", level, string)
  }
}
// > Logger.log(Level.INFO, "ancd")
//  INFO ancd

// java 
// Customer with sequenceOfIds

public class CustomerWithSeqId {
    private static Integer sequenceOfIds;

    private final String name;
    private final String address;

    private Integer id;

    public CustomerWithSeqId(String name, String address) {
        this.name = name;
        this.address = address;
        this.id = nextId();
    }

    private static Integer nextId() {
        if(sequenceOfIds == null) {
            sequenceOfIds = Integer.valueOf(1);
        }
        return sequenceOfIds++;
    }

    public static void main(String[] args) {
        CustomerWithSeqId cu = new CustomerWithSeqId("ddd", "seishincho");
        System.out.println(cu.id);
    }
}


// scala
class Customer(val name: String, val address: String) {
  private val id = Customer.nextId()
}
object Customer {
  private var seqIds = 0
  // private def nextId() wont work
  def nextId() = {
    seqIds += 1
    seqIds
  }
}

//**************  // factory method
// using apply method for the above scala
class Customer(val name: String, val address: String) {
  private val id = Customer.nextId()
}
object Customer {
  // factory method
  def apply(name: String, address: String) = new Customer(name, address)
  private var seqIds = 0
  // private def nextId() wont work
  def nextId() = {
    seqIds += 1
    seqIds
}
}


// apply method
object Greet {
 def apply(name: String): String = {
   "Hello %s".format(name)
 }
}

// I can call apply explicitly if I want:
Greet.apply("ddd")
// => "Hello ddd"

// Or I can call Greet like it is a function:
Greet("ddd")
// => "Hello ddd"

//this wont work
val greeting = new Greet("bob")


//********************* case class
case class Person(name : String, address : String ){}

// calling 3 ways of case class
val person1 = new Person("ddd", "seishincho")
val person2 = Person.apply("d", "sei")
val person3 = Person("de", "eesei")


//********************* apply as class builder
case class Apply2CreateAnotherClass(name: String, address: String) {
}

class MySample(val name: String, val address: String) {
}

object MySample {
  def apply(name: String, address: String): Apply2CreateAnotherClass = new Apply2CreateAnotherClass(name, address)

  def main(args: Array[String]): Unit = {
    // MySample constructor is called
    val mySample1 = new MySample("ddd" , "seishincho")
    println(mySample1) // MySample@47f37ef1

    // apply method is called
    val mySample2 = MySample("ddd" , "seishincho")
    println(mySample2) // Apply2CreateAnotherClass(ddd,seishincho)

  }
}
// sample usage
abstract class DatabaseDriver {
  // some database stuff
}

object DatabaseDriver {
  def apply(config: Configuration) = config.dbType match {
    case "MYSQL" => new MySqlDriver()
    case "PSQL" => new PostgresDriver()
    case _ => new GenericDriver()
  }
}

// now I get the right version!
// NOTE : no new when calling
val mydatabase = DatabaseDriver(dbConfig)


//********************** apply function as anonymous function
val func = (x: String) => "hello %s".format(x)
func("world") // => hello world
func.apply("world")// => hello world


//************** apply function in a class ( not an object)
class Amazing {
  def apply(x: String) = "Amazing %s!".format(x)
}
val amazing = new Amazing()
amazing("world")
// => Amazing world!
```