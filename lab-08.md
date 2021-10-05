# Gson and JSON

- Today I we learned how to use Gson and build out instances of objects utilizing strings
- We also learned how to retrieve a string using a filepath

- [Array of Objects example ](https://github.com/jennerdulce/quotes/blob/main/app/src/main/java/quotes/Quote.java)

```java
public class Quote {
    ArrayList<Quote> quotes;
    ArrayList<String> tags = new ArrayList<>();
    String author;
    String likes;
    String text;

    public Quote(ArrayList<String> tags, String author, String likes, String text) {
        this.tags = tags;
        this.author = author;
        this.likes = likes;
        this.text = text;
    }

    public static String randomQuote(String path) throws IOException {
        File file = new File(path);
        // Read file
        FileReader quotesFileReader = new FileReader(file);

        Gson gson = new Gson();

        // Creates array of quotes
        Quote[] quote = gson.fromJson(quotesFileReader, Quote[].class);
        int x = (int) (Math.random()* quote.length);
        String someQuote = quote[x].author + "\n";
        someQuote += quote[x].text;
        System.out.println(someQuote);
        return someQuote;
    }
}
```

- [Singular Object Example](https://github.com/codefellows/seattle-java-401d11/blob/main/class-08/demo/unicorns/app/src/main/java/unicorns/App.java)

```java
public class App {
    public static void main(String[] args) throws IOException
    {
        ArrayList<Unicorn> classUnicorns = new ArrayList<>();
        ArrayList<String> mattColors = new ArrayList<>();
        mattColors.add("Blue");
        Unicorn matticorn = new Unicorn(mattColors, 20, false, "Matticorn");
        ArrayList<String> patrickColors = new ArrayList<>();
        patrickColors.add("Blue"); patrickColors.add("White"); patrickColors.add("Red");
        Unicorn patricorn = new Unicorn(patrickColors, 30, true, "Patricorn");
        ArrayList<String> jenColors = new ArrayList<>();
        jenColors.add("Black");
        Unicorn jennicorn = new Unicorn(jenColors, 35, true, "Jennicorn");
        ArrayList<String> haustinColors = new ArrayList<>();
        haustinColors.add("Orange"); haustinColors.add("White");
        Unicorn hausicorn = new Unicorn(haustinColors, 14, false, "Hausicorn");

        classUnicorns.add(matticorn);
        classUnicorns.add(patricorn);
        classUnicorns.add(jennicorn);
        classUnicorns.add(hausicorn);

        Gson gson = new Gson();
        String matticornJson = gson.toJson(matticorn);
        System.out.println(matticornJson);

        String edicornJson =
                "{" +
                "   \"colors\": [\"black\", \"white\", \"purple\"]," +
                "   \"hornLength\": 2," +
                "   \"hasWings\": true," +
                "   \"name\": \"Edicorn\"" +
                "}";

        //Unicorn edicorn = gson.fromJson(edicornJson, Unicorn.class);

        File unicornFile = new File(".\\app\\src\\test\\resources\\unicorn.json");
        FileReader unicornFileReader = new FileReader(unicornFile);

        Unicorn edicorn = gson.fromJson(unicornFileReader, Unicorn.class);

        // try-with-resources

        File unicornFileOut = new File(".\\app\\src\\test\\resources\\unicorn2.json");
        try (FileWriter unicornFileWriter = new FileWriter(unicornFileOut))
        {
            gson.toJson(edicorn, unicornFileWriter);
            System.out.println("test");
        }
        //gson.
        //Cupcake cupcake = gson.fromJson(edicornJson, Cupcake.class);
    }
}
```

```java

public class Unicorn
{
    ArrayList<String> colors;
    int hornLength;
    boolean hasWings;
    String name;

    public Unicorn(ArrayList<String> colors, int hornLength, boolean hasWings, String name)
    {
        this.colors = colors;
        this.hornLength = hornLength;
        this.hasWings = hasWings;
        this.name = name;
    }
}

public class Cupcake
{
    ArrayList<String> colors;
    int hornLength;
    boolean hasWings;
    String name;

    public Cupcake(ArrayList<String> colors, int hornLength, boolean hasWings, String name)
    {
        this.colors = colors;
        this.hornLength = hornLength;
        this.hasWings = hasWings;
        this.name = name;
    }
}
```
