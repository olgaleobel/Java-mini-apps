## Example Code

### 1. Activity setup (initialisation and UI binding)

The activity initialises the UI components and sets the initial state of the screen.
The informational text is displayed and the Clear button is hidden until the user interacts with the interface.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Bind UI elements
    initialText = findViewById(R.id.initialText);
    roseButton = findViewById(R.id.btnrose);
    thistleButton = findViewById(R.id.btnthistle);
    daffodilButton = findViewById(R.id.btndaffodill);
    shamrockButton = findViewById(R.id.btnshamrock);
    cleartextButton = findViewById(R.id.btnclear);

    // Initial state
    initialText.setText(R.string.initial_text);
    cleartextButton.setVisibility(View.GONE);
}
```
### 2. Reusable button behaviour (cleaner code design)

Instead of writing separate click listeners for each flower, a reusable method was created.
This reduces code repetition and allows the behaviour of all buttons to be configured through parameters (text, sound and colour).

```java
private void setButtonBehavior(ImageView button, int textResId, int soundResId, int color) {
    button.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {

            initialText.setText(textResId);

            MediaPlayer mediaPlayer = MediaPlayer.create(MainActivity.this, soundResId);
            mediaPlayer.start();

            initialText.setTextColor(color);
            cleartextButton.setBackgroundColor(color);
            cleartextButton.setVisibility(View.VISIBLE);
        }
    });
}
```

### 3. Applying behaviour to multiple UI elements

Each flower button is configured with a different text, sound and colour.
This approach keeps the activity code compact and easy to maintain.

```java
setButtonBehavior(roseButton, R.string.rose_text, R.raw.england, Color.RED);
setButtonBehavior(thistleButton, R.string.thistle_text, R.raw.scotland,
        ContextCompat.getColor(this, R.color.purple));
setButtonBehavior(daffodilButton, R.string.daffodil_text, R.raw.wales,
        ContextCompat.getColor(this, R.color.darkyellow));
setButtonBehavior(shamrockButton, R.string.shamrock_text, R.raw.nireland,
        ContextCompat.getColor(this, R.color.darkgreen));
```

### 4. Layout structure (UI composition)

The central layout contains the main informational text and a button for resetting the screen.
The layout is vertically aligned and centred to keep the interface simple and readable.

```java

<LinearLayout
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:layout_gravity="center"
    android:gravity="center">

    <TextView
        android:id="@+id/initialText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="26sp"
        android:textStyle="bold"
        android:textAlignment="center"/>

    <Button
        android:id="@+id/btnclear"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Clear"/>
</LinearLayout>

```

