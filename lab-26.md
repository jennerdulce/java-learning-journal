#

## Basic Andriod setup

- Empty activity
- Activities are close to pages in a web app
- Kotlin
- CamelCase name
- Package name: `com.jennerdulce.buystuffdemo`;
  - Do not use `com.example`
- Minimum SDK:
  - Can run on certain devices and have certain functionality;
  - Older versions SDK does not support new funcationality
  - Not everyone have the newest technology to use the newer SDK
- Ignore legacy

## After created

- Switch to project view on the top left
- 2 build.gradels
  - Project level
    - Do not really have to tamper with
  - App level
    - Will be importing dependencies in this one
    - minSDk #
      - Anyone below this SDK will not be able to run app
      - Can run above the SDK
      - If you want to change to a newer level this is what you have to change
      - applicationId
        - If you decide to change package name
        - Or refactor and rename your folder on the left side bar
          - 'rename package'
            - search for commetns and string
            - search for text occurrences
- Turn off compact middle packages
- compileOptions
  - `JavaVersion.VERSION_11`
  - Keep build environments the same
  - Andriod actually doesn't run on java
  - They implements SOME thing when they feel like

## AndriodManifest.xml

- Where activities will live

## Add virural andriod devices

- Tools > AVD manager > create phone
- Need playStore access
- API level: pick highest
- pissibly need an ARM build for newer devices
- AVD just skip and create
- Select virtural device on the top left AND build configuration
- design
- blueprint view
- or both

## activity_main

- Declared attribtues tab on the right
- Internationalizion is very important and prevent addition to hard coded code
- Use streams to make dynamic
- Small button to the right of the text box
- Adds string to values > strings.xml;
- ALWAYS FIX WARNING
  - Google will not allow you to publish

## Constraints

- Constraints set your buttons and things on the GUi
- YOU NEED CONSTRAINTS

## Event setup

- Naming conventions
  - Search andriod style guides
  - in MainActivity.java: `findViewById(R.id.productNameTextView);`
  - in order to work with the string, we have to convert to a text view: `TextView productNameTextView = findViewById(R.id.productNameTextView);`
  - Now we can alter the code: `productNameTextView.setText(R.string.TextingText);`
  - Reaches in the values > string.xml

## Intent

- Going to a different activity


## Working With buttons

```java
// Add Task Intent Button
        Button addTaskButton = (Button) findViewById(R.id.addTaskButton);
        addTaskButton.setOnClickListener(view -> {
            Intent addTaskIntent = new Intent(MainActivity.this, AddTaskActivity.class);
            startActivity(addTaskIntent);
        });
```

- Select the button
- Add Listener
- Navigate to different activity
  - Set new intent
  - Put your current activity and your second activity as arguments
  - `startActivity()`
- How to add extra Info: `orderFormIntent.putExtra(PRODUCT_NAME_STRING, productNamePlainText.getText());` to pass into the next activity
  - Retrieve the extras by:
    ```java
    Intent intent = getIntent();
        String productName = intent.getExtras().get(MainActivity.PRODUCT_NAME_STRING).toString();
    ```


## Setting Text

```java
// Step 1. Select Element
        TextView productNameTextView = findViewById(R.id.productNameTextView);

        // Step 2. Change text with a
        productNameTextView.setText(R.string.TextingText);
        // or
        productNameTextView.setText("Some text here");
```

- Select Element
- Use `setText`
- `R.string.TextingText` This example goes into the values  dirctory and retrieves string from the strings.xml

## Retrieve from Input Text

```java
  TextView productNamePlainText= (TextView) findViewById(R.id.productNamePlainText);
  submitStatusTextView.setText(productNamePlainText.getText());
```

- Target the plain text
- `productNamePlainText.getText()`

## Other Tips

- `Log.i("RANDOM TEXT", "HELLO");` is similar to Console.log
