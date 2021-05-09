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

select AddGeometryColumn ('volusia','parcel','geom','2236','MULTIPOLYGON',2);
update volusia.parcel a set geom = p.geom from volusia.gis_parcels p where a.parid=p.altkey;
alter table volusia.parcel add nearest_evac_route double precision;

Within the Python code, there are two important SQL commands being ran:
These commands run through each row within the parcel table and calcualtes the distance and then is added to the parcel table under "nearest_evac_route" from the second command.
- sql2 = "select p.parid::integer, p.geom, ST_Distance(p.geom, (select p2.geom from volusia.parcel p2 where p2.parid=" + parid + "))/5280 from volusia.parcel p where p.luc='0000' or p.luc='0100' or p.luc='0200' or p.luc='0400' or p.luc='0800' order by p.geom <-> (select p2.geom from volusia.parcel p2 where p2.parid=" + parid + ") limit 1;"
    cur2.execute(sql2)
- sql3 = "update volusia.parcel p1 set nearest_evac_route = " + str(distance) + " where p1.parid=" + parid + ";"

To view data and to clean up:
-create index idx_parcel_luc on volusia.parcel(luc);
- create index idx_parcel on volusia.parcel(paris);
- create index parcel_geom_idx on volusia.parcel using GIST(geom);
- vacuum analyze volusia.parcel;
- select parid, luc, luc_desc, nearest_evac_route from volusia.parcel where nearest_evac_route is not null limit 20;


