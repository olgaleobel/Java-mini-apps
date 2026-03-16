[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)

# UK Unis app

## Example Code

### 1. Activity setup (initialisation and UI binding)

The activity initialises the main UI components including the horizontal scroll view, image gallery and text fields.  
Arrays are used to store references to images and related text content, allowing the interface to update dynamically depending on the current position.

```java
horizontalScrollView = findViewById(R.id.horizontal_scroll_view);
topTextView = findViewById(R.id.topTextView);
textView = findViewById(R.id.textView);

imageViews[0] = findViewById(R.id.image1);
imageViews[1] = findViewById(R.id.image2);
imageViews[2] = findViewById(R.id.image3);
imageViews[3] = findViewById(R.id.image4);

thumbnailViews[0] = findViewById(R.id.thumbnail1);
thumbnailViews[1] = findViewById(R.id.thumbnail2);
thumbnailViews[2] = findViewById(R.id.thumbnail3);
thumbnailViews[3] = findViewById(R.id.thumbnail4);
```

---

### 2. Dynamic text updates based on the selected image

Text content for each university is stored in arrays and displayed depending on the currently selected image.  
This approach separates UI content from interaction logic.

```java
textsTop[0] = getString(R.string.text_11);
textsTop[1] = getString(R.string.text_22);
textsTop[2] = getString(R.string.text_33);
textsTop[3] = getString(R.string.text_44);

textsBottom[0] = getString(R.string.text_1);
textsBottom[1] = getString(R.string.text_2);
textsBottom[2] = getString(R.string.text_3);
textsBottom[3] = getString(R.string.text_4);

updateText(currentPosition);
```

---

### 3. Detecting scroll position and snapping to the nearest image

The application listens for horizontal scroll events and determines which image is currently in view.  
After scrolling stops, the view smoothly aligns to the nearest image and updates the corresponding text.

```java
horizontalScrollView.setOnScrollChangeListener(new HorizontalScrollView.OnScrollChangeListener() {

    private static final int SCROLL_DELAY_MS = 150;
    private Runnable scrollRunnable;

    @Override
    public void onScrollChange(View v, int scrollX, int scrollY, int oldScrollX, int oldScrollY) {

        float density = getResources().getDisplayMetrics().density;
        int imageWidth = (int) (450 * density + 16 * density);

        if (scrollRunnable != null) {
            horizontalScrollView.removeCallbacks(scrollRunnable);
        }

        scrollRunnable = new Runnable() {
            @Override
            public void run() {
                int position = Math.round((float) scrollX / imageWidth);
                int targetScrollX = position * imageWidth;

                horizontalScrollView.smoothScrollTo(targetScrollX, 0);
                updateText(position);
            }
        };

        horizontalScrollView.postDelayed(scrollRunnable, SCROLL_DELAY_MS);
    }
});
```

---

### 4. Navigation buttons for browsing images

Previous and Next buttons allow the user to move through the image gallery.  
The application updates both the scroll position and the corresponding text content.

```java
previousButton.setOnClickListener(v -> {
    if (currentPosition > 0) {
        currentPosition--;
        updateText(currentPosition);
        scrollToCurrentPosition();
    }
});

nextButton.setOnClickListener(v -> {
    if (currentPosition < textsTop.length - 1) {
        currentPosition++;
        updateText(currentPosition);
        scrollToCurrentPosition();
    }
});
```

---

### 5. Thumbnail navigation

Clickable thumbnails provide an additional way to navigate directly to a specific university image.

```java
for (int i = 0; i < thumbnailViews.length; i++) {
    final int index = i;
    thumbnailViews[i].setOnClickListener(v -> {
        currentPosition = index;
        updateText(currentPosition);
        scrollToCurrentPosition();
    });
}
```

---

### 6. Horizontal image gallery layout

A `HorizontalScrollView` is used to create a scrollable gallery of university images.  
Each image represents a university and triggers a corresponding text update.

```xml
<HorizontalScrollView
    android:id="@+id/horizontal_scroll_view"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <ImageView
            android:id="@+id/image1"
            android:layout_width="450dp"
            android:layout_height="300dp"
            android:layout_marginRight="16dp"
            android:src="@drawable/image1oxford" />

        <ImageView
            android:id="@+id/image2"
            android:layout_width="450dp"
            android:layout_height="300dp"
            android:layout_marginRight="16dp"
            android:src="@drawable/image2cambridge" />

    </LinearLayout>
</HorizontalScrollView>
```

---

[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)
