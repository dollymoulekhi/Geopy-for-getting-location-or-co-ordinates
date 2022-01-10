# Geopy-for-getting-location-or-coordinates

## Geopy used for getting the location from a village - (like district and state)

### Importing required modules
```
import geopy
from geopy.geocoders import Nominatim
from geopy.extra.rate_limiter import RateLimiter
from geopy import distance

import pandas as pd
from ipyleaflet import Map, AntPath, MeasureControl
import ipywidgets
```


### Nominatim geocoder for OpenStreetMap data with RateLimiter

```
geocoder = RateLimiter(Nominatim(user_agent='tutorial').geocode, min_delay_seconds=1)
district_mapped_1['Location'] = district_mapped_1['Invalid district data'].apply(geocoder)
```


### add latitude and longitude to dataframe

```
district_mapped_1['Latitude'] = district_mapped_1['Location'].apply(lambda loc: loc.latitude if loc else None)
district_mapped_1['Longitude'] = district_mapped_1['Location'].apply(lambda loc: loc.longitude if loc else None)

district_mapped_1

```

### combining latitude and longitude

```
district_mapped_1['Latitude']=district_mapped_1['Latitude'].astype(str)
district_mapped_1['Longitude']=district_mapped_1['Longitude'].astype(str)
district_mapped_1['geo-coordinates'] = district_mapped_1[['Latitude','Longitude']].apply(lambda x: ','.join(x), axis = 1)
district_mapped_1
```

### according to geo-coordinates getting the district of that location

```
geolocator = Nominatim(user_agent="geoapiExercises")
dict_1={}
for i in a:
#     print(i)
#     print(type(i))
    x=geolocator.reverse(i)
#     print(x)
    address=x.raw['address']
#     print(address)
    if 'state_district' in address.keys():
        dict_1[i]= address['state_district']
dict_1
```
