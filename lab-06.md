# Implement / Interface

- Interface is very similar to an abstract method

```java
// Interface
public interface Animal
{
    public void noise();

    public void eat();
}

// Extends Interface
public interface ClimbingAnimal extends Animal
{
    public void climb();
}

// Implement Interface
public class Sloth implements ClimbingAnimal
{
    Sloth()
    {
    }

    @Override
    public void noise()
    {
        System.out.println("Yaaaawwwwwnnnnn");
    }

    @Override
    public void eat()
    {
        System.out.println("chew chew chew");
    }

    @Override
    public void climb()
    {
        System.out.println("climb climb climb");
    }
}
```

- When implementing an interface, you must `@Override` all of the methods of the interface for every Implementation
- Why would I want an interface besides a Subclass?
  - Give implementing interfaces freely to do things
  - I do these things but I'm not going to tell you how
- You build off classes
- Combared to classes.. Interfaces is a contract; Given a contract, you must ensure that you create what the interface asks for
- PRO: Helps keep track of what you need
- CON: Drawback have to have every method from interface

## General Tips

- String dollarSign = "$"
- String nDollarSigns = dollarSign.repeat(3);
