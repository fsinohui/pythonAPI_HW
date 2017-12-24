# pythonAPI_HW

Python API HW.
The temperature definatly gets hotter on average as you approach the equator. There are two low points in humidity between twenty and fourty for positive and negative lat. Wind gets stronger the further south y9u go past the equator. 


```python
import random
from citipy import citipy
import pandas as pd
import requests as req
import json
import matplotlib.pyplot as plt
```


```python
api_key = "afbde06f4217fea7175e8c03acbc3eac"
url = "http://api.openweathermap.org/data/2.5/weather?"
units = 'imperial'
query_url = url + "appid=" + api_key + "&units=" + units + "&q="
```


```python
count = 0
lats = []
lngs = []

while count < 1200:
    lats.append(random.uniform(-90,90))
    lngs.append(random.uniform(-180,180))
    count = count+1
```


```python
cities = ['london']
countries =['GB']
for lat, lng in zip(lats, lngs):
    cityid = citipy.nearest_city(lat, lng)
    city = cityid.city_name
    country = cityid.country_code
    cities.append(city)
    countries.append(country)
```


```python
temp_data       = []
lon_data        = [] 
temp_data       = []
lat_data        = []
humidity_data   = []
cloud_data      = []
wind_data       = []

for city in cities:
    weather_json = req.get(query_url + city).json()
    try:
        temp_data.append(weather_json['main']['temp'])
        lon_data.append(weather_json['coord']['lon'])
        lat_data.append(weather_json['coord']['lat'])
        humidity_data.append(weather_json['main']['humidity'])
        cloud_data.append(weather_json['clouds']['all'])
        wind_data.append(weather_json['wind']['speed'])
    except:
        print('no city found')

```

    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    no city found
    


```python
weather_data = {"lon": lon_data, 'temp':temp_data, 'lat':lat_data,'humidity':humidity_data, 'cloud':cloud_data, 'wind': wind_data}
weather_data = pd.DataFrame(weather_data)
weather_data.head() 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cloud</th>
      <th>humidity</th>
      <th>lat</th>
      <th>lon</th>
      <th>temp</th>
      <th>wind</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90</td>
      <td>87</td>
      <td>51.51</td>
      <td>-0.13</td>
      <td>46.74</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>100</td>
      <td>72.79</td>
      <td>-56.15</td>
      <td>10.92</td>
      <td>7.90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>75</td>
      <td>88</td>
      <td>-7.84</td>
      <td>-79.15</td>
      <td>66.20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>31</td>
      <td>-46.19</td>
      <td>168.86</td>
      <td>70.01</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>83</td>
      <td>-21.21</td>
      <td>-159.78</td>
      <td>73.40</td>
      <td>3.36</td>
    </tr>
  </tbody>
</table>
</div>




```python
weather_df = weather_data.drop_duplicates(keep='first')
weather_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cloud</th>
      <th>humidity</th>
      <th>lat</th>
      <th>lon</th>
      <th>temp</th>
      <th>wind</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90</td>
      <td>87</td>
      <td>51.51</td>
      <td>-0.13</td>
      <td>46.74</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>100</td>
      <td>72.79</td>
      <td>-56.15</td>
      <td>10.92</td>
      <td>7.90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>75</td>
      <td>88</td>
      <td>-7.84</td>
      <td>-79.15</td>
      <td>66.20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>31</td>
      <td>-46.19</td>
      <td>168.86</td>
      <td>70.01</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>83</td>
      <td>-21.21</td>
      <td>-159.78</td>
      <td>73.40</td>
      <td>3.36</td>
    </tr>
  </tbody>
</table>
</div>




```python
len(weather_df)
```




    504




```python
# Build a scatter plot for each data type
plt.scatter(weather_data["lat"], weather_data["temp"], marker="o")

# Incorporate the other graph properties
plt.title("Temperature in World Cities")
plt.ylabel("Temperature")
plt.xlabel("Latitude")
plt.show()
```


![png](output_9_0.png)



```python
plt.scatter(weather_data["lat"], weather_data["humidity"], marker="o")
plt.title("Humidity in World Cities")
plt.ylabel("Humidity")
plt.xlabel("Latitude")
plt.show()
```


![png](output_10_0.png)



```python
plt.scatter(weather_data["lat"], weather_data["cloud"], marker="o")
plt.title("Cloudiness in World Cities")
plt.ylabel("Cloudiness")
plt.xlabel("Latitude")
plt.show()
```


![png](output_11_0.png)



```python
plt.scatter(weather_data["lat"], weather_data["wind"], marker="o")
plt.title("wind in World Cities")
plt.ylabel("Wind Speed")
plt.xlabel("Latitude")
plt.show()
```


![png](output_12_0.png)

