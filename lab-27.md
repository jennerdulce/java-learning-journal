
# Data in TaskMaster

- sharedPreferences = global
- Intent is wasteful
- ROOM databases

## Storing Data / 'State

```java
public class UserSettingsActivity extends AppCompatActivity {
    public final static String USERNAME_KEY = "username";

    // In order to used saved "state"
    public static SharedPreferences sharedPreferences;
    public static SharedPreferences.Editor sharedPreferencesEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_user_settings);

        sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
        sharedPreferencesEditor = sharedPreferences.edit();

        // Accesses stored values and sets the value for the PlainText
        EditText usernameInputText = findViewById(R.id.usernameInputPlainText);
        String username = sharedPreferences.getString(USERNAME_KEY, "");
        usernameInputText.setText(username);

        Button userSettingsSaveButton = findViewById(R.id.userSettingsSaveButton);
        userSettingsSaveButton.setOnClickListener(view -> {
            String changeUsername = usernameInputText.getText().toString();
            sharedPreferencesEditor.putString(USERNAME_KEY, changeUsername);
            sharedPreferencesEditor.apply();
        });
    }
}
```

- Import `SharedPreferences` and `SharedPreferences.Editor`
  - These allow you to store data
  - Follow the steps, they are kind of boiler plate
  - `.putString()`
  - And `.apply()`

## Using SharedPreferences

```java
protected static SharedPreferences sharedPreferences;
protected static Resources res;

@Override
  protected void onResume(){
      super.onResume();
      String username = sharedPreferences.getString(USERNAME_KEY, "");

      if(!username.equals("")){
          // This line finds the saved String ID from the strings.xml file and instantiate at the '%1$s' at the second parameter
          ((TextView) findViewById(R.id.welcomeUsernameMessageTextView)).setText(res.getString(R.string.WelcomeUsername, username));
      }
  }
```

- Import Preferences and resources
- sharedPreferences allows you to access where data is stored
- Import USERNAME_KEY
- `res.getString(R.string.WelcomeUsername, username)`
  - This allows helps prevent hard coding data
  - Uses the `WelcomeUsername` String that is stored in `values > string.xml`
  - `WelcomeUsername` looks like `Welcome %1$s!`
    - `username` is inserted at `%1$s`

## Espresso tests

- Integration tests for Andriod
- Records commands and runs the test
- Any elements that touch the sides of the screen does not work correctly
