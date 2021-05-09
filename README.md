# CS540 Nearest Evacuation Zone
This Github contains instructions on how to utilize the data contained in the "evaczones.zip" file. It contains the files, including the shape file that would be placed within QGIS. The problem that was presented via this final project, was to detemine the distance a parcel was from the nearest evaucation zone.

# Instructions
After downloading the recommended file, perform an update on the volusia.parcel table. There will be one added column, "nearest_evac_zone", that will contain the distance from a given parcel is from the nearest evacuation zone.

It is also recommended that you download the evaczones.zip file so you can use it in QGIS to visually see where the evacuation zones are located. Once downloaded you can use QGIS to import the .shp file as a new layer. When the layer has been imported correctly when the zones appear as a new layer near the coast.

# Applications used
- PostGres SQL
- pgAdmin
- Spyder
- QGIS 
- Volusia county shape files
