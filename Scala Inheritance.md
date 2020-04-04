##### Scala Inheritance
### Inheritance
## Sub-type inheritance
## Interfaces
## Abstract class
## "Mixin" Behaviour
```scala

// java Customer and DiscountedCustomer
public class Customer {
    private final String name;
    private final String address;
    private final ShoppingBasket basket = new ShoppingBasket();

    public Customer(String name, String address) {
        this.name = name;
        this.address = address;
    }

    public void add(Item item) {
        basket.add(item);
    }

    public Double total() {
        return basket.value();
    }
}

public class DiscountedCustomer extends Customer {
    public DiscountedCustomer(String name, String address) {
       super(name, address);
    }

    public Double total() {
        return 0.8 * super.total();
    }
}

// ************* Scala Customer and DiscountedCustomer

class Customer(val name : String, val address : String) {
    private final val basket = new ShoppingBasket

    def add(item : Item) {
        basket.add(item)
    }

    def total : Double = {
        basket.value
    }
}

// ** note down the arguments , no val, var etc
class DiscountedCustomer(name : String, address : String)
 extends Customer(name, address) {
    override def total : Double = {
        super.total * 0.8
    }
 }
// anonymous sub classes
object DiscountedCustomer {
    def main(args : Array[String]) {
        val dc = new DiscountedCustomer("ddd", "seishincho")
        // note down after Item no arguments
        // note down no override
        dc.add( new Item {
                def price = 2.5
            }
        )
        dc.add( new Item {
                def price = 3.5
            }
        )
    }
}

#### Interfaces
trait Readable {
    def read(buffer: CharBuffer) : Int
}

// extends rather than implements
// override in front of def is optional,
// since it is abstract method (in trait Readable)

class FileReader(file : File) extends Readable {
    def read(buffer: CharBuffer) : Int = {
        val linesRead: Int = 0
        linesRead
    }
}

````