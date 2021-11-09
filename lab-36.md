# Cognito

## build.gradle

- Add to build.gradle
  - `implementation 'com.amplifyframework:aws-auth-cognito:1.28.3'`
  - Sync
- In terminal, go to app
  - amplify add auth
  - Default config
  - How do you want users to sign in? email
    - Will send verification to email later
    - No, I am done
- amplify push

## Application Document

- Application.java
- Amplify.addPlugin(new AWSCognitoAuthPlugin())
  - Before Amplify.configure

## Signup

### Hardcoded

```java
// Create a user
Amplify.Auth.signUp("jennerdulce@hotmail.com",
                      "password",
                      AuthSignUpOptions.builder()
                        .userAttribute(AuthUserAttribute.email(), "jennerdulce@gmail.com")
                        .userAttribute(AuthUserAttributeKey.nickname(), "Jen").build(),
                        success -> {TAG},
                        failure ->{TAG});
- After user has been created, go on to AWS console and check cognito
```

### Activity

## Verify email works

- Manage User Pools
- Will say unverified. Need to verify email
- Take verification code that has been sent to your email

```java
Amplify.Auth.confirmSignUp("jennerdulce@hotmail.com",
                        ######,
                        success -> {TAG},
                        failure ->{TAG});
```

- Will change account status to confirmed

## Login application with new account

```java
Amplify.Auth.signin("jennerdulce@hotmail.com",
                      "password",
                        success -> {TAG},
                        failure ->{TAG});
```

## Signout

```java
Amplify.Auth.signOut(()-> {},
                failure ->{TAG});                  
```

## Get currentUser

```java
AuthUser currentUser = Amplify.Auth.getCurrentUser()
if(currentUser != null){
String username = currentUser.getUsername();
Amplify.Auth.fetchUserAttributes(username,
            success-> username + ": " + success.toString()
            failure -> failure.toString())
}

String nickname = "";
for(AuthUserAttribute userAttribute: success{
  if(userAttribute.getKey().getKeyString().equals("nickname")){
    nickname = userAttribute.getValue()
  }
}

```

## General

- IAM users are not the same as cognito users
- You do not have to keep loggin into your app when you close and reopen the app. This is the magic of cognito

## Reflect

- What went well, that I might forget if I don’t write down?
  - Dont forget to add plugin to MainApp
  - Dont forget to add dependency to build.gradle
  - This lab was great. I digested the information fairly well.
  - Cognito is able to retrieve who is logged in

```java
AuthUser currentUser = Amplify.Auth.getCurrentUser();
        if(currentUser == null){
            Intent loginActivityIntent = new Intent(MainActivity.this, LoginActivity.class);
            startActivity(loginActivityIntent);
}
```

- What did I learn today?
  - I learned how to implement auth using Cognito

- What should I do differently next time?
  - Nothing new, I feel like I picked this up fairly quickly. I need to just study up on it so that I am more comfortable

- What still puzzles me, or what do I need to learn more about?
  - Nothing really puzzles me at the moment. I am starting to really like Java seeing that it has things like this that it has to offer. Really amazing.

- Is the assignment complete? If not, where exactly did you leave off, and what work remains?
  - This assignment is complete