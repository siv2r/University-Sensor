# University-Sensor
This project takes a list of universities from the user and uses Google Places API to get their latitude and longitude and finally visualizing them on a Goolge maps.


## INSTRUCTIONS :

Using the **Google Places API** with a Database and
Visualizing Data on Google Map

In this project, I am using the **Google Geocoding API**
to clean up some user-entered geographic locations of
university names and then placing the data on a Google
Map.

**Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each command window you open, you may need
to type the following command before running this code:**

    chcp 65001 
    
[Click here for more info](http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how)


You should install the SQLite browser to view and modify
the databases from: [here](http://sqlitebrowser.org/)

The first problem to solve is that the Google geocoding
API is rate limited to a fixed number of requests per day.
So if you have a lot of data you might need to stop and
restart the lookup process several times.  So we break
the problem into two phases.

In the first phase we take our input data in the file
(where.data) and read it one line at a time, and retrieve the
geocoded response and store it in a database (geodata.sqlite).
Before we use the geocoding API, we simply check to see if
we already have the data for that particular line of input.

You can re-start the process at any time by removing the file
geodata.sqlite

Run the geoload.py program.   This program will read the input
lines in where.data and for each line check to see if it is already
in the database and if we don't have the data for the location,
call the Geocoding API to retrieve the data and store it in
the database.

As of December 2016, the Google Geocoding APIs changed dramatically.
They moved some functionality that we use from the Geocoding API
into the Places API.  Also all the Google Geo-related APIs require an
API key. To execute these codes without a Google account,
without an API key, or from a country that blocks
access to Google, you can use a subset of that data which is
available [here](http://py4e-data.dr-chuck.net/json)

To use this, simply leave the api_key set to False in 
geoload.py.

This URL only has a subset of the data but it has no rate limit so
it is good for testing.

If you want to try this with the API key, follow the
instructions [here](https://developers.google.com/maps/documentation/geocoding/intro)

and put the API key in the code.

**Here is a sample run after there is already some data in the
database:**
![](images/sample1.JPG)

The geoload.py can be stopped at any time, and there is a counter
that you can use to limit the number of calls to the geocoding
API for each run.

Once you have some data loaded into geodata.sqlite, you can
visualize the data using the (geodump.py) program.  This
program reads the database and writes tile file (where.js)
with the location, latitude, and longitude in the form of
executable JavaScript code.

**Sample output after the run of the geodump.py program:**
![](images/sample2.JPG)

The file (where.html) consists of HTML and JavaScript to visualize
a Google Map.  It reads the most recent data in where.js to get
the data to be visualized.  Here is the format of the where.js file:

myData = [
[42.3396998,-71.08975, 'Northeastern University, 360 Huntington Avenue, Boston, MA 02115, USA'],
[40.6963857,-89.6160811, 'Bradley University, 1501 West Bradley Avenue, Peoria, IL 61625, USA'],
[32.7775,35.0216667, 'Technion, Viazman 87, Kesalsaba, 32000, Israel'],
   ...
];

This is a JavaScript list of lists.  The syntax for JavaScript
list constants is very similar to Python so the syntax should
be familiar to you.

Simply open where.html in a browser to see the locations.  You
can hover over each map pin to find the location that the
gecoding API returned for the user-entered input.  If you
cannot see any data when you open the where.html file, you might
want to check the JavaScript or developer console for your browser.

**Sample output after opening the where.html**
![](images/sample3.JPG)

![](images/sample4.JPG)

## Credits:
This projects was part of the online course "Using Python to Access Web Data" by Dr.Chuck (University of Michigan)
