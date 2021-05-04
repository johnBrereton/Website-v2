# NYC Hotspot Locator
---

<iframe width="372" height="620" style="border: 0px;" src="https://studio.code.org/projects/applab/9Dz03zbi1JHIcJ2rHklY8a4pPKmypWLozo1iONFKGEw/embed"></iframe>

[:octicons-file-code-24: Source](https://github.com/johnBrereton/NYC-Hotspot-Locator)

The NYC Hotspot locator is a simple JavaScript app with UI designed in Code.org App Lab.  I used the Code.org ["NYC Public Wifi Locations" dataset](https://github.com/johnBrereton/NYC-Hotspot-Locator/blob/main/NYC%20Public%20Wifi%20Locations.csv) which contains about 2,500 entries and sufficent information for each location.  The application uses the user entered latitude and longitude to calculate the distance between the user and each Wi-Fi hotspot in the dataset.  This data is then sorted into an ordered list and displayed for the user, unfortunately list sorting in JavaScript is very inneficient especially with large data sets, resulting in a 2 to 4 minute wait.  The source code is on [Github](https://github.com/johnBrereton/NYC-Hotspot-Locator) along with the UI converted into and HTML file and all the necessary dependancies to run the program.

*[UI] : User Interface
*[HTML] : HyperText Markup Language