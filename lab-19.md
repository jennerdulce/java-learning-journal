# Imperative vs Functional

## Example

```java
public class App {
    // Imperative, maintains internal state, manipulates it and send it back
    int testInt = 0;

    public static void main(String[] args) {
        // Imperative
        App app = new App();
        int outputInt = app.addOneToInt();
        System.out.println(outputInt);

        // Functional
        int outputPassed = app.numPassed(10);
        System.out.println(outputPassed);
    }

    // Imperative; Using state
    public int addOneToInt(){
        testInt++;
        return testInt;
    }

    // Functional; Using functions
    // Not relying on internal state of program
    // Stateless, Idempotent
    public int numPassed(int numPassed){
        numPassed++;
        return numPassed;
    }
}
```

## Imperative

- What I am personally used to
- Easier to understand
- Typically ends in longer code
- May make the developer seem less experienced?

## Funcitonal

- Source: `IntStream.range(1, 11)`
- Intermediate Operations: 
    - `.skip(5)` skip the first 5
    - `.boxed()` convert to correct data type
    - `.limit(5)` only 5
- Terminal Operations: 
    - `.collect(toList())` typically used when returning a list

- Less lines of code
- Harder to understand
- Use of built in java methods
- May not be favored when working a big teams

## General

- It is good to used both techniques in conjunction with each other to accomplish a task