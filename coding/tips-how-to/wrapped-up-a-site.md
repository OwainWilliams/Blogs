# Wrapped up a site

First thing is you need to check if there is pending work on Dev that isn't on the live environment.

If there is, (check by making a temp PR on DEV to UAT for example) this work really should get pushed up to LIVE through the usual steps e.g DEV->UAT, UAT-> LIVE



Assuming there isn't any changes, you'll want to pull down Develop, and then clean it up (remove connection strings, api keys etc).

Then zip it up without the .git hidden folder, (there is more you can clean up such as doing a VS clean on it to clear obj and bin folders, removing the packages folder etc other wise it will be 100's of MB big.

You'll also want to zip up the live Umbraco forms, and Media from blob storage, and then the live database.

\
