# AWS Serverless and Amplify

## Models

- AWS AppSync supports Scalar
- Amplify > backend > amplifyDatasource > schema
- Scalar types: [Link](https://docs.aws.amazon.com/appsync/latest/devguide/scalars.html)
- A lot of Java data types are not in Scalar
- After you've  created models: `amplify codegen models`
  - Takes graphQL models and makes Java code out of it
  - Also whos you where it in created
  - Cannot change these methods. `amplify codegen models` rewrites the class, defaulting changes
- Make changes at the `schema.graphql` then `amplify codegen model`

### Create model based on TaskItem Class

- Make types that mirror TaskItem properties

```java
Type TaskItem @model {
  id: ID!
  taskName: String
  timeAdded: AWSDateTime
  status: String
}
```

- Now that we have created a model, then execute: `amplify codegen models`
- Use model to display info on your app
- `amplify status` Operation should say update
- Update by `amplify push`

## Replacing code

- Delete TaskItem model
- Will point you to where it breaks in your application.. Replace code at these points
- Import class from the new location
- To access ID has `.getId()`
- Need to use builder pattern to construct

## Create Application Class

- [Example](https://stackoverflow.com/questions/18002227/why-extend-the-android-application-class)
- Create class `extends Application`  
- `Amplify.addPlugin(new AWSApiPlugin());`
- Put `Amplify.configure(getApplicationContext())` in here

### Android Manifest

- `android:name=".taskmaster"`

### Creating a new Object

```java
// Not that there is no new
TaskItem taskItem = TaskItem.builder()
  .taskName(taskNamePlainTextString)
  .status(TaskStatusEnum.UNKNOWN)
  .otherProperty(PlainTextString)
  .build()

Amplify.API.mutate(
  // Used to make new objects in DynamoDB
  ModelMutation.create(taskItem),
  success -> log.i(TAG, "Succeeded"),
  failure -> log.i(TAG, "Failed")
  )
)
```

## When you see version in your data table

- `amplify update api`

## Display Database Data

```java
Amplify.API.query(
  ModelQUery.list(TaskItem.class),
  success -> {
    List<TaskItem> taskItemList = new ArrayList<>();
    fpr (TaskItem taskItem : success.getData()){
      taskItemList.add(taskItem)
    }
    runOnUiThread(task -> )
  }
)

```