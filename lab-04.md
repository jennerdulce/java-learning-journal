# Lab: 04 - Bitmap, Classes, OOP

## Classes

```java

// Class boilerplate
public Class1 {

  // Privacy
  private int privateInt;

  // Package Protected / Default
  int someint;

  // Classes that extend can use
  protected String coolString;
  private ArrayList<Integer> someNumbers;

  // If you want to use the same variable name of the Original class
  public Class1(int _myint){
    
  }

  // Default Constructor
  public Class1(){
    // Code Block
  }

  public int addNumbers)_{
    // Code block
  }
}
```

### Extending a class

```java
// Consider the parent class
public class Pastry {
    boolean isIced;
    String flavor;
    boolean isVegan;

    // Makes consistent throughout  all objects and can be accessed anywhere like a global variabel
    // Reassigning this variable in some other part of the code changes it everywhere
    // If you want to access static variable, You do not have to instantiate the object before using it. just do Class.variable;
    static String baker = "Shan";

    public Pastry(boolean isIced, String flavor, boolean isVegan){
        this.isIced = isIced;
        this.flavor = flavor;
        this.isVegan = isVegan;
    }
}

```

```java
// Consider the child class
public class Donut extends Pastry{
  // Unique properties of the donut class
    boolean isCake;
    char size;

  // Need to include properties from parent class in constructor as well as in super()
    public Donut(boolean isIced,
                 String flavor,
                 boolean isVegan,
                 boolean isCake,
                 char size) {
        super(isIced, flavor, isVegan);
        this.isCake = isCake;
        this.size = size;
    }

    // Java does not have a way to print out the whole object in a neat way. You have to override the toString() method in order to do this.
    @Override
    public String toString(){
        String description = "";
        description += "Donut \n";
        description += "isIced: " + this.isIced + "\n";
        description += "flavor: " + this.flavor + "\n";
        description += "isVegan: " + this.isVegan + "\n";
        description += "isCake: " + this.isCake + "\n";
        description += "size: " + this.size;
        return description;
    }
    public void helloWorld(){
        System.out.println("Hello World");
    }

//    public String otherToString(){
//        String description = String.format()
//    }
}
```

### Accessing properties from subclass

```java
package BakeryDemo;

public class App {

    public static void main(String[] args) {
      // This creates an arrayList called 'pastires' as a property
        Bakery bestBakery = new Bakery();
        Donut donut1 = new Donut(true, "Chocolate", true, true, 'S');
        Cake cake1 = new Cake(false, "Vanilla", true, 5);


        bestBakery.pastries.add(donut1);
        bestBakery.pastries.add(cake1);
        Pastry pastry1 = bestBakery.pastries.get(0);
        Pastry pastry2 = bestBakery.pastries.get(1);

//        Will not work because currently pastry, although a donut, is created as a pastry.. However, pastry1 is in fact an instance of Donut
          System.out.println(pastry1.isCake());
//        In order to access  properties of specific subclass, you have to cast it to the subclass

        if (pastry1 instanceof Donut){
            // isCake now works in here after being casted
            Donut sameDonut = (Donut) pastry1;
            sameDonut.isCake();
            System.out.println(sameDonut.toString());
        }
        if(pastry2 instanceof Cake){
          // Same thing, you have to cast into the subclass if you want to access properties
            Cake sameCake = (Cake) pastry2;
            System.out.println(sameCake.numberOfLayers);
        }
    }
}

```

## Bitmap Lab

### How to locate your directory

- Get used to locating a file in someway
  - Easiest way to find current directory: `System.out.println(System.getProperty("user.dir"));`
  - Will return something like `"/Users/jenner/codefellows/Java-401/bitmap-transformer/app/src/main/resources/baldy-8bit.bmp"`

### How to alter an image

1. Create a `BufferedImage`

- `BufferedImage = ImageIO.read(new File(filePath))`
  - You now have access to many methods of the `BufferedImage` class

2. Modify Image

- Other classes are used in conjunction with Buffered image:
  - ColorSpace
  - ColorConvertOp
  - Graphics2D

3. Export Image

```java
// Filepath should include the name of the image file at the end of the file path
// img in this case is the `BufferedImage you were working with`
File outputFile = new File(this.outputFilePath + "/" + transformImageName + ".bmp") ;
ImageIO.write(img, "bmp", outputFile);
```

## General Tips

- Control click on methods to find out where they are being used
- Setting args
- Edit Configs
- program args: Allows you to hand in things to the main
- .\gradlew run --args "Brandon Patrick"