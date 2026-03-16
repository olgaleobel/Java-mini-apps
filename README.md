[⬅️ Back to main page](https://github.com/olgaleobel/)

# Java-mini-apps

A collection of seven small Android applications developed in **Java using Android Studio**.  
These projects represent my first hands-on experience with **Java programming and Android mobile development**.

Each app focuses on practising core mobile development concepts, including **UI layout design, user interaction, form validation, dynamic data handling, and list-based interfaces**. 
Together, they demonstrate progressive learning of Android components such as `RecyclerView`, `SearchView`, `Spinner`, and multi-`Activity` navigation.

All applications were designed, implemented, and tested to meet the assignment requirements, with several features extended beyond the original scope.


### UK Flowers (App 1)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/e9939f0323216dbbc94625372720ffc79421a32b/images/ukflowers.png" width="950">

</td>
<td>

A simple single-screen application developed in Java as my first Android Studio project. 

The app demonstrates basic UI layout and interaction using `ImageView`, `TextView`, and `Button`.  Clicking a flower image (representing a UK country) displays information in the centre of the screen, changes UI colours, and reveals a **Clear** button that resets the interface.

Additional functionality includes sound feedback associated with each selected flower.

</td>
</tr>
</table>
</table>

### OFitness (App 2)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/58718ada572dfb9e022a238bded6452725e6724e/images/ofitness.png" width="170">

</td>
<td>
  
A single-screen application developed to practise interactive UI components.  

The app uses `RadioButton` / `RadioGroup` to select a fitness category and dynamically updates a `Spinner` with exercises related to the chosen activity.  
After pressing **Submit**, the application displays the advantages and disadvantages of the selected exercise.  
Includes basic input validation (warning message when no option is selected) and a **Clear** button that resets the UI to its initial state.


</td>
</tr>
</table>
</table>

### Dish Filler (App 3)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/5800db75e7c58889eee6768eb24a8e019d9f6aaa/images/dishfiller.png" width="150">

</td>
<td>
  
A single-screen application developed to practise working with `CheckBox` components, logical conditions, and basic arithmetic operations.  

Users can build a dish by selecting ingredients via checkboxes, while the app dynamically updates the total price and calorie count.  
A visual plate preview updates in real time to reflect the selected ingredients using layered images.  
Pressing **Order** displays a confirmation `Toast` message with the final price and calories, while the **Clear** button resets the interface.


</td>
</tr>
</table>
</table>

### UK Unis (App 4)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/d4f76326ab00aaed49725b225bc10af4bd92c8bb/images/ukunis.png" width="250">

</td>
<td>

A single-screen application developed to practise horizontal scrolling and dynamic UI interactions.  

The app presents a catalogue of UK universities using a scrollable image gallery. Users can navigate through universities by swiping images, using **Next** / **Previous** buttons, or selecting thumbnails from a bottom gallery.  
The text content updates dynamically based on the currently displayed university image.  
Additional logic ensures that gallery images snap into correct alignment when scrolled, preventing partial images from appearing on the screen.

</td>
</tr>
</table>
</table>

### Login App (App 5)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/72bf8f67ca482f389a9afd8aa289e80bcc2182b0/images/login.png" width="200">

</td>
<td>

A multi-screen application developed to practise form handling and input validation.  
The app includes user registration and login functionality, with separate `Activity` screens for login, registration, and a welcome page.  
Validation checks ensure that required fields are completed and that login credentials match registered data, with error messages and highlighted fields indicating issues.  
Successful registration and certain actions are confirmed using `Toast` messages, while the welcome screen displays user information derived from the registration data.

</td>
</tr>
</table>
</table>

### OLPhoneContact (App 6)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/6cfc1a71839c98cbabbcba497871f002a892a031/images/contacts.png" width="150">

</td>
<td>
  
An application developed to practise working with `RecyclerView` and dynamic search functionality.  
The app displays a scrollable list of contacts and uses `SearchView` to provide instant filtering as the user types.  
Selecting a contact opens options to initiate a phone call or send a message to the selected number.  
The project demonstrates efficient list handling with `RecyclerView`, dynamic UI updates, and basic interaction with device communication features.


</td>
</tr>
</table>
</table>

### Blue Rent (App 7)

<table>
<tr>
<td>

<img src="https://raw.githubusercontent.com/olgaleobel/Java-mini-apps/72bf8f67ca482f389a9afd8aa289e80bcc2182b0/images/bluerent.png" width="120">

</td>
<td>

An application developed to practise building a reservation/basket system with dynamic data.  
The app displays a list of transport options using `RecyclerView`, with images and information loaded from an external JSON data source (with placeholders for missing images).  
Users can select a vehicle, choose a rental date range via `DatePicker`, and add it to the current order.  
Selected items can be reviewed, modified, or confirmed through a checkout screen, with the booking process finalised via a confirmation `Toast` message.

</td>
</tr>
</table>
</table>

[⬅️ Back to main page](https://github.com/olgaleobel/)


ukflowers.png
│   ├─ ofitness.png
│   ├─ dishfiller.png
│   ├─ ukunis.png
│   ├─ login.png
│   ├─ contacts.png
│   └─ bluerent.png
