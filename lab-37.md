# Simple Storage Service

- S3:
  - Can store objects that are max 5 TB in size
  - Cannot update (only replace)
  - No indexes
  - No search
  - No transactions
  - No queries
  - Made for High, Bursty output, but not low latency
  - S3 works with whole objects

- DynamoDb: Can store items that are max 400k
  - Throttles for small objects even at fairly small throughput
  - Is good for low latency and sustained
  - A waiter servicing a few tables in a sustained way
  - Low latency
  - Not good for high bursts or high throughput
  - Can work with parts of an item or table

## Setup

- Add S3 Dependency to build.gradle
- Add S3 Plugin to AppFile
- `amplify add storage`
- Name resource: `tasknamestorage` you cannot rename your resource
  - `amplify remove storage` if you need later
- Bucketname
- Auth users only
- What kind of access for Auth? CRUD
- Trigger Lamda resource? No
- `amplify push`

## Main Activity

```java
// Test S3 file upload
        // 1. Make a file in this new place
        File testFileFolder = new File(getApplicationContext().getFilesDir(), "testFileName")
        try (BufferedWriter testFileBufferedWriter = new BufferedWriter(new FileWriter(testFileFolder));){
            testFileBufferedWriter.append("This is a test");
        } catch (IOException ioe){
            Log.i(TAG, ioe.getMessage());
        }
        
        // 2. S3 storage
        Amplify.Storage.uploadFile(
                "testFileKey",
                testFileFolder,
                success -> {Log.i(TAG, "S3 Upload Success: " + success.getKey());},
                failure -> {Log.i(TAG, "S3 Upload Failed" + failure.getMessage(), failure);}
```

- Check S3 buckets
- Download and open in notepad

## Boiler Plate

```java
    protected void selectFileAndSaveToS3(){
        // Grab file from filepicker
        Intent imageFilePickIntent = new Intent(Intent.ACTION_GET_CONTENT);
        imageFilePickIntent.setType("*/*"); // Allows one kind of category of file
        // Restrictions
        imageFilePickIntent.putExtra(Intent.EXTRA_MIME_TYPES, new String[]{"image/jpg", "image/png"});
        // Brings you to photos app on your phone
//        ActivityResultLauncher<Intent> activityResultLauncher = getImagePickingActivityResultLauncher();
        activityResultLauncher.launch(imageFilePickIntent);
    }

    protected ActivityResultLauncher<Intent> getImagePickingActivityResultLauncher(){
        ActivityResultLauncher<Intent> imagePickingActivityResultLauncher = registerForActivityResult(
                new ActivityResultContracts.StartActivityForResult(),
                new ActivityResultCallback<ActivityResult>()
                {
                    @Override
                    public void onActivityResult(ActivityResult result) {
                        // Check to see if result is okay and start processing
                        if(result.getResultCode() == Activity.RESULT_OK){
                            if(result.getData() != null){ // returns an intent
                                Uri pickedImageFileUri = result.getData().getData();
                                try {
                                    InputStream pickedImageInputStream = getContentResolver().openInputStream(pickedImageFileUri);
                                    String pickedImageFilename = getFilenameFromUri(pickedImageFileUri);;
                                    Log.i(TAG, "Succeeded in getting input stream from file on phone! Filename is: " + pickedImageFilename);
                                    uploadInputStreamToS3(pickedImageInputStream, pickedImageFilename);
                                } catch (FileNotFoundException fnfe){
                                    Log.e(TAG, "File not found File picker: " + fnfe.getMessage(), fnfe);
                                }
                            }
                        }
                    }
                }
        );
        return imagePickingActivityResultLauncher;
    }

    // Make getFilenameFromUri Method
    @SuppressLint("Range")
    protected String getFilenameFromUri(Uri uri) {
        String result = null;
        if (uri.getScheme().equals("content")) {
            try (Cursor cursor = getContentResolver().query(uri, null, null, null, null))
            {
                if (cursor != null && cursor.moveToFirst())
                {
                    result = cursor.getString(cursor.getColumnIndex(OpenableColumns.DISPLAY_NAME));
                }
            }
        }
        if (result == null) {
            result = uri.getPath();
            int cut = result.lastIndexOf('/');
            if (cut != -1) {
                result = result.substring(cut + 1);
            }
        }
        return result;
    }

    private int getSpinnerIndex(Spinner spinner, String stringValueToCheck){
        for (int i = 0;i < spinner.getCount(); i++){
            if (spinner.getItemAtPosition(i).toString().equalsIgnoreCase(stringValueToCheck)){
                return i;
            }
        }
        return 0;
    }

    protected void uploadInputStreamToS3(InputStream pickedImageFileInputStream, String pickedImageFilename){
        Amplify.Storage.uploadInputStream(
                pickedImageFilename,
                pickedImageFileInputStream,
                success -> {
                    Log.i(TAG, "Succeeded in getting uploaded file to S3. Key is: " + success.getKey());
                    awsImageKey = success.getKey();
                },
                failure -> {
                    Log.e(TAG, "Failed in getting uploaded file to S3. Key is: " + pickedImageFilename + " with error: " + failure.getMessage(), failure);
                }
        );
    }
```

## General Notes

- Small refactors here and there go a long way
- Completeable  Future and Image picker do not interact with each other well
  - Flaw in  completeable future
  - Do not Run completeable future and   image picker within the on click listener at the same time
- You can use intent to open other apps on your phone, such as your photos library
- "Must call register before started"

## Reflect

- What went well, that I might forget if I don’t write down?
  - Refactor
  - Completable futures and image pickers dont mesh
  - Refer to boiler plate
  - If a variable is null, check to see where it is declared

- What did I learn today?
  - I learned how to use AWS Amazon S3

- What should I do differently next time?
  - Keep improving on debugging

- What still puzzles me, or what do I need to learn more about?
  - Lots of boiler plate AGAIN.
  - I was able to complete the lab and refactor what I needed with minimal help

- Is the assignment complete? If not, where exactly did you leave off, and what work remains?
  - Yes this assignment is complete
