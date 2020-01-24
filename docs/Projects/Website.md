#This Website
---
![This Website](/img/material.png)
##Domain
This website uses Google domains a domain registration service offered by Google.

##Hosting
For hosting, I used a [Raspberry Pi 3 B+](https://amzn.to/2PQSVmL "Raspberry Pi 3 B+"), my original plan was to use digital ocean, a cloud computing company, but I chose the raspberry pi because it allows me to have full controll of my web server and everything on it and is a one time purchase rather than a series of monthly payments.

##Design
I designed this website using the [MkDocs material](https://squidfunk.github.io/mkdocs-material/) theme based off Google's material design.  I chose to use MkDocs because they have tons of great themes that I can edit to better fit my website.  I also used Disqus, a comment hosting service.

##Editing and Version History
To manage edits and version history on my website I use Github, a service for software development with integrated version control.  When I make an edit I begin by using a text editor by Microsoft called Visual Studio Code to edit the page or pages I want to change.  From there I can commit and push changes to github and the version is automatically documented and saved.  I then use SSH(Secure Shell), a network protocol to access remote devices to connect to the Raspberry Pi I use to host my website.  I can then pull the changed code from github and upload it to the live version of my website.  I am in the process of making this automated, making the process much easier by writing code to automatically pull code from github and post it to the live version of my website on the Raspberry Pi end.

<!--<div id="amzn-assoc-ad-f7e9c181-005b-4bb6-9d54-7952d3c68cdb"></div><script async src="//z-na.amazon-adsystem.com/widgets/onejs?MarketPlace=US&adInstanceId=f7e9c181-005b-4bb6-9d54-7952d3c68cdb"></script>-->