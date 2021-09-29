# Implement / Interface 2

- For methods that you do not use within a implementation of an interface UnsupportedOperatonException

```java
public class Car{
  int year;
  String make;
  String color;
}

public interface Chargable{
  public void chargable();
}

public class Honda extends Car implements Chargable;

public interface Chargable
  public void chargable(){
    sout(charging)
  }
```

- A subclass can extend from a parent class AND implement at the same time like so
- Interfaces are specific methods whereever you want it to be
- Useful when you have methods you only want in certain classes?
  - Still unsure why you cannot just add on to a subclass

```java
// Override a private method
@Override public void trimExcess()
{
  snip()
}

private void snip(){
  sout("Snip")
}
```

### Generic parameters

- Plant<T>  is going to have a type T
- T description;

```java
import garden.interfaces.Shearable;
//Plant
import garden.interfaces.Waterable;
import garden.tools.WateringHose;

import java.util.ArrayList;

public class Plant<T> implements Waterable
{
    public String color;
    String purpose;
    int height;
    boolean isEdible;
    T description;

    public void water(int waterInOz, WateringHose hose)
    {
        System.out.println("woosh woosh");
        waterInOz = 10;
        hose.color = "Brown";
    }

    public T getDescription()
    {
        return description;
    }

    public void setDescription(T description)
    {
        this.description = description;
    }
}

// Tomato
public class Tomato<T> extends Plant<T> implements Shearable
{
    String kind;

    public Tomato()
    {
        color = "Red";
    }

    @Override
    public void trimExcess()
    {
        snip();
    }

    private void snip()
    {
        System.out.println("Snip snip");
    }
}

//Heirloom Tomato
public class HeirloomTomato<T> extends Tomato<T>
{
    @Override
    public void trimExcess()
    {
        System.out.println("Please be careful!");
    }
}
```

- Tomato<T> extends Plant<T>
- Plant<String> newPlant = new Plant<>();
- newPlant.setDescription("Hello Im plant");
- Java passes everything by value

### Getter

- Class method that gets a piece of state

### Setter

- Sets a piece of state

```java
public class Node<X>{
  X value;
  Node<X> next;

  public Node(X value){
    value = value;
  }
}
```
