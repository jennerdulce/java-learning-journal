# Intent Filter

- Explicit Intent: Go to another specific place between activities

- Implicit Intent: Other applications can satisfy by opening other applications
  - Use chrome to open
  - Open image in chrome to open image in application
  
  - You need to specify activites you intend on using
  - Whatever activity you want this in.
  - head to that activity within the andriodmanifiest.xml
    - add intent filter here


```java
<activity
            android:name=".activities.AddTaskActivity"
            android:exported="true" />
            <intent-filter>
                
            </intent-filter>
```

- Separate input streams


## Share boiler plate
```java
Intent intent = getIntent();
        if((intent.getType() != null) && (intent.getType().startsWith("image/"))){
            Uri incomingFileUri = intent.getParcelableExtra(Intent.EXTRA_STREAM);
            if (incomingFileUri != null){
                try{
                    pickedImageFileUri = incomingFileUri;
                    pickedImageFilename = getFilenameFromUri(incomingFileUri);
                    InputStream incomingImageFileInputStream = getContentResolver().openInputStream(incomingFileUri);
                    ImageView previewShareImageView = findViewById(R.id.previewShareImageView);
                    previewShareImageView.setImageBitmap(BitmapFactory.decodeStream(incomingImageFileInputStream));
                } catch (FileNotFoundException fnfe){
                    Log.e(TAG, "Could not get file from file picker! " + fnfe.getMessage(), fnfe);
                }
            }
        }

```

## Reflect

- What went well, that I might forget if I don’t write down?
  - Refer to notes above

- What did I learn today?
  - Today I learned how to use an Explicit Intent. Being able to open my application by using a different application
  - Using google and being able to share

- What should I do differently next time?
  - Everything went well. Just need to study up a bit more on all of the parts

- What still puzzles me, or what do I need to learn more about?
  - Still a lot of boilerplate. The different Objects that are created and how to figure out how to handle them..
  - What all the parts mean:
    - Input Stream
    - Uri
    - When to use runOnUiThread

- Is the assignment complete? If not, where exactly did you leave off, and what work remains?
  - Today's assignment is complete!
