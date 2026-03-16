[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)

## Blue Rent app

### 1. Checkout Activity – displaying reserved orders

This activity shows the list of transport bookings passed from the main selection screen.
It handles "Back" to return and "Finish" to exit the app with a confirmation toast.

```java

orderInfoList = getIntent().getStringArrayListExtra("orderInfoList");

TextView orderDetailsTextView = findViewById(R.id.order_details_text);
if (orderInfoList != null && !orderInfoList.isEmpty()) {
    StringBuilder orders = new StringBuilder();
    for (String order : orderInfoList) {
        orders.append(order).append("\n\n");
    }
    orderDetailsTextView.setText(orders.toString().trim());
} else {
    orderDetailsTextView.setText("No orders yet.");
}

Button finishButton = findViewById(R.id.finish_button);
finishButton.setOnClickListener(v -> {
    Toast.makeText(CheckOutActivity.this, "ENJOY!", Toast.LENGTH_LONG).show();
    finishAffinity(); // Close all activities
});

```

### 2. Fetching JSON data asynchronously

GetJSONData loads transport info from a JSON API and converts it to Transport objects.
It uses AsyncTask to perform network operations off the main thread.

```Java

URL url = new URL("https://api.jsonserve.com/_9Gh51");
HttpURLConnection conn = (HttpURLConnection) url.openConnection();
BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(conn.getInputStream()));

JSONArray jsonArray = new JSONArray(data);
for (int i = 0; i < jsonArray.length(); i++) {
    JSONObject jsonObject = jsonArray.getJSONObject(i);
    Transport transport = new Transport(
        jsonObject.getString("transportCategory"),
        jsonObject.getString("transportName"),
        jsonObject.getString("transportCapacity"),
        jsonObject.optString("transportImage")
    );
    myTransport.add(transport);
}

```

### 3. RecyclerView ViewHolder – binding transport data

ItemHolder stores references to views in a transport item and provides methods to set their content.
Picasso is used to load images from URLs efficiently.

```Java

public void setTransportImageView(String imageUrl) {
    Picasso.get().load(imageUrl).into(transportImage);
}

public void setTransportName(String name) {
    transportName.setText(name);
}

public void setTransportCapacity(String capacity) {
    transportCapacity.setText(capacity);
}

```

### 4. RecyclerView Adapter – handling selection and booking

The adapter manages the list of transport items.
It tracks which items are booked and allows users to select a date range using MaterialDatePicker.

```Java

if (!isOrdered[position]) {
    MaterialDatePicker<Pair<Long, Long>> datePicker = MaterialDatePicker.Builder.dateRangePicker()
        .setTitleText("Select Date Range")
        .build();

    datePicker.addOnPositiveButtonClickListener(selection -> {
        String startDate = new SimpleDateFormat("yyyy-MM-dd").format(new Date(selection.first));
        String endDate = new SimpleDateFormat("yyyy-MM-dd").format(new Date(selection.second));
        orderInfoList.add("Transport: " + currentTransport.getTransport_name() +
                          "\nCapacity: " + currentTransport.getTransport_capacity() +
                          "\nPeriod: " + startDate + " to " + endDate);

        isOrdered[position] = true;
        updateButtonAppearance(holder, position);

        showOrderDialog();
    });
}

```

### 5. Updating Order button appearance

The button text and color change depending on whether the item is selected.
This gives immediate visual feedback to the user.

```Java

private void updateButtonAppearance(@NonNull ItemHolder holder, int position) {
    if (isOrdered[position]) {
        holder.getOrderButton().setText("Cancel Selection");
        holder.getOrderButton().setBackgroundColor(myContext.getResources().getColor(R.color.orange));
    } else {
        holder.getOrderButton().setText("Book");
        holder.getOrderButton().setBackgroundColor(myContext.getResources().getColor(R.color.defaultcolour));
    }
}

```

### 6. Transport data model

A simple Transport class stores type, name, capacity, and image URL of each transport.
It provides getters for use in adapter and view holder.

```Java

public class Transport {
    private String transport_type;
    private String transport_name;
    private String transport_capacity;
    private String transport_image;

    public Transport(String transport_type, String transport_name, String transport_capacity, String transport_image) {
        this.transport_type = transport_type;
        this.transport_name = transport_name;
        this.transport_capacity = transport_capacity;
        this.transport_image = transport_image;
    }

    public String getTransport_name() { return transport_name; }
    public String getTransport_capacity() { return transport_capacity; }
    public String getTransport_type() { return transport_type; }
    public String getTransport_image() { return transport_image; }
}

```

### 7. Layout – RecyclerView item for each transport

Each item shows an image, details, and a booking button.
A hidden TextView stores order info and becomes visible when needed.

```Java

<ImageView
    android:id="@+id/transportImageView"
    android:layout_width="220dp"
    android:layout_height="150dp"
    android:src="@drawable/placeholder" />

<TextView
    android:id="@+id/transportNameTextView"
    android:textSize="22sp"
    android:textStyle="bold"/>

<Button
    android:id="@+id/orderButton"
    android:text="Book" />

<TextView
    android:id="@+id/orderInfoTextView"
    android:visibility="gone" />
    
   ```

[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)    

