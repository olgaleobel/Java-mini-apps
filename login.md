### Welcome Screen – Displaying User Details

Retrieves user information from a local database and displays it on a welcome screen after successful login.

```java
// Getting username from previous activity
username = getIntent().getStringExtra("username");

// Retrieving user details from database
User user = dbHelper.getUserDetails(username);

if (user != null) {
    fullNameText.setText(user.getFullName());
    genderText.setText("Sex: " + user.getGender());
    ageText.setText("Age: " + user.getAge());
} else {
    fullNameText.setText("User data not found.");
    genderText.setVisibility(View.GONE);
    ageText.setVisibility(View.GONE);
}
```

### Activity Navigation

Implements navigation back to the main login screen using an explicit intent.

```java
Button backButton = findViewById(R.id.button_back);
backButton.setOnClickListener(v -> {
    Intent intent = new Intent(WelcomeActivity.this, MainActivity.class);
    startActivity(intent);
    finish();
});
```

### Layout Structure

Defines a vertically structured layout displaying the user’s details and a navigation button.

```xml
<TextView
    android:id="@+id/fullNameText"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:gravity="center"
    android:textSize="24sp"
    android:textStyle="bold" />

<Button
    android:id="@+id/button_back"
    android:layout_width="158dp"
    android:layout_height="60dp"
    android:text="Back" />
```
