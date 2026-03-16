[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)

# Dish Filler app

## Example Code

### 1. Activity setup (initialisation and UI binding)

The activity initialises the main UI components including checkboxes, overlay images and result fields.  
Arrays are used to store references to related UI elements, which simplifies handling multiple ingredients in a compact way.

```java
baseImage = findViewById(R.id.baseImage);

overlayImages = new ImageView[]{
        findViewById(R.id.overlayImageFish1),
        findViewById(R.id.overlayImageRice2),
        findViewById(R.id.overlayImageTomatoes3),
        findViewById(R.id.overlayImageSteak4),
        findViewById(R.id.overlayImageEgg5),
        findViewById(R.id.overlayImageSalad6)
};

checkboxes = new CheckBox[]{
        findViewById(R.id.chkboxFish),
        findViewById(R.id.chkboxRice),
        findViewById(R.id.chkboxTomatoes),
        findViewById(R.id.chkboxSteak),
        findViewById(R.id.chkboxEgg),
        findViewById(R.id.chkboxSalad)
};

sumPriceText = findViewById(R.id.sumPrice);
sumCaloriesText = findViewById(R.id.sumCalories);
```

---

### 2. Handling checkbox interactions and updating the dish

Each checkbox controls the visibility of a corresponding ingredient image layered on the plate.  
A loop is used to attach listeners to all checkboxes, reducing repetitive code.

```java
for (int i = 0; i < checkboxes.length; i++) {
    final int index = i;
    checkboxes[i].setOnCheckedChangeListener((buttonView, isChecked) -> {
        overlayImages[index].setVisibility(isChecked ? View.VISIBLE : View.GONE);

        // Updating totals when selection changes
        updateSums();
    });
}
```

---

### 3. Calculating total price and calories

The application calculates the total price and calorie count based on the selected ingredients.  
Arrays are used to store numeric values for each option, allowing the sums to be computed dynamically.

```java
private void updateSums() {
    sumPrice = 0;
    sumCalories = 0;

    for (int i = 0; i < checkboxes.length; i++) {
        if (checkboxes[i].isChecked()) {
            sumPrice += valuesSumPrice[i];
            sumCalories += valuesSumCalories[i];
        }
    }

    sumPriceText.setText(String.valueOf(sumPrice));
    sumCaloriesText.setText(String.valueOf(sumCalories));
}
```

---

### 4. Submit and validation logic

When the user places the order, the application checks whether at least one ingredient has been selected.  
If nothing is selected, a message prompts the user to choose an item. Otherwise, a confirmation message is displayed.

```java
submitButton.setOnClickListener(v -> {
    int checkedCount = getCheckedCount();

    if (checkedCount == 0) {
        Toast.makeText(MainActivity.this,
                "Please select at least one item",
                Toast.LENGTH_LONG).show();

        sumPriceText.setText("0");
        sumCaloriesText.setText("0");

    } else {
        String message = "Your order totaling £" + sumPrice +
                " (" + sumCalories + " kcal) has been accepted.";

        Toast.makeText(MainActivity.this,
                message,
                Toast.LENGTH_LONG).show();
    }
});
```

---

### 5. Layered UI layout for visual dish composition

A `FrameLayout` is used to stack ingredient images on top of the base plate image.  
Each ingredient image is initially hidden and becomes visible when the corresponding checkbox is selected.

```xml
<FrameLayout
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center">

    <ImageView
        android:id="@+id/baseImage"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:src="@drawable/imageplate0f" />

    <ImageView
        android:id="@+id/overlayImageFish1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/imagefish1f"
        android:visibility="gone" />

    <ImageView
        android:id="@+id/overlayImageRice2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/imagerice2f"
        android:visibility="gone" />

</FrameLayout>
```

---

[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)
