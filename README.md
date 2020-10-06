# Wether-Forecast-in-Google-Colab

Perform a weather forecast in a Jupyter notebook for France (5 cities) using IBM Weather Company Data on Google Colaboratory

Use this sample tutorial as reference:

https://developer.ibm.com/clouddataservices/2016/10/06/your-own-weather-forecast-in-a-python-notebook/

Outcome:  Jupyter notebook with results (including final two map diagrams) should be zipped up as a compressed file and uploaded to the created “turnit-in” link.

Use Jupyter notebook: Python 2.7, spark 2.1.0 flavor.  Python 3.x has a defect (bug) regarding matplotlib toolkit (mpl_toolkits basemap).

Reference:  https://github.com/ibm-watson-data-lab/python-notebooks/blob/master/Weather%20forecast.ipynb

Instead of London and Great Britain (England) use Paris and France as subject of the weather forecast. This is Homework Requirement

Implement the forecast for the following cities:
    'Paris',48.864716, 2.349014
    'Le Mans',48.0061, 0.1996
    'Nantes',47.2184, 1.5536
    'Rennes',48.1173, 1.6778
    'Tours',47.3941, 0.6848
    'Angers',47.4784, 0.5632

The sample Jupyter notebook has couple of defects (bugs).  See below potential corrections you may need to apply:
A:
# extract time and use it as index
time = np.array(df['fcst_valid_local'])
for row in range(len(time)):
    time[row] = datetime.strptime(time[row], '%Y-%m-%dT%H:%M:%S+%f')

(In some case may need to use this datetime template:  '%Y-%m-%dT%H:%M:%S-%f' )

B:
# weather icons map
for [icon,city] in izip(icons,cities):
 		 if (icon != None):
       		 	lat = city[1]
       			 lon = city[2]
pngfile=urllib.urlopen('https://github.com/ibm-cds-labs/python-notebooks/blob/master/weathericons/icon'+str(int(icon))+'.png?raw=true')
        			icon_hand = read_png(pngfile)
        			imagebox = OffsetImage(icon_hand, zoom=.15)
       			ab = AnnotationBbox(imagebox,m1(lon,lat),frameon=False) 
        			axes[0].add_artist(ab)
 
# temperature colors   


Sample expected outcome:

 


This homework will allow you to work with multiple type of big data:
	Weather Data
	Location data (Latitude, Longitude)
	Various types of visualization using MAPs
	Plotting timeseries data:

Plot the following values: Temperature, Rain, WindDirection, WindSpeed, Clouds, like shown below:

 

Tip for how to generate the new map:
Basemap(projection='mill',resolution=None,llcrnrlon=-0.5,llcrnrlat=45.0,urcrnrlon=3.5,urcrnrlat=51.0 ,
