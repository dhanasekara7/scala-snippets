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

// "extends" rather than implements
// override in front of def is optional,
// since it is abstract method (in trait Readable)
// Additional traits "with" keyword
class FileReader(file : File) extends Readable with AutoCloseable {
    def read(buffer: CharBuffer) : Int = {
        val linesRead: Int = 0
        linesRead
    }

    def close() : Unit = ???
}

// default method in java 8
interface Sortable<A extends Comparable<A>> extends Iterable<A> {
    default public List<A> sort() {
        List<A> list = new ArrayList<>();
        for(A element: this)
            list.add(A);
        // natural ordering (first, second) -> first.compareTo(second)
        list.sort((first, second) -> first.compareTo(second));
        return list;
    }
}
// scala
trait Sortable[A <: Ordered[A]] extends Iterable[A] {
    def sort: Seq[A] = {
        this.toList.sorted
    }
}

class Customer .... extends Ordered[Customer] {
    ...
    def compare(that : Customer) : Int = name.compareTo(that.name)
    override def toString : name + " $ " + total

}

// trait and subclass

trait Counter {
    protected var count = 0
    def increment()
}

class IncrementByOne extends Counter {
    // increment() is abstract in trait, so "override" is not mandatory
    override def increment(): Unit = count += 1
}

class ExponentialIncrementer(rate : Int) extends Counter {
    def increment(): Unit = {
        count += rate * count
    }
}

class Foo {
    val foo = new IncrementByOne
    foo.count // not allowed, because "count" is protected,
    //only on the subtypes it is allowed
}

// abstract class
abstract class AbstractCustomer {
    def total: Double
}

// forces subtypes to force a value for "count",
// since it is NOT initialized
trait Counter {
    protected var count
    def increment()
}

// super class method calling order
// right to left
class Animal
trait HasWings
trait Bird extends HasWings
trait HasFourLegs extends Animal

// if all the move has "move" method
// super.move in the FlyingHorse calls
// the right to left order
// FlyingHorse HasFourLegs Bird Animal
// this is called "linearization"
// ( not avl in java 8)
class FlyingHorse extends Animal with Bird with HasFourLegs



````