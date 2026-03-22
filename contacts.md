[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)

# Phone Contacts app

## Example Code

### 1. RecyclerView Adapter with ViewHolder pattern

The adapter manages the contact list display and implements efficient view recycling. It maintains two data lists — `contactList` for display and `contactListFull` as an immutable backup for filtering operations. Interface-based click delegation ensures loose coupling between adapter and activity.

```java
package com.example.olphonecontacts;

import android.text.TextUtils;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.ArrayList;
import java.util.List;

public class ContactAdapter extends RecyclerView.Adapter<ContactAdapter.ContactViewHolder> {

    private final List<Contact> contactList;
    private final List<Contact> contactListFull;
    private final OnContactClickListener listener;

    public ContactAdapter(List<Contact> contactList, OnContactClickListener listener) {
        this.contactList = contactList;
        this.contactListFull = new ArrayList<>(contactList);
        this.listener = listener;
    }

    @NonNull
    @Override
    public ContactViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.contact_item, parent, false);
        return new ContactViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ContactViewHolder holder, int position) {
        Contact contact = contactList.get(position);

        holder.name.setText(contact.getName());
        holder.phone.setText(contact.getPhone());
        holder.email.setText(contact.getEmail());
        holder.image.setImageResource(
                contact.getImageResId() > 0 ? contact.getImageResId() : R.drawable.placeholder);

        holder.itemView.setOnClickListener(v -> listener.onContactClick(contact.getPhone()));
    }

    @Override
    public int getItemCount() {
        return contactList.size();
    }

    public interface OnContactClickListener {
        void onContactClick(String phoneNumber);
    }
}
```

---

### 2. Real-time search filtering

Custom filter method enables instant contact search by name with case-insensitive matching. Falls back to full list when query is cleared, and notifies the adapter to refresh the view.

```java
public void filter(String query) {
    contactList.clear();
    if (TextUtils.isEmpty(query)) {
        contactList.addAll(contactListFull);
    } else {
        for (Contact contact : contactListFull) {
            if (contact.getName() != null && 
                contact.getName().toLowerCase().contains(query.toLowerCase())) {
                contactList.add(contact);
            }
        }
    }
    notifyDataSetChanged();
}
```

---

### 3. ContactViewHolder – binding contact data

ViewHolder caches references to UI elements to avoid expensive findViewById calls during scroll. The constructor initialises all view references for the contact item layout.

```java
static class ContactViewHolder extends RecyclerView.ViewHolder {
    TextView name, phone, email;
    ImageView image;

    public ContactViewHolder(@NonNull View itemView) {
        super(itemView);
        name = itemView.findViewById(R.id.contactName);
        phone = itemView.findViewById(R.id.contactPhone);
        email = itemView.findViewById(R.id.contactEmail);
        image = itemView.findViewById(R.id.contactImage);
    }
}
```

---

### 4. Contact data model

Simple POJO storing contact information with getter-only access. Encapsulates name, phone, email, and avatar resource ID. Immutability prevents accidental state corruption during list operations.

```java
package com.example.olphonecontacts;

public class Contact {
    private String name;
    private String phone;
    private String email;
    private int imageResId;

    public Contact(String name, String phone, String email, int imageResId) {
        this.name = name;
        this.phone = phone;
        this.email = email;
        this.imageResId = imageResId;
    }

    public String getName() {
        return name;
    }

    public String getPhone() {
        return phone;
    }

    public String getEmail() {
        return email;
    }

    public int getImageResId() {
        return imageResId;
    }
}
```

---

### 5. RecyclerView item layout

Each list item displays a contact image, name, phone number, and email in a horizontal row. Clicking the item triggers the phone dialer via the callback interface implemented in the activity.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="12dp">

    <ImageView
        android:id="@+id/contactImage"
        android:layout_width="60dp"
        android:layout_height="60dp"
        android:src="@drawable/placeholder"
        android:scaleType="centerCrop" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:layout_marginStart="12dp">

        <TextView
            android:id="@+id/contactName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="18sp"
            android:textStyle="bold" />

        <TextView
            android:id="@+id/contactPhone"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="14sp" />

        <TextView
            android:id="@+id/contactEmail"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="14sp" />

    </LinearLayout>
</LinearLayout>
```

---

[⬅️ Back to Java mini apps](https://github.com/olgaleobel/Java-mini-apps/)
