# HappyPlaces
INTRODUCTION

The Happy Places Application is an intuitive and user-friendly mobile application designed to help users capture, record, and cherish their happiest moments and locations. With the increasing emphasis on mental well-being and the value of positive experiences, this application aims to provide users with a platform to create a digital repository of places that hold sentimental or joyful significance.
The application allows users to seamlessly add details such as the title, description, date, and location of their happy places. They can also upload or capture an image to visually represent each memory. By integrating features like Google Places API, location tracking, and a built-in database, the app ensures that users can both manually input details or automatically fetch their current location for a more personalized experience.
Key features of the app include:
    • Image Integration: Users can select images from their gallery or capture photos using their device camera.
    • Location Services: With support for real-time GPS tracking, users can fetch and store the geographical coordinates and addresses of their happy places.
    • Google Places Autocomplete: Simplifies the process of selecting and searching for locations.
    • Internal Storage: Ensures images and data are securely stored within the device for offline access.
    • Database Management: Efficiently stores, updates, and retrieves user inputs using SQLite for long-term persistence.




Page 1: Favorite Locations Overview
This page serves as the central hub for viewing and managing all saved favorite places. It features a well-organized RecyclerView that displays a list of happy places added by the user, including their names and images for quick identification.
Features:
    1. List View of Happy Places: All saved locations are displayed in a scrollable RecyclerView. Each item in the list shows the title and an image of the location.
    2. Edit and Delete Options:
        ◦ Swipe Right: Users can edit the details of a selected happy place, including the name, description, image, date, or location.
        ◦ Swipe Left: Users can delete a happy place from the list.
    3. Persistent Storage: All saved places are stored locally in SQLite, ensuring data is available offline.



Page 2: Add a Happy Place
This page allows users to input the details of a new happy place. The form ensures that all required information is captured to create a meaningful entry.
Features:
    1. Form Inputs:
        ◦ Name: The user must enter the title of the place.
        ◦ Description: A brief description about why the place is special.
        ◦ Date: The date of the visit, selected using a date picker.
        ◦ Location: Choose the location using the Google Places API or select the current GPS-based location.
        ◦ Image: Upload an image of the place either by capturing it with the device camera or selecting it from the gallery.
    2. Location Picker:
        ◦ Search Location: Use the Google Places API to search and select a specific location.
        ◦ Current Location: Use GPS to automatically fetch the current location coordinates.
    3. Validation: The app ensures all fields are filled before saving.
    4. Save Button: Saves the data into SQLite and updates the main list in RecyclerView.

Page 3: Happy Place Details
This page provides an in-depth view of a selected happy place, offering more context and visualization.
Features:
    1. Details View: Displays all the details of the selected happy place, including:
        ◦ Name
        ◦ Description
        ◦ Date
        ◦ Full Address
        ◦ Image
    2. Google Maps Integration: The location is visualized on a map using the Google Maps API.
        ◦ Map Marker: Marks the exact location of the happy place on the map.
        ◦ Navigation Options: Users can open the location in Google Maps for navigation.
    3. Edit Option: A quick link to return to the Add/Update Happy Place page for editing details.
    4. Interactive Experience: Smooth animations and transitions enhance the user's experience when exploring location details.
       
Page 4: RecyclerView with Map Integration
The fourth page focuses on combining the RecyclerView and Google Maps Activity to provide an enhanced user experience. It lists the saved places and allows users to view their locations on a map.
Features:
    1. RecyclerView Integration: Displays all happy places with a thumbnail image, name, and a short description.
    2. Map Integration:
        ◦ Users can click on a location to view it in Google Maps Activity.
        ◦ This activity uses the Google Maps API to place a marker on the selected location.
        ◦ The map includes zoom controls and navigation options for a better user experience.
    3. Edit and Delete Functionality:
        ◦ Swipe to Edit: Allows users to quickly update a location's details.
        ◦ Swipe to Delete: Deletes the selected happy place from the SQLite database.
HappyPlacesAdapter
The HappyPlacesAdapter is responsible for binding data to the RecyclerView. It handles how each item in the list is displayed and interacted with.
Key Responsibilities:
    1. View Binding: Connects data (e.g., title, description, image) from the SQLite database to individual RecyclerView items.
    2. Item Click Handling: Detects user clicks on a list item and launches the detailed view of the happy place.
    3. Swipe Gesture Support: Integrates with swipe actions for editing and deleting list items.







DatabaseHandler
The DatabaseHandler is a custom class that manages all interactions with the SQLite database. It serves as the bridge between the application and the database.
Key Functions:
    1. Create Database: Sets up tables for storing happy place data.
    2. CRUD Operations:
        ◦ Create: Adds a new happy place to the database.
        ◦ Read: Fetches all happy places for displaying in the RecyclerView.
        ◦ Update: Updates the details of an existing happy place.
        ◦ Delete: Removes a happy place from the database.






HappyPlaceModel
This is a data class that defines the structure of a happy place entry. It simplifies data handling by encapsulating all properties in one object.
Attributes:
    • ID: Unique identifier for each happy place.
    • Title: Name of the happy place.
    • Image: URI of the image associated with the place.
    • Description: Details about why the place is special.
    • Date: Date of the visit.
    • Location: Address of the place.
    • Latitude and Longitude: Coordinates for map integration.
      
GetAddressFromLatLng
This utility class fetches a human-readable address from latitude and longitude coordinates using the Geocoder API.
Key Responsibilities:
    1. Address Conversion: Converts geographic coordinates into an address string.
    2. Listener for Asynchronous Fetch:
        ◦ onAddressFound: Called when the address is successfully fetched.
        ◦ onError: Called if an error occurs during the fetch.
    3. Integration with Location API: Helps in real-time location updates when the user selects "Use Current Location."





Swipe to Edit and Delete Functionality
Swipe to Delete
    1. Implementation: Uses the ItemTouchHelper.Callback class to detect swipe gestures.
    2. Behavior:
        ◦ Swiping left deletes the corresponding item from the RecyclerView.
        ◦ The item is also removed from the SQLite database.
    3. Undo Snackbar: Optional feature to let users undo accidental deletions.
Swipe to Edit
    1. Implementation: Similar to swipe-to-delete but configured for right swipes.
    2. Behavior:
        ◦ Swiping right opens the Add Happy Place Activity with pre-filled data for the selected place.
        ◦ Users can modify and save updates, which are reflected in the RecyclerView.
