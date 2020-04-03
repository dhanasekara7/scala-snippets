##### Scala overriding setters and getters 2
```scala
//**************1)  java: prevent id is being set again
// isEmpty check on setId

public class Customer {
    private final String name;
    private final String address;

    private String id;

    public void setId(String id) {
        if (this.id.isEmpty()) {
            this.id = id;
        }
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
class CustomerWithId(val name: String, val address: String) {
  private var _id = ""

  def id = _id

  def id_=(value: String): Unit = {
    if (id.isEmpty) {
      _id = value
    }
  }

}

object CustomerWithId {
  def main(args: Array[String]): Unit = {
    val ddd = new CustomerWithId("ddd", "seishincho")
    ddd.id = "1234"
    println(">>>>before" + ddd.id)
    ddd.id = "9876"
    println(">>>>after" + ddd.id)
  }
}
// produces output
/*
>>>>before1234
>>>>after1234
*/

// decompile scala
//java -jar ~/tools/java_decompiler/cfr/cfr-0.149.jar CustomerWithId

public class CustomerWithId {
    private final String name;
    private final String address;
    private String _id;

    public static void main(String[] arrstring) {
        CustomerWithId$.MODULE$.main(arrstring);
    }

    public String name() {
        return this.name;
    }

    public String address() {
        return this.address;
    }

    private String _id() {
        return this._id;
    }

    private void _id_$eq(String x$1) {
        this._id = x$1;
    }

    public String id() {
        return this._id();
    }

    public void id_$eq(String value) {
        block0: {
            if (!this.id().isEmpty()) break block0;
            this._id_$eq(value);
        }
    }

    public CustomerWithId(String name, String address) {
        this.name = name;
        this.address = address;
        this._id = "";
    }
}

//2) ********* no val, no var in constructor

class MyCust(str : String) {

}

object MyCust {
  def main(args: Array[String]): Unit = {
    println("this is argument with no val or no var")
  }
}

// argument included in the generated constructor
// java -jar ~/tools/java_decompiler/cfr/cfr-0.149.jar MyCust
public class MyCust {
    public static void main(String[] arrstring) {
        MyCust$.MODULE$.main(arrstring);
    }

    public MyCust(String str) {
    }
}
```

### val, var, None table

| class Foo(? x)                       | val x        | var y        | x   | private val x | private var x |
|--------------------------------------|--------------|--------------|-----|---------------|---------------|
| getter x() created?                  | yes (public) | yes (public) | no  | yes (private) | yes (private) |
| setter x_=(y) created?               | no           | yes (public) | no  | no            | yes (private) |
| generated constructor includes "x" ? | yes          | yes          | yes | yes           | yes           |