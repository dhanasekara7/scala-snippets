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
```