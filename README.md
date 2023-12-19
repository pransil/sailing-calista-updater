# sailing-calista-updater
GitHub cron job and shell to update gpx files for maps on the SailingCalista wordpress site.

On Calista (my sailboat) I have a RaspberryPI system that will log my lat,lon every minute in a time-based db. Every hour another db will be updated adding new lat/lon data points when the boat is moving. I will have some threshold and if (lat1 - lat0) + (lon1 - lon0) is above that threshold, the new point gets added. This should ignore points collected while docked or at anchor (the majority of the time). Call this db coordsTh.25 if the threshold is 0.25 nautical miles.

After coordsTh.25 is updated, it will be written to a file that gets uploaded to this GitHub repo. So far, this is all using code and a cron job on the RPI system on Calista. 

A Github-Action cron job will run each hour to
1. See if there is a new version of coordsTh.25 in the repo.
2. If so, run a script that updates a map on my wordpress site by forcing a 'republish' of any pages using the map. These maps use the Waymark pluggin that reads a gpx file each time the page using the map is republished.
