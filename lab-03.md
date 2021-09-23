# Read: 03 - Maps, primitives, File I/O

## HashMaps<Key, Value>

```java
Hashmap<String, Boolean> dailyAttendance = new Hashmap<>()

      dailyAttendance.put("Ed", false);
      // You can check for null ****
      if(dailyAttendance.get("Santa") != null)
      if(dailyAttendance.containsKey(""))

// Another exmaple of what hashmap you can build
HashMap <ArrayList<Integer>, ArrayList<Integer>> dailyAttendance = new HashMap<>();
```

## HashSet<Key>

- Similar to an array but cannot contain duplicates
- Similar to HashMaps, has methods to access and modify contents of HashSet

```java
classStudents.add("Brandon")
classStudents.addAll(1, 2, 3, 4, 5)
classStudents.contains("Brandon")
```

## File.io

```java
// Obtain the path by
Path filePath = Paths.get(".");
System.out.println(filePath.toAbsolutePath())

// Replace path '.' with the actual path by copy and pasting path from the console
Path filePath = Paths.get("actual Path");

// Create scanner and use scanner methods to read the file
Scanner scanner = new Scanner(filePath);



// EXAMPLE
public static String linter(String filePath) {
        int lineCounter = 0;
        String errorMessage = "";
        try {
          // Create Path
            Path newPath = Paths.get(filePath);
            // Use path in scanner
            Scanner scanner = new Scanner(newPath);
            while(scanner.hasNextLine()){
                lineCounter++;
                // scanner methods
                String currentString = scanner.nextLine();
                if(currentString.isEmpty() || currentString.endsWith(";") || currentString.endsWith("{") || currentString.endsWith("}") || currentString.contains("if") || currentString.contains("else")){
                    continue;
                } else {
                    errorMessage += "Line " + lineCounter + ": Missing semicolon.\n";
                }
            }
        } catch (Exception e){
            System.out.println(e + " Line: " + lineCounter);
        }
        return errorMessage;
    }
```

## Other notes

- `console .\gradlew run`
- `.equals()` when comparing
- You are able to compare null
