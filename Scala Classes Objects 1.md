##### basics
```scala
// in java
for(int i = 0; i <= 100; i++) {
    System.out.printn(i)
}
// in scala (0 and 100 inclusive )
(0 to 100).foreach(println(_))

//1) java Customer ---------------------------------------
public class Customer() {
  private final String name;
  private final String address;
  
  public Customer(String name, String address) {
    this.name = name;
    this.address = address;
  }
  
  public static void main(String[] args) {
    final Customer customer = new Customer("ddd", "tokyo");
  }
}

//corresponding scala may be 
class Customer(private val name: String,private val address: String) { 
 
}

// but when decompile scala, there are private getters also
public class CustomerScala {
    private final String name;
    private final String address;

    public static void main(String[] arrstring) {
        CustomerScala$.MODULE$.main(arrstring);
    }

    private String name() {
        return this.name;
    }

    private String address() {
        return this.address;
    }

    public CustomerScala(String name, String address) {
        this.name = name;
        this.address = address;
    }
}

// ---------------------------------------

//2) example
/*** scala Customer ---------------------------------***/
class Customer(val name: String, val address: String) { 
 
}

// compiled as 
// java -jar ~/tools/java_decompiler/cfr/cfr-0.149.jar target/scala-2.13/classes/CustomerScala.class
// no setters since "val" is mentioned 

public class CustomerScala {
    private final String name;
    private final String address;

    public static void main(String[] arrstring) {
        CustomerScala$.MODULE$.main(arrstring);
    }

    public String name() {
        return this.name;
    }

    public String address() {
        return this.address;
    }

    public CustomerScala(String name, String address) {
        this.name = name;
        this.address = address;
    }
}
/*** ---------------------------------***/

//3) example
/*** Java Customer with id ---------------------------------***/

public class Customer {
    private final String name;
    private final String address;

    private String id;

    public void setId(String id) {
        this.id = id;
    }

    public Customer(String name, String address) {
        this.name = name;
        this.address = address;
    }

    public String getName() {
        return name;
    }

    public String getAddress() {
        return address;
    }

    public static void main(String[] args) {
        final Customer customer = new Customer("dddd", "seishincho");
        customer.setId("12345");
    }
}

// scala
class CustomerWithId(val name: String, val address : String) {
  var id = ""
}
object CustomerWithId {
  def main(args: Array[String]): Unit = {
    val ddd = new CustomerWithId("ddd", "seishincho")
  }
}


//decompiled scala 
// note setter method id_$eq
public class CustomerWithId {
    private final String name;
    private final String address;
    private String id;

    public static void main(String[] arrstring) {
        CustomerWithId$.MODULE$.main(arrstring);
    }

    public String name() {
        return this.name;
    }

    public String address() {
        return this.address;
    }

    public String id() {
        return this.id;
    }

    public void id_$eq(String x$1) {
        this.id = x$1;
    }

    public CustomerWithId(String name, String address) {
        this.name = name;
        this.address = address;
        this.id = "";
    }
}




```