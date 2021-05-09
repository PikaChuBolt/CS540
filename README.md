# CS540 Nearest Evacuation Route
This Github contains instructions on how to utilize the data contained in the "evaczones.zip" file. It contains the files, including the shape file that would be placed within QGIS. The problem that was presented via this final project, was to detemine the distance a parcel was from the nearest evaucation zone.

# Instructions
After downloading the recommended file, perform an update on the volusia.parcel table with the given command at the bottom. There will be one added column, "nearest_evac_route", that will contain the distance from a given parcel is from the nearest evacuation zone. Before running "evac.py" be sure to change the Postgres password It is also recommended that you download the evaczones.zip file so you can use it in QGIS to visually see where the evacuation zones are located. Once downloaded you can use QGIS to import the .shp file as a new layer. When the layer has been imported correctly when the zones appear as a new layer near the coast.

# Applications used
- PostGres SQL
- pgAdmin
- Spyder
- QGIS 
- Volusia county shape files

# SQL Commands
To determine the distance for each parcel in a county, a Python script was created in order to loop through the county entirely, excluding the "null" geometries. The SQL command, before running the python code, to be used:

alter table volusia.parcel add nearest_evac_route double precision;
