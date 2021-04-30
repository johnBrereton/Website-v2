# NYC Hotspot Locator
---

<iframe width="372" height="620" style="border: 0px;" src="https://studio.code.org/projects/applab/9Dz03zbi1JHIcJ2rHklY8a4pPKmypWLozo1iONFKGEw/embed"></iframe>```
/**
 * Simple Code.org JS app to find the closest Wi-Fi hotspot in NYC
 * Uses Code.org "NYC Public Wifi Locations" dataset
 * Uses about 9,000,000 traversals to sort the list of over 2,500 distances
 * @author John Brereton
 * @since 4/20/2021
 */

// Create lists to represent the dataset
var providerList = getColumn("NYC Public Wifi Locations", "Provider");
var locationList = getColumn("NYC Public Wifi Locations", "Location");
var latitudeList = getColumn("NYC Public Wifi Locations", "Latitude");
var longitudeList = getColumn("NYC Public Wifi Locations", "Longitude");
var accessList = getColumn("NYC Public Wifi Locations", "Access Location");
var boroughList = getColumn("NYC Public Wifi Locations", "Borough");
var neighborhoodList = getColumn("NYC Public Wifi Locations", "Neighborhood");
var zipList = getColumn("NYC Public Wifi Locations", "Postal Code");

// List to store the distance between each access point location and the user entered location
var distList = [];
var sortedIdList = [];

// Miles are now used for all distance calculations
// var distListMiles = [];

// Booleans that indicate wheather or not an error has been made when entering latitude and longitude
var latError;
var longError;

// Stores the results page currently being viewed
var resultsPage = 0;

// Stores the reference number of the location being viewed on the info page
var infoId;

// Stores the distance between the user entered lat and long and the item being traversed
var dist;

// Miles are now used for all distance calculations
// var distMiles;

// Finds and organizes the closest hotspots when the go button is clicked
onEvent("goButton", "click", function() {
    if(validateFields()) {
        setScreen("loadingScreen");
        generateDistList();
        sortedIdList = sortList(distList)[1];
        updateResults();
        setScreen("resultsScreen");
    }
});

// Returns to the home screen when the results screen back button is pressed
onEvent("resultsBackButton", "click", function() {
    setScreen("homeScreen");
    resultsPage = 0;
});

// Returns to the results screen when the info screen back button is pressed
onEvent("infoBackButton", "click", function() {
    setScreen("resultsScreen");
});

// Changes to the previous page when the previous arrow is clicked
onEvent("prevButton", "click", function() {
    if(resultsPage>0) {
        resultsPage--;
        updateResults();
    }
});

// Changes to the next page when the next arrow is clicked
onEvent("nextButton", "click", function() {
    if(resultsPage<512) {
        resultsPage++;
        updateResults();
    }
});

// On event for the first result
// Sets the info id and runs the function to update the info screen
onEvent("result0", "click", function() {
    infoId = (5*resultsPage);
    updateInfo();
    setScreen("infoScreen");
});

// On event for the second result
onEvent("result1", "click", function() {
    infoId = (5*resultsPage)+1;
    updateInfo();
    setScreen("infoScreen");
});

// On event for the third result
onEvent("result2", "click", function() {
    infoId = (5*resultsPage)+2;
    updateInfo();
    setScreen("infoScreen");
});

// On event for the fourth result
onEvent("result3", "click", function() {
    infoId = (5*resultsPage)+3;
    updateInfo();
    setScreen("infoScreen");
});

// On event for the fifth result
onEvent("result4", "click", function() {
    infoId = (5*resultsPage)+4;
    updateInfo();
    setScreen("infoScreen");
});

// Validates that the latitude and longitude values the user enters are valid
// Checks that they are not blank
// Checks that they are a number
// Checks that they are within the latitude and longitude of NYC
function validateFields() {
    // Verifies latitude input
    if(getText("latitudeInput") == "") {
        setProperty("latitudeWarning", "text", "This is a required field");
        latError = true;
    }
    else if(isNaN(getText("latitudeInput"))) {
        setProperty("latitudeWarning", "text", "Please enter a valid number");
        latError = true;
    }
    else if(getText("latitudeInput") > calcMaxMin(latitudeList)[0] || getText("latitudeInput") < calcMaxMin(latitudeList)[1]) {
        setProperty("latitudeWarning", "text", "Please enter a latitudinal value within NYC");
        latError = true;
    }
    else {
        latError = false;
        setProperty("latitudeWarning", "text", "");
    }

    // Verifies longitude input
    if(getText("longitudeInput") == "") {
        setProperty("longitudeWarning", "text", "This is a required field");
        longError = true;
    }
    else if(isNaN(getText("longitudeInput"))) {
        setProperty("longitudeWarning", "text", "Please enter a valid number");
        longError = true;
    }
    else if(getText("longitudeInput") > calcMaxMin(longitudeList)[0] || getText("longitudeInput") < calcMaxMin(longitudeList)[1]) {
        setProperty("longitudeWarning", "text", "Please enter a longitudinal value within NYC");
        longError = true;
    }
    else {
        longError = false;
        setProperty("longitudeWarning", "text", "");
    }

    // Returns weather or not the user made a mistake in entering their latitude and longitude
    if(latError == false && longError == false) {
        return true;
    }
    else {
        return false;
    }
}

// Calculates the maximum and minimum value of an list
// Returns values as an list
function calcMaxMin(calcList) {
    var max = calcList[0];
    var min = calcList[0];
    for(var i=0; i < calcList.length; i++) {
        if(calcList[i] > max) {
            max = calcList[i];
        }
        else if(calcList[i] < min) {
            min = calcList[i];
        }
    }
    return [max, min];
}

// Generates list of distances from the user in miles and coordinate values
function generateDistList() {
    var userLatitude = getText("latitudeInput");
    var userLongitude = getText("longitudeInput");
    for(var i = 0; i < providerList.length; i++) {
        // Old method, used latitude and longitude wihtout miles conversion
        // Since latitude and longitude are not equal measurements this method was not accurate
        // dist = Math.sqrt(Math.abs((Math.abs(userLatitude)-Math.abs(latitudeList[i])))+Math.abs((Math.abs(userLongitude)-Math.abs(longitudeList[i]))));
        // distList[i] = dist;

        // New method, converts latitude and longitude to miles
        dist = Math.round(Math.sqrt((Math.pow(Math.abs((userLatitude*69)-(latitudeList[i]*69)), 2)) + (Math.pow(Math.abs((userLongitude*54.6)-(longitudeList[i]*54.6)), 2)))*100)/100;
        distList[i] = dist;
    }
}

// Sorts list from least to greatest
// Returns list of sorted values and a list of their origional list ids
// Uses two for loops to go through every possible combination of two values in the list and see which one is greater
// If the larger number is in front of the smaller number their positions will be exchanged
function sortList(list) {
    var sortedList = [];
    var sortedIds = [];
    var temp = 0;
    sortedList = list;
    sortedIds = createNumericalList(0, list.length);
    for (var i = 0; i < sortedList.length; i++) {
        for (var j=i; j < sortedList.length; j++) {
            if (sortedList[j] < sortedList[i]) {
                temp = sortedIds[j];
                sortedIds[j] = sortedIds[i];
                sortedIds[i] = temp;

                temp = sortedList[j];
                sortedList [j] = sortedList[i];
                sortedList[i] = temp;
            }
        }
    }
    return [sortedList, sortedIds];
}

// Creates a list of consecutive integers
// Requires a starting(from) and ending(to) number
function createNumericalList(from, to) {
    var list = [];
    for (var i=from; i<=to; i++) {
        appendItem(list, i);
    }
    return list;
}

// Updates the results page
// Shows results in order from closest to furthest using the sorted id list
function updateResults() {
    for (var i=0; i<=4; i++) {
        setProperty("result" + i, "text", "Location: " + locationList[sortedIdList[(5*resultsPage)+i]] + " " + boroughList[sortedIdList[(5*resultsPage)+i]] +
                                        " NYC\nProvider: " + providerList[sortedIdList[(5*resultsPage)+i]]);
    }
    setProperty("pageLabel", "text", "Page: " + (resultsPage+1) + " of 513");
}

// Updates the info page
// Info id represents which button was clicked
// Sorted id list is used to make info corespond to correct button on results page
// Only takes the first 20 values of the string to prevent the string from expanding into a second line
function updateInfo() {
    setProperty("infoOutput", "text", distList[sortedIdList[infoId]] + " Miles" +
                                    "\n" + providerList[sortedIdList[infoId]] +
                                    "\n" + locationList[sortedIdList[infoId]].toString().substring(0, 20) +
                                    "\n" + accessList[sortedIdList[infoId]].toString().substring(0, 20) +
                                    "\n" + boroughList[sortedIdList[infoId]].toString().substring(0, 20) +
                                    "\n" + neighborhoodList[sortedIdList[infoId]].toString().substring(0, 20) +
                                    "\n" + zipList[sortedIdList[infoId]].toString().substring(0, 20));
}
```

[:octicons-file-code-24: Source](https://github.com/johnBrereton/NYC-Hotspot-Locator)

The NYC Hotspot locator is a simple JavaScript app with UI designed in Code.org App Lab.  I used the Code.org ["NYC Public Wifi Locations" dataset](https://github.com/johnBrereton/NYC-Hotspot-Locator/blob/main/NYC%20Public%20Wifi%20Locations.csv) which contains about 2,500 entries and sufficent information for each location.  The application uses the user entered latitude and longitude to calculate the distance between the user and each Wi-Fi hotspot in the dataset.  This data is then sorted into an ordered list and displayed for the user, unfortunately list sorting in JavaScript is very inneficient especially with large data sets, resulting in a 2 to 4 minute wait.  The source code is on [Github](https://github.com/johnBrereton/NYC-Hotspot-Locator) along with the UI converted into and HTML file and all the necessary dependancies to run the program.

*[UI] : User Interface