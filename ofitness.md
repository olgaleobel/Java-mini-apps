[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)

# O'Fitness app

## Example Code

### 1. Dynamic Spinner Content Based on Selected Category

The application dynamically updates the spinner options depending on the selected exercise category.
This allows the interface to present different exercise lists without creating separate UI components.

```java
radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup group, int checkedId) {
        if (checkedId == R.id.radioCardio) {
            setSpinnerOptions(cardio);
        } else if (checkedId == R.id.radioStrength) {
            setSpinnerOptions(strength);
        } else if (checkedId == R.id.radioCalisthenics) {
            setSpinnerOptions(calisthenics);
        }
    }
});

```

### 2. Reusable Method for Spinner Configuration

A reusable method is used to configure the spinner adapter.
This approach avoids repeating adapter setup logic and keeps the activity code cleaner.

```java
private void setSpinnerOptions(String[] options) {
    spinnerAdapter = new ArrayAdapter<>(this, android.R.layout.simple_spinner_item, options);
    spinnerAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
    spinner.setAdapter(spinnerAdapter);
    spinner.setSelection(0); // "No selection" on default
}

```

### 3. Handling User Selection from Spinner

The spinner listener stores the currently selected exercise, which is later used to display the corresponding description.

```java
spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
    @Override
    public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
        selectedExercise = spinner.getSelectedItem().toString();
    }

    @Override
    public void onNothingSelected(AdapterView<?> parent) {
        selectedExercise = null;
    }
});
```

### 4.Mapping Exercise Selection to Description Text

A switch structure maps each exercise to its corresponding description stored in the application's string resources.
This keeps text content separated from logic and improves maintainability.

```java
private String getResultText(String selectedExercise) {
    switch (selectedExercise) {
        case "Running":
            return getString(R.string.running_description);
        case "Cycling":
            return getString(R.string.cycling_description);
        case "Swimming":
            return getString(R.string.swimming_description);
        case "Benchpress":
            return getString(R.string.benchpress_description);
        case "Deadlift":
            return getString(R.string.deadlift_description);
        case "Squat":
            return getString(R.string.squat_description);
        case "Pullups":
            return getString(R.string.pullups_description);
        case "Pushups":
            return getString(R.string.pushups_description);
        case "Dips":
            return getString(R.string.dips_description);
        default:
            return getString(R.string.please_select);
    }
}
```

### 5. UI Structure (Layout Example)

Radio buttons allow the user to select a category of exercises.
The selected category determines which exercise options appear in the spinner.

```java
<RadioGroup
    android:id="@+id/radioGroup"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <RadioButton
        android:id="@+id/radioCardio"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Cardio" />

    <RadioButton
        android:id="@+id/radioStrength"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Strength" />

    <RadioButton
        android:id="@+id/radioCalisthenics"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Calisthenics" />

</RadioGroup>

```
[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)
