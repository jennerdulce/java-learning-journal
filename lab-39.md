# Location

## General

- Location is private information
  - Need to request permission to allow this data to be passed
  - In andoriod manifest <uses-permission andriod:name

- Request Permission
  - `requestPermissions(new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, FINE_LOCATION_PERMISSION_CODE);`
- Dependency
  - `implementation 'com.google.android.gms:play-services-location:18.0.0'`

## Boiler Plate

```java
Geocoder geocoder;
FusedLocationProviderClient fusedLocationProviderClient;
String latitude;
String longitude;
String city;

 requestPermissions(new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, FINE_LOCATION_PERMISSION_CODE);
        fusedLocationProviderClient = LocationServices.getFusedLocationProviderClient(getApplicationContext());
        geocoder = new Geocoder(getApplicationContext(), Locale.getDefault());

        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            // TODO: Consider calling
            //    ActivityCompat#requestPermissions
            // here to request the missing permissions, and then overriding
            //   public void onRequestPermissionsResult(int requestCode, String[] permissions,
            //                                          int[] grantResults)
            // to handle the case where the user grants the permission. See the documentation
            // for ActivityCompat#requestPermissions for more details.
            return;
        }

        fusedLocationProviderClient.getLastLocation().addOnSuccessListener(location -> {
            latitude = Double.toString(location.getLatitude());
            longitude = Double.toString(location.getLongitude());
            try {
                List<Address> addressGuesses = geocoder.getFromLocation(location.getLatitude(), location.getLongitude(), 1);
                Address address = addressGuesses.get(0);
                city = address.getLocality();
            } catch (IOException e) {
                e.printStackTrace();
            }
        });

```

## USEFUL REFERENCES

- https://developers.google.com/maps/documentation/android-sdk/config
- https://developers.google.com/maps/documentation/android-sdk/start (the 
- https://developers.google.com/maps/documentation/android-sdk/map
- https://github.com/googlemaps/android-samples/blob/main/ApiDemos/java/app/src/gms/java/com/example/mapdemo/RawMapViewDemoActivity.java
- https://console.cloud.google.com/
- https://stackoverflow.com/questions/19043577/android-mapview-display-empty

## Reflect

- What went well, that I might forget if I don’t write down?
  - Cannot store doubles in GraphQL
    - Store lat and long as a string and revert back to double when needed
  - Addresses are returned as a list
    - Picking index at 0 is the most accurate

- What did I learn today?
  - Today I learned how to request permissions to extract location data from users phone
  - This permission allows us to then work with FusedLocationProviderClient
  - Boilerplate works with geocoder to get the data

- What should I do differently next time?
  - Nothing, this lab went well

- What still puzzles me, or what do I need to learn more about?
  - I'm just realizing that there is a lot of boilerplate with Java and that I just have to accept it. Also that along with the fast paced day course make it hard to absorb the infomation throughly

- Is the assignment complete? If not, where exactly did you leave off, and what work remains?
  - This assignment is completed
