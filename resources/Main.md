

```python
#installed citipy and seaborn
#! pip install citipy
#! pip install seaborn
```


```python
#import dependencies

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import requests
import random
import citipy
import seaborn as sns
```


```python
# openweather api key
api_key = "e5760248211a864fbc4f4418cc6d872d"
```


```python
#from citipy import citipy

#import cities from citipy
cities = pd.read_csv("https://raw.githubusercontent.com/wingchen/citipy/master/citipy/worldcities.csv")


#take a sample of 500 cities
random_cities = pd.DataFrame(cities.sample(n=550))
random_cities.reset_index(inplace = True)
random_cities

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
      <th>index</th>
      <th>Country</th>
      <th>City</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>43594</td>
      <td>us</td>
      <td>lexington-fayette</td>
      <td>38.049722</td>
      <td>-84.458611</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3727</td>
      <td>br</td>
      <td>porto real</td>
      <td>-22.417200</td>
      <td>-44.286100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>42803</td>
      <td>us</td>
      <td>clermont</td>
      <td>28.549167</td>
      <td>-81.773056</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45740</td>
      <td>us</td>
      <td>pecan grove</td>
      <td>29.625833</td>
      <td>-95.731389</td>
    </tr>
    <tr>
      <th>4</th>
      <td>44404</td>
      <td>us</td>
      <td>barnstead</td>
      <td>43.333889</td>
      <td>-71.293333</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25835</td>
      <td>no</td>
      <td>flateby</td>
      <td>59.833333</td>
      <td>11.166667</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17403</td>
      <td>in</td>
      <td>chatsu</td>
      <td>26.600000</td>
      <td>75.950000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>30124</td>
      <td>ph</td>
      <td>santo nino</td>
      <td>13.701800</td>
      <td>121.094900</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18193</td>
      <td>in</td>
      <td>kelamangalam</td>
      <td>12.600000</td>
      <td>77.850000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>41131</td>
      <td>ua</td>
      <td>auly</td>
      <td>48.527081</td>
      <td>34.494931</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19069</td>
      <td>in</td>
      <td>puranpur</td>
      <td>28.516667</td>
      <td>80.150000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>28009</td>
      <td>ph</td>
      <td>damortis</td>
      <td>16.242300</td>
      <td>120.405100</td>
    </tr>
    <tr>
      <th>12</th>
      <td>39987</td>
      <td>sv</td>
      <td>tenancingo</td>
      <td>13.833333</td>
      <td>-88.983333</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14405</td>
      <td>gr</td>
      <td>ziparion</td>
      <td>36.875000</td>
      <td>27.204167</td>
    </tr>
    <tr>
      <th>14</th>
      <td>17434</td>
      <td>in</td>
      <td>chikmagalur</td>
      <td>13.316667</td>
      <td>75.783333</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8673</td>
      <td>de</td>
      <td>calbe</td>
      <td>51.900000</td>
      <td>11.766667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>540</td>
      <td>ar</td>
      <td>san vicente</td>
      <td>-34.982645</td>
      <td>-58.376169</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18476</td>
      <td>in</td>
      <td>mahbubnagar</td>
      <td>16.733333</td>
      <td>77.983333</td>
    </tr>
    <tr>
      <th>18</th>
      <td>15130</td>
      <td>hn</td>
      <td>san francisco de yojoa</td>
      <td>15.016667</td>
      <td>-87.966667</td>
    </tr>
    <tr>
      <th>19</th>
      <td>9144</td>
      <td>de</td>
      <td>kronberg</td>
      <td>50.183333</td>
      <td>8.500000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>164</td>
      <td>am</td>
      <td>arapi</td>
      <td>40.779722</td>
      <td>43.800556</td>
    </tr>
    <tr>
      <th>21</th>
      <td>36747</td>
      <td>ru</td>
      <td>kysyl-syr</td>
      <td>63.898611</td>
      <td>122.761667</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23395</td>
      <td>mx</td>
      <td>armeria</td>
      <td>18.915278</td>
      <td>-103.969444</td>
    </tr>
    <tr>
      <th>23</th>
      <td>17323</td>
      <td>in</td>
      <td>bodinayakkanur</td>
      <td>10.016667</td>
      <td>77.350000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>21650</td>
      <td>jp</td>
      <td>ninomiya</td>
      <td>35.303333</td>
      <td>139.253333</td>
    </tr>
    <tr>
      <th>25</th>
      <td>41193</td>
      <td>ua</td>
      <td>borzna</td>
      <td>51.254645</td>
      <td>32.426901</td>
    </tr>
    <tr>
      <th>26</th>
      <td>21971</td>
      <td>ke</td>
      <td>butere</td>
      <td>0.209444</td>
      <td>34.492778</td>
    </tr>
    <tr>
      <th>27</th>
      <td>41115</td>
      <td>tz</td>
      <td>uyovu</td>
      <td>-3.283333</td>
      <td>31.525833</td>
    </tr>
    <tr>
      <th>28</th>
      <td>18676</td>
      <td>in</td>
      <td>mundgod</td>
      <td>14.966667</td>
      <td>75.033333</td>
    </tr>
    <tr>
      <th>29</th>
      <td>8492</td>
      <td>de</td>
      <td>bad durkheim</td>
      <td>49.468611</td>
      <td>8.166389</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>520</th>
      <td>1</td>
      <td>ad</td>
      <td>canillo</td>
      <td>42.566667</td>
      <td>1.600000</td>
    </tr>
    <tr>
      <th>521</th>
      <td>14156</td>
      <td>gr</td>
      <td>poliplatanos</td>
      <td>40.682500</td>
      <td>22.191389</td>
    </tr>
    <tr>
      <th>522</th>
      <td>31632</td>
      <td>pt</td>
      <td>lagos</td>
      <td>37.101782</td>
      <td>-8.674242</td>
    </tr>
    <tr>
      <th>523</th>
      <td>36596</td>
      <td>ru</td>
      <td>krasnoye</td>
      <td>52.729500</td>
      <td>39.162900</td>
    </tr>
    <tr>
      <th>524</th>
      <td>27794</td>
      <td>ph</td>
      <td>caningay</td>
      <td>9.829700</td>
      <td>122.644200</td>
    </tr>
    <tr>
      <th>525</th>
      <td>8293</td>
      <td>cz</td>
      <td>steti</td>
      <td>50.453141</td>
      <td>14.378383</td>
    </tr>
    <tr>
      <th>526</th>
      <td>9843</td>
      <td>de</td>
      <td>wertheim</td>
      <td>49.757500</td>
      <td>9.509444</td>
    </tr>
    <tr>
      <th>527</th>
      <td>22318</td>
      <td>lk</td>
      <td>monaragala</td>
      <td>6.866667</td>
      <td>81.350000</td>
    </tr>
    <tr>
      <th>528</th>
      <td>19008</td>
      <td>in</td>
      <td>phaphund</td>
      <td>26.600000</td>
      <td>79.466667</td>
    </tr>
    <tr>
      <th>529</th>
      <td>16456</td>
      <td>id</td>
      <td>prambanan</td>
      <td>-7.750000</td>
      <td>110.494167</td>
    </tr>
    <tr>
      <th>530</th>
      <td>23312</td>
      <td>mx</td>
      <td>ahuacatlan</td>
      <td>21.050000</td>
      <td>-104.483333</td>
    </tr>
    <tr>
      <th>531</th>
      <td>6509</td>
      <td>cn</td>
      <td>yushan</td>
      <td>31.377623</td>
      <td>120.954305</td>
    </tr>
    <tr>
      <th>532</th>
      <td>38381</td>
      <td>ru</td>
      <td>stoyba</td>
      <td>52.800000</td>
      <td>131.700000</td>
    </tr>
    <tr>
      <th>533</th>
      <td>46499</td>
      <td>ws</td>
      <td>sapapalii</td>
      <td>-13.683333</td>
      <td>-172.116667</td>
    </tr>
    <tr>
      <th>534</th>
      <td>42517</td>
      <td>us</td>
      <td>rubidoux</td>
      <td>33.996111</td>
      <td>-117.404722</td>
    </tr>
    <tr>
      <th>535</th>
      <td>229</td>
      <td>am</td>
      <td>dashtavan</td>
      <td>40.101667</td>
      <td>44.390556</td>
    </tr>
    <tr>
      <th>536</th>
      <td>16028</td>
      <td>hu</td>
      <td>szigetszentmiklos</td>
      <td>47.343819</td>
      <td>19.043351</td>
    </tr>
    <tr>
      <th>537</th>
      <td>21909</td>
      <td>jp</td>
      <td>urayasu</td>
      <td>35.663338</td>
      <td>139.908548</td>
    </tr>
    <tr>
      <th>538</th>
      <td>46339</td>
      <td>ve</td>
      <td>la fria</td>
      <td>8.218889</td>
      <td>-72.248333</td>
    </tr>
    <tr>
      <th>539</th>
      <td>13021</td>
      <td>gb</td>
      <td>walkerburn</td>
      <td>55.633333</td>
      <td>-3.016667</td>
    </tr>
    <tr>
      <th>540</th>
      <td>38961</td>
      <td>ru</td>
      <td>volokolamsk</td>
      <td>56.038968</td>
      <td>35.957021</td>
    </tr>
    <tr>
      <th>541</th>
      <td>34930</td>
      <td>rs</td>
      <td>mali zvornik</td>
      <td>44.395278</td>
      <td>19.115833</td>
    </tr>
    <tr>
      <th>542</th>
      <td>7282</td>
      <td>co</td>
      <td>san andres</td>
      <td>6.903333</td>
      <td>-75.682500</td>
    </tr>
    <tr>
      <th>543</th>
      <td>141</td>
      <td>al</td>
      <td>vore</td>
      <td>41.390833</td>
      <td>19.655000</td>
    </tr>
    <tr>
      <th>544</th>
      <td>45403</td>
      <td>us</td>
      <td>salinas</td>
      <td>17.979444</td>
      <td>-66.298333</td>
    </tr>
    <tr>
      <th>545</th>
      <td>41315</td>
      <td>ua</td>
      <td>ispas</td>
      <td>48.297342</td>
      <td>25.274064</td>
    </tr>
    <tr>
      <th>546</th>
      <td>31069</td>
      <td>pl</td>
      <td>czechowice-dziedzice</td>
      <td>49.913416</td>
      <td>19.004789</td>
    </tr>
    <tr>
      <th>547</th>
      <td>16573</td>
      <td>id</td>
      <td>wonosari</td>
      <td>-7.306111</td>
      <td>110.773889</td>
    </tr>
    <tr>
      <th>548</th>
      <td>5631</td>
      <td>cl</td>
      <td>bulnes</td>
      <td>-36.733333</td>
      <td>-72.300000</td>
    </tr>
    <tr>
      <th>549</th>
      <td>46410</td>
      <td>vn</td>
      <td>ha giang</td>
      <td>22.833333</td>
      <td>104.983333</td>
    </tr>
  </tbody>
</table>
<p>550 rows × 5 columns</p>
</div>




```python
# openweathermap API
rowcount = 0
random_cities['Temperature'] = ""
random_cities['Humidity'] = ""
random_cities['Cloudiness'] = ""
random_cities['Wind Speed'] = ""


for index, row in random_cities.iterrows():
   
    
    targetCityNumber = row['index']
    targetCity = row['City']
    targetCountry = row['Country']
    targetURL = "http://api.openweathermap.org/data/2.5/weather?q={},{}&units=IMPERIAL&mode=json&APPID={}".format(targetCity, targetCountry, api_key)
    targetURL = targetURL.replace(" ","+")
    
    cityWeather = requests.get(targetURL).json()
    
    try:
        tempF = cityWeather["main"]["temp"]
        humidity = cityWeather["main"]["humidity"]
        cloudiness = cityWeather["clouds"]["all"]
        windspeed = cityWeather["wind"]["speed"]

        random_cities.set_value(index, "Temperature", tempF)
        random_cities.set_value(index, "Humidity", humidity)
        random_cities.set_value(index, "Cloudiness", cloudiness)
        random_cities.set_value(index, "Wind Speed", windspeed)
    except:
        continue

       
    
    rowcount+=1
    
    print("----------------------------")
    print("Retreiving City #: {}".format(rowcount))
    print("City Number: {}".format(targetCityNumber))
    print("City: {}".format(targetCity))
    print("Country: {}".format(targetCountry))
    print(targetURL)
    
randomcitiesDF = pd.DataFrame(random_cities)
randomcitiesDF
```

    ----------------------------
    Retreiving City #: 1
    City Number: 43594
    City: lexington-fayette
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=lexington-fayette,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 2
    City Number: 3727
    City: porto real
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=porto+real,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 3
    City Number: 42803
    City: clermont
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=clermont,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 4
    City Number: 45740
    City: pecan grove
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=pecan+grove,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 5
    City Number: 44404
    City: barnstead
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=barnstead,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 6
    City Number: 25835
    City: flateby
    Country: no
    http://api.openweathermap.org/data/2.5/weather?q=flateby,no&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 7
    City Number: 30124
    City: santo nino
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=santo+nino,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 8
    City Number: 18193
    City: kelamangalam
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=kelamangalam,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 9
    City Number: 41131
    City: auly
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=auly,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 10
    City Number: 19069
    City: puranpur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=puranpur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 11
    City Number: 28009
    City: damortis
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=damortis,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 12
    City Number: 39987
    City: tenancingo
    Country: sv
    http://api.openweathermap.org/data/2.5/weather?q=tenancingo,sv&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 13
    City Number: 14405
    City: ziparion
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=ziparion,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 14
    City Number: 17434
    City: chikmagalur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=chikmagalur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 15
    City Number: 8673
    City: calbe
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=calbe,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 16
    City Number: 540
    City: san vicente
    Country: ar
    http://api.openweathermap.org/data/2.5/weather?q=san+vicente,ar&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 17
    City Number: 18476
    City: mahbubnagar
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=mahbubnagar,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 18
    City Number: 15130
    City: san francisco de yojoa
    Country: hn
    http://api.openweathermap.org/data/2.5/weather?q=san+francisco+de+yojoa,hn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 19
    City Number: 9144
    City: kronberg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=kronberg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 20
    City Number: 36747
    City: kysyl-syr
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=kysyl-syr,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 21
    City Number: 23395
    City: armeria
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=armeria,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 22
    City Number: 17323
    City: bodinayakkanur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=bodinayakkanur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 23
    City Number: 21650
    City: ninomiya
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=ninomiya,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 24
    City Number: 41193
    City: borzna
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=borzna,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 25
    City Number: 21971
    City: butere
    Country: ke
    http://api.openweathermap.org/data/2.5/weather?q=butere,ke&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 26
    City Number: 41115
    City: uyovu
    Country: tz
    http://api.openweathermap.org/data/2.5/weather?q=uyovu,tz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 27
    City Number: 18676
    City: mundgod
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=mundgod,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 28
    City Number: 8492
    City: bad durkheim
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=bad+durkheim,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 29
    City Number: 27494
    City: bolo
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=bolo,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 30
    City Number: 14493
    City: ixtahuacan
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=ixtahuacan,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 31
    City Number: 8253
    City: rudolfov
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=rudolfov,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 32
    City Number: 4894
    City: princeton
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=princeton,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 33
    City Number: 5686
    City: parral
    Country: cl
    http://api.openweathermap.org/data/2.5/weather?q=parral,cl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 34
    City Number: 34
    City: jurm
    Country: af
    http://api.openweathermap.org/data/2.5/weather?q=jurm,af&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 35
    City Number: 24832
    City: valparaiso
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=valparaiso,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 36
    City Number: 34080
    City: sacelu
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=sacelu,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 37
    City Number: 44221
    City: white bear lake
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=white+bear+lake,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 38
    City Number: 27020
    City: amadeo
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=amadeo,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 39
    City Number: 1760
    City: sint-truiden
    Country: be
    http://api.openweathermap.org/data/2.5/weather?q=sint-truiden,be&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 40
    City Number: 43901
    City: holliston
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=holliston,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 41
    City Number: 30140
    City: san vicente
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=san+vicente,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 42
    City Number: 19570
    City: tasgaon
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=tasgaon,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 43
    City Number: 37065
    City: mokhsogollokh
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=mokhsogollokh,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 44
    City Number: 11598
    City: fecamp
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=fecamp,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 45
    City Number: 14463
    City: el asintal
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=el+asintal,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 46
    City Number: 25761
    City: alvdal
    Country: no
    http://api.openweathermap.org/data/2.5/weather?q=alvdal,no&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 47
    City Number: 23602
    City: chontalpa
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=chontalpa,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 48
    City Number: 26551
    City: santa rita
    Country: pa
    http://api.openweathermap.org/data/2.5/weather?q=santa+rita,pa&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 49
    City Number: 16742
    City: bet shemesh
    Country: il
    http://api.openweathermap.org/data/2.5/weather?q=bet+shemesh,il&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 50
    City Number: 14694
    City: tacana
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=tacana,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 51
    City Number: 5095
    City: waterloo
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=waterloo,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 52
    City Number: 1624
    City: lille
    Country: be
    http://api.openweathermap.org/data/2.5/weather?q=lille,be&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 53
    City Number: 18368
    City: kumhari
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=kumhari,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 54
    City Number: 21845
    City: tateyama
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=tateyama,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 55
    City Number: 11842
    City: montesson
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=montesson,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 56
    City Number: 37174
    City: nekrasovka
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=nekrasovka,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 57
    City Number: 38606
    City: trosna
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=trosna,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 58
    City Number: 173
    City: arevik
    Country: am
    http://api.openweathermap.org/data/2.5/weather?q=arevik,am&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 59
    City Number: 34703
    City: victoria
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=victoria,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 60
    City Number: 25830
    City: fevik
    Country: no
    http://api.openweathermap.org/data/2.5/weather?q=fevik,no&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 61
    City Number: 22276
    City: triesenberg
    Country: li
    http://api.openweathermap.org/data/2.5/weather?q=triesenberg,li&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 62
    City Number: 12343
    City: bridgend
    Country: gb
    http://api.openweathermap.org/data/2.5/weather?q=bridgend,gb&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 63
    City Number: 39520
    City: hrastnik
    Country: si
    http://api.openweathermap.org/data/2.5/weather?q=hrastnik,si&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 64
    City Number: 8346
    City: uhlirske janovice
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=uhlirske+janovice,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 65
    City Number: 18557
    City: mangaldai
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=mangaldai,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 66
    City Number: 10000
    City: harboore
    Country: dk
    http://api.openweathermap.org/data/2.5/weather?q=harboore,dk&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 67
    City Number: 18226
    City: khanpur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=khanpur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 68
    City Number: 27678
    City: cabul-an
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=cabul-an,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 69
    City Number: 29676
    City: sabang
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=sabang,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 70
    City Number: 27128
    City: bacong
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=bacong,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 71
    City Number: 5976
    City: guiren
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=guiren,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 72
    City Number: 31056
    City: chelmno
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=chelmno,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 73
    City Number: 26224
    City: kawakawa
    Country: nz
    http://api.openweathermap.org/data/2.5/weather?q=kawakawa,nz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 74
    City Number: 23204
    City: quatre soeurs
    Country: mu
    http://api.openweathermap.org/data/2.5/weather?q=quatre+soeurs,mu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 75
    City Number: 12142
    City: vernouillet
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=vernouillet,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 76
    City Number: 7973
    City: hovezi
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=hovezi,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 77
    City Number: 36039
    City: isetskoye
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=isetskoye,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 78
    City Number: 36356
    City: kirovskiy
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=kirovskiy,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 79
    City Number: 42010
    City: rakai
    Country: ug
    http://api.openweathermap.org/data/2.5/weather?q=rakai,ug&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 80
    City Number: 24782
    City: totolac
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=totolac,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 81
    City Number: 19881
    City: esfahan
    Country: ir
    http://api.openweathermap.org/data/2.5/weather?q=esfahan,ir&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 82
    City Number: 17294
    City: bilaspur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=bilaspur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 83
    City Number: 3168
    City: jacarei
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=jacarei,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 84
    City Number: 8583
    City: bestwig
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=bestwig,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 85
    City Number: 27568
    City: bulalacao
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=bulalacao,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 86
    City Number: 8817
    City: fellbach
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=fellbach,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 87
    City Number: 6700
    City: capitanejo
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=capitanejo,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 88
    City Number: 39211
    City: zavety ilicha
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=zavety+ilicha,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 89
    City Number: 33468
    City: magesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=magesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 90
    City Number: 41813
    City: uspenka
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=uspenka,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 91
    City Number: 9835
    City: werdau
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=werdau,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 92
    City Number: 28318
    City: ilihan
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=ilihan,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 93
    City Number: 45899
    City: centreville
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=centreville,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 94
    City Number: 32257
    City: barcea
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=barcea,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 95
    City Number: 6416
    City: xiashi
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=xiashi,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 96
    City Number: 40148
    City: huai mek
    Country: th
    http://api.openweathermap.org/data/2.5/weather?q=huai+mek,th&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 97
    City Number: 20255
    City: casteldaccia
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=casteldaccia,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 98
    City Number: 34788
    City: zarand
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=zarand,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 99
    City Number: 28171
    City: gabi
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=gabi,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 100
    City Number: 37649
    City: pinyug
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=pinyug,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 101
    City Number: 20783
    City: piossasco
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=piossasco,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 102
    City Number: 45086
    City: parma
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=parma,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 103
    City Number: 41636
    City: poshtove
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=poshtove,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 104
    City Number: 42637
    City: broomfield
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=broomfield,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 105
    City Number: 9110
    City: kirchhain
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=kirchhain,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 106
    City Number: 44307
    City: maplewood
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=maplewood,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 107
    City Number: 41873
    City: vysoke
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=vysoke,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 108
    City Number: 38658
    City: tuzha
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=tuzha,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 109
    City Number: 7477
    City: toro
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=toro,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 110
    City Number: 17601
    City: digras
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=digras,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 111
    City Number: 30479
    City: tigbinan
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=tigbinan,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 112
    City Number: 11575
    City: dreux
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=dreux,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 113
    City Number: 24447
    City: san julian
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=san+julian,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 114
    City Number: 45656
    City: friendswood
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=friendswood,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 115
    City Number: 26080
    City: stjordalshalsen
    Country: no
    http://api.openweathermap.org/data/2.5/weather?q=stjordalshalsen,no&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 116
    City Number: 45734
    City: orange
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=orange,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 117
    City Number: 1939
    City: dospat
    Country: bg
    http://api.openweathermap.org/data/2.5/weather?q=dospat,bg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 118
    City Number: 30539
    City: tranca
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=tranca,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 119
    City Number: 7127
    City: ortega
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=ortega,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 120
    City Number: 16337
    City: kertosono
    Country: id
    http://api.openweathermap.org/data/2.5/weather?q=kertosono,id&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 121
    City Number: 17376
    City: chandannagar
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=chandannagar,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 122
    City Number: 33767
    City: pacureti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=pacureti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 123
    City Number: 15153
    City: san juan pueblo
    Country: hn
    http://api.openweathermap.org/data/2.5/weather?q=san+juan+pueblo,hn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 124
    City Number: 7143
    City: palermo
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=palermo,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 125
    City Number: 1066
    City: brcko
    Country: ba
    http://api.openweathermap.org/data/2.5/weather?q=brcko,ba&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 126
    City Number: 32199
    City: baita de sub codru
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=baita+de+sub+codru,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 127
    City Number: 5675
    City: machali
    Country: cl
    http://api.openweathermap.org/data/2.5/weather?q=machali,cl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 128
    City Number: 41448
    City: lopukhiv
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=lopukhiv,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 129
    City Number: 3385
    City: miguel pereira
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=miguel+pereira,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 130
    City Number: 14198
    City: rizomilos
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=rizomilos,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 131
    City Number: 19686
    City: umred
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=umred,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 132
    City Number: 40827
    City: taitung
    Country: tw
    http://api.openweathermap.org/data/2.5/weather?q=taitung,tw&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 133
    City Number: 25571
    City: heythuysen
    Country: nl
    http://api.openweathermap.org/data/2.5/weather?q=heythuysen,nl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 134
    City Number: 25677
    City: soest
    Country: nl
    http://api.openweathermap.org/data/2.5/weather?q=soest,nl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 135
    City Number: 31281
    City: polaniec
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=polaniec,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 136
    City Number: 8760
    City: eilenburg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=eilenburg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 137
    City Number: 46705
    City: umtata
    Country: za
    http://api.openweathermap.org/data/2.5/weather?q=umtata,za&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 138
    City Number: 28011
    City: damulog
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=damulog,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 139
    City Number: 10656
    City: algete
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=algete,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 140
    City Number: 1665
    City: mol
    Country: be
    http://api.openweathermap.org/data/2.5/weather?q=mol,be&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 141
    City Number: 18768
    City: narasimharajapura
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=narasimharajapura,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 142
    City Number: 3586
    City: parnamirim
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=parnamirim,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 143
    City Number: 32933
    City: domnesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=domnesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 144
    City Number: 13791
    City: kontariotissa
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=kontariotissa,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 145
    City Number: 3229
    City: jucurutu
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=jucurutu,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 146
    City Number: 1524
    City: grez-doiceau
    Country: be
    http://api.openweathermap.org/data/2.5/weather?q=grez-doiceau,be&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 147
    City Number: 3700
    City: pompeu
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=pompeu,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 148
    City Number: 12007
    City: saint-etienne
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=saint-etienne,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 149
    City Number: 6247
    City: pingdingshan
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=pingdingshan,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 150
    City Number: 20102
    City: atessa
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=atessa,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 151
    City Number: 40715
    City: tarsus
    Country: tr
    http://api.openweathermap.org/data/2.5/weather?q=tarsus,tr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 152
    City Number: 41752
    City: starokostyantyniv
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=starokostyantyniv,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 153
    City Number: 38379
    City: stolbovaya
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=stolbovaya,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 154
    City Number: 28205
    City: gibgos
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=gibgos,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 155
    City Number: 5555
    City: zurich
    Country: ch
    http://api.openweathermap.org/data/2.5/weather?q=zurich,ch&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 156
    City Number: 30266
    City: sulop
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=sulop,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 157
    City Number: 4587
    City: durham
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=durham,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 158
    City Number: 21998
    City: kilifi
    Country: ke
    http://api.openweathermap.org/data/2.5/weather?q=kilifi,ke&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 159
    City Number: 7787
    City: santa maria
    Country: cv
    http://api.openweathermap.org/data/2.5/weather?q=santa+maria,cv&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 160
    City Number: 21168
    City: port antonio
    Country: jm
    http://api.openweathermap.org/data/2.5/weather?q=port+antonio,jm&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 161
    City Number: 22795
    City: beroroha
    Country: mg
    http://api.openweathermap.org/data/2.5/weather?q=beroroha,mg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 162
    City Number: 26866
    City: punaauia
    Country: pf
    http://api.openweathermap.org/data/2.5/weather?q=punaauia,pf&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 163
    City Number: 44272
    City: bridgeton
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=bridgeton,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 164
    City Number: 6780
    City: corozal
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=corozal,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 165
    City Number: 17649
    City: etah
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=etah,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 166
    City Number: 25225
    City: afikpo
    Country: ng
    http://api.openweathermap.org/data/2.5/weather?q=afikpo,ng&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 167
    City Number: 4364
    City: tamasane
    Country: bw
    http://api.openweathermap.org/data/2.5/weather?q=tamasane,bw&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 168
    City Number: 3204
    City: jequie
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=jequie,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 169
    City Number: 28344
    City: ipil
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=ipil,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 170
    City Number: 46228
    City: asaka
    Country: uz
    http://api.openweathermap.org/data/2.5/weather?q=asaka,uz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 171
    City Number: 37634
    City: petrovskaya
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=petrovskaya,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 172
    City Number: 5291
    City: biel
    Country: ch
    http://api.openweathermap.org/data/2.5/weather?q=biel,ch&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 173
    City Number: 32648
    City: chisindia
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=chisindia,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 174
    City Number: 35939
    City: goyty
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=goyty,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 175
    City Number: 9344
    City: nauen
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=nauen,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 176
    City Number: 31412
    City: wolomin
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=wolomin,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 177
    City Number: 43757
    City: damascus
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=damascus,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 178
    City Number: 15469
    City: csengele
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=csengele,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 179
    City Number: 26276
    City: rakaia
    Country: nz
    http://api.openweathermap.org/data/2.5/weather?q=rakaia,nz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 180
    City Number: 28625
    City: libato
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=libato,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 181
    City Number: 11470
    City: carmaux
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=carmaux,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 182
    City Number: 16473
    City: rembang
    Country: id
    http://api.openweathermap.org/data/2.5/weather?q=rembang,id&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 183
    City Number: 20121
    City: barberino di mugello
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=barberino+di+mugello,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 184
    City Number: 9859
    City: wildberg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=wildberg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 185
    City Number: 28841
    City: magay
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=magay,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 186
    City Number: 34476
    City: teslui
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=teslui,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 187
    City Number: 40258
    City: phuket
    Country: th
    http://api.openweathermap.org/data/2.5/weather?q=phuket,th&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 188
    City Number: 4171
    City: tucano
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=tucano,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 189
    City Number: 38200
    City: slantsy
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=slantsy,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 190
    City Number: 25483
    City: boxmeer
    Country: nl
    http://api.openweathermap.org/data/2.5/weather?q=boxmeer,nl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 191
    City Number: 26811
    City: tambo
    Country: pe
    http://api.openweathermap.org/data/2.5/weather?q=tambo,pe&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 192
    City Number: 5349
    City: gelterkinden
    Country: ch
    http://api.openweathermap.org/data/2.5/weather?q=gelterkinden,ch&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 193
    City Number: 4230
    City: varzea alegre
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=varzea+alegre,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 194
    City Number: 30306
    City: tabuk
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=tabuk,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 195
    City Number: 33236
    City: harseni
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=harseni,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 196
    City Number: 28641
    City: liboran
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=liboran,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 197
    City Number: 38413
    City: suoyarvi
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=suoyarvi,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 198
    City Number: 38543
    City: teya
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=teya,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 199
    City Number: 7362
    City: santa rosa de viterbo
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=santa+rosa+de+viterbo,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 200
    City Number: 19277
    City: samthar
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=samthar,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 201
    City Number: 41064
    City: nguruka
    Country: tz
    http://api.openweathermap.org/data/2.5/weather?q=nguruka,tz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 202
    City Number: 8507
    City: bad krozingen
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=bad+krozingen,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 203
    City Number: 38613
    City: tselina
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=tselina,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 204
    City Number: 31404
    City: wisla
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=wisla,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 205
    City Number: 31267
    City: parczew
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=parczew,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 206
    City Number: 39085
    City: yayva
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=yayva,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 207
    City Number: 2325
    City: amontada
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=amontada,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 208
    City Number: 14471
    City: el tejar
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=el+tejar,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 209
    City Number: 27344
    City: basco
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=basco,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 210
    City Number: 7751
    City: rodas
    Country: cu
    http://api.openweathermap.org/data/2.5/weather?q=rodas,cu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 211
    City Number: 42454
    City: orange
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=orange,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 212
    City Number: 20521
    City: latiano
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=latiano,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 213
    City Number: 1255
    City: zvornik
    Country: ba
    http://api.openweathermap.org/data/2.5/weather?q=zvornik,ba&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 214
    City Number: 31495
    City: arganil
    Country: pt
    http://api.openweathermap.org/data/2.5/weather?q=arganil,pt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 215
    City Number: 46360
    City: punta cardon
    Country: ve
    http://api.openweathermap.org/data/2.5/weather?q=punta+cardon,ve&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 216
    City Number: 10985
    City: puerto lumbreras
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=puerto+lumbreras,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 217
    City Number: 3039
    City: indiaroba
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=indiaroba,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 218
    City Number: 42555
    City: scotts valley
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=scotts+valley,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 219
    City Number: 32862
    City: daneasa
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=daneasa,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 220
    City Number: 2809
    City: cubatao
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=cubatao,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 221
    City Number: 14494
    City: iztapa
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=iztapa,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 222
    City Number: 34225
    City: semlac
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=semlac,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 223
    City Number: 45277
    City: economy
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=economy,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 224
    City Number: 13230
    City: qaanaaq
    Country: gl
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq,gl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 225
    City Number: 32854
    City: daesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=daesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 226
    City Number: 36184
    City: karasuk
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=karasuk,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 227
    City Number: 21907
    City: uozu
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=uozu,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 228
    City Number: 44345
    City: anaconda
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=anaconda,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 229
    City Number: 33057
    City: francesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=francesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 230
    City Number: 24292
    City: penon blanco
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=penon+blanco,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 231
    City Number: 19465
    City: sitarganj
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=sitarganj,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 232
    City Number: 29892
    City: san juan
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=san+juan,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 233
    City Number: 42607
    City: walnut
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=walnut,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 234
    City Number: 10986
    City: puerto real
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=puerto+real,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 235
    City Number: 43949
    City: norwell
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=norwell,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 236
    City Number: 8023
    City: karvina
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=karvina,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 237
    City Number: 26530
    City: rio grande
    Country: pa
    http://api.openweathermap.org/data/2.5/weather?q=rio+grande,pa&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 238
    City Number: 40549
    City: corum
    Country: tr
    http://api.openweathermap.org/data/2.5/weather?q=corum,tr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 239
    City Number: 31696
    City: odivelas
    Country: pt
    http://api.openweathermap.org/data/2.5/weather?q=odivelas,pt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 240
    City Number: 45583
    City: amarillo
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=amarillo,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 241
    City Number: 41669
    City: rozhnyativ
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=rozhnyativ,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 242
    City Number: 31242
    City: nysa
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=nysa,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 243
    City Number: 27094
    City: atop-atop
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=atop-atop,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 244
    City Number: 37184
    City: nerchinsk
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=nerchinsk,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 245
    City Number: 22803
    City: fianarantsoa
    Country: mg
    http://api.openweathermap.org/data/2.5/weather?q=fianarantsoa,mg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 246
    City Number: 37255
    City: nizhnyaya maktama
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=nizhnyaya+maktama,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 247
    City Number: 40917
    City: kibiti
    Country: tz
    http://api.openweathermap.org/data/2.5/weather?q=kibiti,tz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 248
    City Number: 13464
    City: ayia marina
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=ayia+marina,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 249
    City Number: 33859
    City: piscu vechi
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=piscu+vechi,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 250
    City Number: 42286
    City: desert hot springs
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=desert+hot+springs,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 251
    City Number: 17373
    City: champua
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=champua,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 252
    City Number: 43077
    City: fairburn
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=fairburn,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 253
    City Number: 27843
    City: carmen
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=carmen,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 254
    City Number: 4460
    City: berwick
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=berwick,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 255
    City Number: 4045
    City: senges
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=senges,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 256
    City Number: 45544
    City: humboldt
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=humboldt,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 257
    City Number: 42188
    City: alhambra
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=alhambra,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 258
    City Number: 1352
    City: aartselaar
    Country: be
    http://api.openweathermap.org/data/2.5/weather?q=aartselaar,be&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 259
    City Number: 17279
    City: bidhuna
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=bidhuna,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 260
    City Number: 32592
    City: ceahlau
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=ceahlau,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 261
    City Number: 46359
    City: puerto cabello
    Country: ve
    http://api.openweathermap.org/data/2.5/weather?q=puerto+cabello,ve&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 262
    City Number: 38868
    City: verkhniy baskunchak
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=verkhniy+baskunchak,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 263
    City Number: 6168
    City: liuzhou
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=liuzhou,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 264
    City Number: 32214
    City: balcauti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=balcauti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 265
    City Number: 9750
    City: uhingen
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=uhingen,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 266
    City Number: 7644
    City: santa ana
    Country: cr
    http://api.openweathermap.org/data/2.5/weather?q=santa+ana,cr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 267
    City Number: 35603
    City: cherlak
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=cherlak,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 268
    City Number: 23924
    City: ixtapa
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=ixtapa,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 269
    City Number: 38195
    City: skorodnoye
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=skorodnoye,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 270
    City Number: 38146
    City: shiringushi
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=shiringushi,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 271
    City Number: 28958
    City: malusac
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=malusac,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 272
    City Number: 4009
    City: sao paulo do potengi
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=sao+paulo+do+potengi,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 273
    City Number: 25543
    City: groesbeek
    Country: nl
    http://api.openweathermap.org/data/2.5/weather?q=groesbeek,nl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 274
    City Number: 5484
    City: schattdorf
    Country: ch
    http://api.openweathermap.org/data/2.5/weather?q=schattdorf,ch&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 275
    City Number: 4316
    City: kanye
    Country: bw
    http://api.openweathermap.org/data/2.5/weather?q=kanye,bw&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 276
    City Number: 5450
    City: ollon
    Country: ch
    http://api.openweathermap.org/data/2.5/weather?q=ollon,ch&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 277
    City Number: 44554
    City: lakewood
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=lakewood,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 278
    City Number: 26208
    City: gisborne
    Country: nz
    http://api.openweathermap.org/data/2.5/weather?q=gisborne,nz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 279
    City Number: 41560
    City: nyzhni petrivtsi
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=nyzhni+petrivtsi,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 280
    City Number: 38261
    City: sonkovo
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=sonkovo,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 281
    City Number: 42524
    City: san clemente
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=san+clemente,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 282
    City Number: 37980
    City: sapernoye
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=sapernoye,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 283
    City Number: 15335
    City: abadszalok
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=abadszalok,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 284
    City Number: 11569
    City: douai
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=douai,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 285
    City Number: 37946
    City: rzhanitsa
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=rzhanitsa,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 286
    City Number: 32965
    City: dragu
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=dragu,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 287
    City Number: 8802
    City: eschborn
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=eschborn,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 288
    City Number: 30165
    City: sara
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=sara,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 289
    City Number: 44883
    City: burlington
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=burlington,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 290
    City Number: 41107
    City: urambo
    Country: tz
    http://api.openweathermap.org/data/2.5/weather?q=urambo,tz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 291
    City Number: 46558
    City: brandfort
    Country: za
    http://api.openweathermap.org/data/2.5/weather?q=brandfort,za&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 292
    City Number: 39733
    City: boajibu
    Country: sl
    http://api.openweathermap.org/data/2.5/weather?q=boajibu,sl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 293
    City Number: 11837
    City: montbeliard
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=montbeliard,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 294
    City Number: 38461
    City: syumsi
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=syumsi,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 295
    City Number: 4044
    City: sena madureira
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=sena+madureira,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 296
    City Number: 8104
    City: merin
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=merin,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 297
    City Number: 4817
    City: neepawa
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=neepawa,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 298
    City Number: 6278
    City: qufu
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=qufu,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 299
    City Number: 26521
    City: puerto caimito
    Country: pa
    http://api.openweathermap.org/data/2.5/weather?q=puerto+caimito,pa&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 300
    City Number: 43622
    City: chalmette
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=chalmette,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 301
    City Number: 19340
    City: sehore
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=sehore,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 302
    City Number: 12517
    City: exeter
    Country: gb
    http://api.openweathermap.org/data/2.5/weather?q=exeter,gb&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 303
    City Number: 36146
    City: kamensk-shakhtinskiy
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=kamensk-shakhtinskiy,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 304
    City Number: 37437
    City: oktyabrskiy
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=oktyabrskiy,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 305
    City Number: 36531
    City: krasnaya gorka
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=krasnaya+gorka,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 306
    City Number: 29266
    City: nuing
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=nuing,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 307
    City Number: 43299
    City: lake in the hills
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=lake+in+the+hills,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 308
    City Number: 27212
    City: balayong
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=balayong,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 309
    City Number: 24221
    City: ocotitlan
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=ocotitlan,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 310
    City Number: 21409
    City: iwata
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=iwata,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 311
    City Number: 316
    City: mets parni
    Country: am
    http://api.openweathermap.org/data/2.5/weather?q=mets+parni,am&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 312
    City Number: 42095
    City: bullhead city
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=bullhead+city,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 313
    City Number: 3822
    City: rio real
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=rio+real,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 314
    City Number: 31210
    City: miedzyrzec podlaski
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=miedzyrzec+podlaski,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 315
    City Number: 42316
    City: folsom
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=folsom,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 316
    City Number: 42969
    City: pompano beach highlands
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=pompano+beach+highlands,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 317
    City Number: 41286
    City: hayvoron
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=hayvoron,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 318
    City Number: 253
    City: ghukasavan
    Country: am
    http://api.openweathermap.org/data/2.5/weather?q=ghukasavan,am&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 319
    City Number: 46143
    City: richfield
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=richfield,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 320
    City Number: 41225
    City: chervonohryhorivka
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=chervonohryhorivka,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 321
    City Number: 34059
    City: ruginesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=ruginesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 322
    City Number: 7395
    City: sitionuevo
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=sitionuevo,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 323
    City Number: 8075
    City: letovice
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=letovice,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 324
    City Number: 22531
    City: kayl
    Country: lu
    http://api.openweathermap.org/data/2.5/weather?q=kayl,lu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 325
    City Number: 27330
    City: barongis
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=barongis,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 326
    City Number: 18472
    City: maharajganj
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=maharajganj,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 327
    City Number: 10220
    City: la plaine
    Country: dm
    http://api.openweathermap.org/data/2.5/weather?q=la+plaine,dm&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 328
    City Number: 17084
    City: bamora
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=bamora,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 329
    City Number: 10777
    City: coria del rio
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=coria+del+rio,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 330
    City Number: 27895
    City: cawayan
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=cawayan,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 331
    City Number: 7349
    City: santa catalina
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=santa+catalina,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 332
    City Number: 21623
    City: nakanojo
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=nakanojo,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 333
    City Number: 35548
    City: bykovo
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=bykovo,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 334
    City Number: 14966
    City: laguna verde
    Country: hn
    http://api.openweathermap.org/data/2.5/weather?q=laguna+verde,hn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 335
    City Number: 31344
    City: stargard szczecinski
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=stargard+szczecinski,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 336
    City Number: 9488
    City: radeberg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=radeberg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 337
    City Number: 46423
    City: lang son
    Country: vn
    http://api.openweathermap.org/data/2.5/weather?q=lang+son,vn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 338
    City Number: 34376
    City: studina
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=studina,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 339
    City Number: 40067
    City: amlame
    Country: tg
    http://api.openweathermap.org/data/2.5/weather?q=amlame,tg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 340
    City Number: 10300
    City: arenillas
    Country: ec
    http://api.openweathermap.org/data/2.5/weather?q=arenillas,ec&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 341
    City Number: 18202
    City: kesinga
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=kesinga,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 342
    City Number: 42811
    City: coral terrace
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=coral+terrace,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 343
    City Number: 29577
    City: puerto galera
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=puerto+galera,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 344
    City Number: 44293
    City: independence
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=independence,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 345
    City Number: 30855
    City: kunri
    Country: pk
    http://api.openweathermap.org/data/2.5/weather?q=kunri,pk&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 346
    City Number: 35605
    City: chermoz
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=chermoz,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 347
    City Number: 43529
    City: urbandale
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=urbandale,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 348
    City Number: 6710
    City: cartagena
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=cartagena,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 349
    City Number: 31786
    City: santo antonio da charneca
    Country: pt
    http://api.openweathermap.org/data/2.5/weather?q=santo+antonio+da+charneca,pt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 350
    City Number: 37491
    City: orichi
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=orichi,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 351
    City Number: 46306
    City: cantaura
    Country: ve
    http://api.openweathermap.org/data/2.5/weather?q=cantaura,ve&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 352
    City Number: 1148
    City: malesici
    Country: ba
    http://api.openweathermap.org/data/2.5/weather?q=malesici,ba&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 353
    City Number: 16564
    City: waru
    Country: id
    http://api.openweathermap.org/data/2.5/weather?q=waru,id&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 354
    City Number: 39106
    City: yelizavetinskaya
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=yelizavetinskaya,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 355
    City Number: 3718
    City: porto da folha
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=porto+da+folha,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 356
    City Number: 20727
    City: osimo
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=osimo,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 357
    City Number: 11886
    City: notre-dame-de-gravenchon
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=notre-dame-de-gravenchon,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 358
    City Number: 14538
    City: pachalum
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=pachalum,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 359
    City Number: 29719
    City: salvacion
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=salvacion,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 360
    City Number: 22986
    City: falam
    Country: mm
    http://api.openweathermap.org/data/2.5/weather?q=falam,mm&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 361
    City Number: 46029
    City: opportunity
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=opportunity,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 362
    City Number: 3280
    City: lins
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=lins,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 363
    City Number: 21859
    City: togitsu
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=togitsu,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 364
    City Number: 42875
    City: kendall
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=kendall,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 365
    City Number: 38188
    City: sivaki
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=sivaki,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 366
    City Number: 38843
    City: velikiy novgorod
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=velikiy+novgorod,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 367
    City Number: 45199
    City: baker city
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=baker+city,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 368
    City Number: 23185
    City: midlands
    Country: mu
    http://api.openweathermap.org/data/2.5/weather?q=midlands,mu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 369
    City Number: 21501
    City: kodama
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=kodama,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 370
    City Number: 24900
    City: yaonahuac
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=yaonahuac,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 371
    City Number: 16796
    City: ramat hasharon
    Country: il
    http://api.openweathermap.org/data/2.5/weather?q=ramat+hasharon,il&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 372
    City Number: 23885
    City: huichapan
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=huichapan,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 373
    City Number: 23853
    City: hostotipaquillo
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=hostotipaquillo,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 374
    City Number: 44643
    City: west caldwell
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=west+caldwell,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 375
    City Number: 20457
    City: gavardo
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=gavardo,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 376
    City Number: 24001
    City: la calera
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=la+calera,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 377
    City Number: 2982
    City: hidrolandia
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=hidrolandia,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 378
    City Number: 40214
    City: nong han
    Country: th
    http://api.openweathermap.org/data/2.5/weather?q=nong+han,th&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 379
    City Number: 4496
    City: campbellford
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=campbellford,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 380
    City Number: 41491
    City: medenychi
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=medenychi,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 381
    City Number: 8682
    City: coburg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=coburg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 382
    City Number: 40041
    City: bokoro
    Country: td
    http://api.openweathermap.org/data/2.5/weather?q=bokoro,td&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 383
    City Number: 25203
    City: madarounfa
    Country: ne
    http://api.openweathermap.org/data/2.5/weather?q=madarounfa,ne&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 384
    City Number: 15570
    City: galgamacsa
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=galgamacsa,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 385
    City Number: 16075
    City: tiszaalpar
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=tiszaalpar,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 386
    City Number: 18382
    City: kurara
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=kurara,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 387
    City Number: 9484
    City: quedlinburg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=quedlinburg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 388
    City Number: 13873
    City: loutros
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=loutros,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 389
    City Number: 14518
    City: mazatenango
    Country: gt
    http://api.openweathermap.org/data/2.5/weather?q=mazatenango,gt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 390
    City Number: 16758
    City: iksal
    Country: il
    http://api.openweathermap.org/data/2.5/weather?q=iksal,il&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 391
    City Number: 13724
    City: keratea
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=keratea,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 392
    City Number: 23511
    City: canatlan
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=canatlan,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 393
    City Number: 44412
    City: chester
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=chester,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 394
    City Number: 9810
    City: wasserburg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=wasserburg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 395
    City Number: 4564
    City: danville
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=danville,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 396
    City Number: 33912
    City: pomezeu
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=pomezeu,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 397
    City Number: 42376
    City: laguna hills
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=laguna+hills,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 398
    City Number: 34012
    City: rediu
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=rediu,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 399
    City Number: 37468
    City: olonets
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=olonets,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 400
    City Number: 18770
    City: narauli
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=narauli,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 401
    City Number: 18049
    City: kadaura
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=kadaura,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 402
    City Number: 33217
    City: gura sutii
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=gura+sutii,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 403
    City Number: 33899
    City: poiana stampei
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=poiana+stampei,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 404
    City Number: 8884
    City: gemunden
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=gemunden,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 405
    City Number: 9700
    City: sulzbach-rosenberg
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=sulzbach-rosenberg,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 406
    City Number: 46144
    City: river falls
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=river+falls,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 407
    City Number: 442
    City: caconda
    Country: ao
    http://api.openweathermap.org/data/2.5/weather?q=caconda,ao&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 408
    City Number: 27934
    City: concepcion
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=concepcion,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 409
    City Number: 40176
    City: kui buri
    Country: th
    http://api.openweathermap.org/data/2.5/weather?q=kui+buri,th&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 410
    City Number: 46655
    City: parys
    Country: za
    http://api.openweathermap.org/data/2.5/weather?q=parys,za&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 411
    City Number: 46345
    City: los teques
    Country: ve
    http://api.openweathermap.org/data/2.5/weather?q=los+teques,ve&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 412
    City Number: 14195
    City: rizia
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=rizia,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 413
    City Number: 10818
    City: gibraleon
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=gibraleon,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 414
    City Number: 25103
    City: inhambane
    Country: mz
    http://api.openweathermap.org/data/2.5/weather?q=inhambane,mz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 415
    City Number: 44135
    City: bemidji
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=bemidji,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 416
    City Number: 10755
    City: cartama
    Country: es
    http://api.openweathermap.org/data/2.5/weather?q=cartama,es&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 417
    City Number: 46420
    City: hue
    Country: vn
    http://api.openweathermap.org/data/2.5/weather?q=hue,vn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 418
    City Number: 33062
    City: fratautii vechi
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=fratautii+vechi,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 419
    City Number: 35331
    City: belaya gora
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=belaya+gora,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 420
    City Number: 34051
    City: rosiori de vede
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=rosiori+de+vede,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 421
    City Number: 611
    City: gleisdorf
    Country: at
    http://api.openweathermap.org/data/2.5/weather?q=gleisdorf,at&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 422
    City Number: 33423
    City: lovrin
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=lovrin,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 423
    City Number: 20782
    City: piombino
    Country: it
    http://api.openweathermap.org/data/2.5/weather?q=piombino,it&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 424
    City Number: 37816
    City: psedakh
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=psedakh,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 425
    City Number: 9367
    City: neustadt
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=neustadt,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 426
    City Number: 26365
    City: boquete
    Country: pa
    http://api.openweathermap.org/data/2.5/weather?q=boquete,pa&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 427
    City Number: 37067
    City: mokrousovo
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=mokrousovo,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 428
    City Number: 41850
    City: vladyslavivka
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=vladyslavivka,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 429
    City Number: 2414
    City: autazes
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=autazes,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 430
    City Number: 32090
    City: albesti
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=albesti,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 431
    City Number: 13279
    City: mandiana
    Country: gn
    http://api.openweathermap.org/data/2.5/weather?q=mandiana,gn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 432
    City Number: 4288
    City: mongar
    Country: bt
    http://api.openweathermap.org/data/2.5/weather?q=mongar,bt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 433
    City Number: 4457
    City: belleville
    Country: ca
    http://api.openweathermap.org/data/2.5/weather?q=belleville,ca&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 434
    City Number: 16766
    City: kefar habad
    Country: il
    http://api.openweathermap.org/data/2.5/weather?q=kefar+habad,il&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 435
    City Number: 7274
    City: salento
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=salento,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 436
    City Number: 3637
    City: piacabucu
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=piacabucu,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 437
    City Number: 2448
    City: barra velha
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=barra+velha,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 438
    City Number: 24607
    City: telixtac
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=telixtac,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 439
    City Number: 18571
    City: mankapur
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=mankapur,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 440
    City Number: 38106
    City: shaygino
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=shaygino,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 441
    City Number: 3133
    City: itaqui
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=itaqui,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 442
    City Number: 19250
    City: sahawar
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=sahawar,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 443
    City Number: 18764
    City: naraini
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=naraini,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 444
    City Number: 7535
    City: villarrica
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=villarrica,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 445
    City Number: 2563
    City: cacapava do sul
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=cacapava+do+sul,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 446
    City Number: 1158
    City: nevesinje
    Country: ba
    http://api.openweathermap.org/data/2.5/weather?q=nevesinje,ba&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 447
    City Number: 31247
    City: olesno
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=olesno,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 448
    City Number: 38862
    City: verkhnevilyuysk
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=verkhnevilyuysk,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 449
    City Number: 44517
    City: edgewater
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=edgewater,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 450
    City Number: 2489
    City: bicas
    Country: br
    http://api.openweathermap.org/data/2.5/weather?q=bicas,br&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 451
    City Number: 31377
    City: tarnow
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=tarnow,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 452
    City Number: 18610
    City: mayakonda
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=mayakonda,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 453
    City Number: 35241
    City: aysha
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=aysha,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 454
    City Number: 43208
    City: bloomington
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=bloomington,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 455
    City Number: 1041
    City: xudat
    Country: az
    http://api.openweathermap.org/data/2.5/weather?q=xudat,az&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 456
    City Number: 2077
    City: tervel
    Country: bg
    http://api.openweathermap.org/data/2.5/weather?q=tervel,bg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 457
    City Number: 26344
    City: agua buena
    Country: pa
    http://api.openweathermap.org/data/2.5/weather?q=agua+buena,pa&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 458
    City Number: 33994
    City: rastolita
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=rastolita,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 459
    City Number: 35555
    City: chadan
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=chadan,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 460
    City Number: 41978
    City: koboko
    Country: ug
    http://api.openweathermap.org/data/2.5/weather?q=koboko,ug&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 461
    City Number: 11539
    City: coudekerque-branche
    Country: fr
    http://api.openweathermap.org/data/2.5/weather?q=coudekerque-branche,fr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 462
    City Number: 16022
    City: szentlorinckata
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=szentlorinckata,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 463
    City Number: 1915
    City: blagoevgrad
    Country: bg
    http://api.openweathermap.org/data/2.5/weather?q=blagoevgrad,bg&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 464
    City Number: 15410
    City: bekescsaba
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=bekescsaba,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 465
    City Number: 10454
    City: klooga
    Country: ee
    http://api.openweathermap.org/data/2.5/weather?q=klooga,ee&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 466
    City Number: 42193
    City: american canyon
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=american+canyon,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 467
    City Number: 29563
    City: port barton
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=port+barton,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 468
    City Number: 14142
    City: platanos
    Country: gr
    http://api.openweathermap.org/data/2.5/weather?q=platanos,gr&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 469
    City Number: 6432
    City: xintai
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=xintai,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 470
    City Number: 33250
    City: hlipiceni
    Country: ro
    http://api.openweathermap.org/data/2.5/weather?q=hlipiceni,ro&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 471
    City Number: 14777
    City: balsamo oriental
    Country: hn
    http://api.openweathermap.org/data/2.5/weather?q=balsamo+oriental,hn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 472
    City Number: 19193
    City: raxaul
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=raxaul,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 473
    City Number: 1
    City: canillo
    Country: ad
    http://api.openweathermap.org/data/2.5/weather?q=canillo,ad&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 474
    City Number: 31632
    City: lagos
    Country: pt
    http://api.openweathermap.org/data/2.5/weather?q=lagos,pt&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 475
    City Number: 36596
    City: krasnoye
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=krasnoye,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 476
    City Number: 27794
    City: caningay
    Country: ph
    http://api.openweathermap.org/data/2.5/weather?q=caningay,ph&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 477
    City Number: 8293
    City: steti
    Country: cz
    http://api.openweathermap.org/data/2.5/weather?q=steti,cz&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 478
    City Number: 9843
    City: wertheim
    Country: de
    http://api.openweathermap.org/data/2.5/weather?q=wertheim,de&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 479
    City Number: 22318
    City: monaragala
    Country: lk
    http://api.openweathermap.org/data/2.5/weather?q=monaragala,lk&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 480
    City Number: 19008
    City: phaphund
    Country: in
    http://api.openweathermap.org/data/2.5/weather?q=phaphund,in&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 481
    City Number: 23312
    City: ahuacatlan
    Country: mx
    http://api.openweathermap.org/data/2.5/weather?q=ahuacatlan,mx&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 482
    City Number: 6509
    City: yushan
    Country: cn
    http://api.openweathermap.org/data/2.5/weather?q=yushan,cn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 483
    City Number: 42517
    City: rubidoux
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=rubidoux,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 484
    City Number: 229
    City: dashtavan
    Country: am
    http://api.openweathermap.org/data/2.5/weather?q=dashtavan,am&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 485
    City Number: 16028
    City: szigetszentmiklos
    Country: hu
    http://api.openweathermap.org/data/2.5/weather?q=szigetszentmiklos,hu&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 486
    City Number: 21909
    City: urayasu
    Country: jp
    http://api.openweathermap.org/data/2.5/weather?q=urayasu,jp&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 487
    City Number: 46339
    City: la fria
    Country: ve
    http://api.openweathermap.org/data/2.5/weather?q=la+fria,ve&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 488
    City Number: 38961
    City: volokolamsk
    Country: ru
    http://api.openweathermap.org/data/2.5/weather?q=volokolamsk,ru&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 489
    City Number: 7282
    City: san andres
    Country: co
    http://api.openweathermap.org/data/2.5/weather?q=san+andres,co&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 490
    City Number: 141
    City: vore
    Country: al
    http://api.openweathermap.org/data/2.5/weather?q=vore,al&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 491
    City Number: 45403
    City: salinas
    Country: us
    http://api.openweathermap.org/data/2.5/weather?q=salinas,us&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 492
    City Number: 41315
    City: ispas
    Country: ua
    http://api.openweathermap.org/data/2.5/weather?q=ispas,ua&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 493
    City Number: 31069
    City: czechowice-dziedzice
    Country: pl
    http://api.openweathermap.org/data/2.5/weather?q=czechowice-dziedzice,pl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 494
    City Number: 16573
    City: wonosari
    Country: id
    http://api.openweathermap.org/data/2.5/weather?q=wonosari,id&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 495
    City Number: 5631
    City: bulnes
    Country: cl
    http://api.openweathermap.org/data/2.5/weather?q=bulnes,cl&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    ----------------------------
    Retreiving City #: 496
    City Number: 46410
    City: ha giang
    Country: vn
    http://api.openweathermap.org/data/2.5/weather?q=ha+giang,vn&units=IMPERIAL&mode=json&APPID=e5760248211a864fbc4f4418cc6d872d
    




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
      <th>index</th>
      <th>Country</th>
      <th>City</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>43594</td>
      <td>us</td>
      <td>lexington-fayette</td>
      <td>38.049722</td>
      <td>-84.458611</td>
      <td>29.57</td>
      <td>74</td>
      <td>1</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3727</td>
      <td>br</td>
      <td>porto real</td>
      <td>-22.417200</td>
      <td>-44.286100</td>
      <td>61.94</td>
      <td>100</td>
      <td>100</td>
      <td>2.51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>42803</td>
      <td>us</td>
      <td>clermont</td>
      <td>28.549167</td>
      <td>-81.773056</td>
      <td>64.2</td>
      <td>100</td>
      <td>90</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45740</td>
      <td>us</td>
      <td>pecan grove</td>
      <td>29.625833</td>
      <td>-95.731389</td>
      <td>42.8</td>
      <td>81</td>
      <td>90</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>4</th>
      <td>44404</td>
      <td>us</td>
      <td>barnstead</td>
      <td>43.333889</td>
      <td>-71.293333</td>
      <td>29.98</td>
      <td>63</td>
      <td>1</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25835</td>
      <td>no</td>
      <td>flateby</td>
      <td>59.833333</td>
      <td>11.166667</td>
      <td>46.4</td>
      <td>93</td>
      <td>92</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17403</td>
      <td>in</td>
      <td>chatsu</td>
      <td>26.600000</td>
      <td>75.950000</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>7</th>
      <td>30124</td>
      <td>ph</td>
      <td>santo nino</td>
      <td>13.701800</td>
      <td>121.094900</td>
      <td>84.31</td>
      <td>82</td>
      <td>20</td>
      <td>1.72</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18193</td>
      <td>in</td>
      <td>kelamangalam</td>
      <td>12.600000</td>
      <td>77.850000</td>
      <td>79.75</td>
      <td>61</td>
      <td>40</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>9</th>
      <td>41131</td>
      <td>ua</td>
      <td>auly</td>
      <td>48.527081</td>
      <td>34.494931</td>
      <td>32</td>
      <td>100</td>
      <td>75</td>
      <td>11.18</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19069</td>
      <td>in</td>
      <td>puranpur</td>
      <td>28.516667</td>
      <td>80.150000</td>
      <td>74.54</td>
      <td>75</td>
      <td>8</td>
      <td>3.74</td>
    </tr>
    <tr>
      <th>11</th>
      <td>28009</td>
      <td>ph</td>
      <td>damortis</td>
      <td>16.242300</td>
      <td>120.405100</td>
      <td>79.81</td>
      <td>86</td>
      <td>76</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>12</th>
      <td>39987</td>
      <td>sv</td>
      <td>tenancingo</td>
      <td>13.833333</td>
      <td>-88.983333</td>
      <td>73.4</td>
      <td>78</td>
      <td>0</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14405</td>
      <td>gr</td>
      <td>ziparion</td>
      <td>36.875000</td>
      <td>27.204167</td>
      <td>41.11</td>
      <td>49</td>
      <td>20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>14</th>
      <td>17434</td>
      <td>in</td>
      <td>chikmagalur</td>
      <td>13.316667</td>
      <td>75.783333</td>
      <td>79.22</td>
      <td>65</td>
      <td>76</td>
      <td>2.62</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8673</td>
      <td>de</td>
      <td>calbe</td>
      <td>51.900000</td>
      <td>11.766667</td>
      <td>39.2</td>
      <td>91</td>
      <td>40</td>
      <td>17.22</td>
    </tr>
    <tr>
      <th>16</th>
      <td>540</td>
      <td>ar</td>
      <td>san vicente</td>
      <td>-34.982645</td>
      <td>-58.376169</td>
      <td>69.95</td>
      <td>95</td>
      <td>12</td>
      <td>2.06</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18476</td>
      <td>in</td>
      <td>mahbubnagar</td>
      <td>16.733333</td>
      <td>77.983333</td>
      <td>82.37</td>
      <td>55</td>
      <td>20</td>
      <td>4.29</td>
    </tr>
    <tr>
      <th>18</th>
      <td>15130</td>
      <td>hn</td>
      <td>san francisco de yojoa</td>
      <td>15.016667</td>
      <td>-87.966667</td>
      <td>75.2</td>
      <td>100</td>
      <td>40</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>19</th>
      <td>9144</td>
      <td>de</td>
      <td>kronberg</td>
      <td>50.183333</td>
      <td>8.500000</td>
      <td>33.8</td>
      <td>99</td>
      <td>90</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>20</th>
      <td>164</td>
      <td>am</td>
      <td>arapi</td>
      <td>40.779722</td>
      <td>43.800556</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>21</th>
      <td>36747</td>
      <td>ru</td>
      <td>kysyl-syr</td>
      <td>63.898611</td>
      <td>122.761667</td>
      <td>-26.62</td>
      <td>41</td>
      <td>44</td>
      <td>10.89</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23395</td>
      <td>mx</td>
      <td>armeria</td>
      <td>18.915278</td>
      <td>-103.969444</td>
      <td>60.59</td>
      <td>92</td>
      <td>0</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>23</th>
      <td>17323</td>
      <td>in</td>
      <td>bodinayakkanur</td>
      <td>10.016667</td>
      <td>77.350000</td>
      <td>75.76</td>
      <td>74</td>
      <td>24</td>
      <td>1.95</td>
    </tr>
    <tr>
      <th>24</th>
      <td>21650</td>
      <td>jp</td>
      <td>ninomiya</td>
      <td>35.303333</td>
      <td>139.253333</td>
      <td>52.88</td>
      <td>40</td>
      <td>20</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>25</th>
      <td>41193</td>
      <td>ua</td>
      <td>borzna</td>
      <td>51.254645</td>
      <td>32.426901</td>
      <td>22.34</td>
      <td>87</td>
      <td>44</td>
      <td>8.21</td>
    </tr>
    <tr>
      <th>26</th>
      <td>21971</td>
      <td>ke</td>
      <td>butere</td>
      <td>0.209444</td>
      <td>34.492778</td>
      <td>69.8</td>
      <td>83</td>
      <td>75</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>27</th>
      <td>41115</td>
      <td>tz</td>
      <td>uyovu</td>
      <td>-3.283333</td>
      <td>31.525833</td>
      <td>67.79</td>
      <td>92</td>
      <td>44</td>
      <td>4.63</td>
    </tr>
    <tr>
      <th>28</th>
      <td>18676</td>
      <td>in</td>
      <td>mundgod</td>
      <td>14.966667</td>
      <td>75.033333</td>
      <td>78.82</td>
      <td>78</td>
      <td>12</td>
      <td>3.85</td>
    </tr>
    <tr>
      <th>29</th>
      <td>8492</td>
      <td>de</td>
      <td>bad durkheim</td>
      <td>49.468611</td>
      <td>8.166389</td>
      <td>33.8</td>
      <td>98</td>
      <td>20</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>520</th>
      <td>1</td>
      <td>ad</td>
      <td>canillo</td>
      <td>42.566667</td>
      <td>1.600000</td>
      <td>19.1</td>
      <td>53</td>
      <td>0</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>521</th>
      <td>14156</td>
      <td>gr</td>
      <td>poliplatanos</td>
      <td>40.682500</td>
      <td>22.191389</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>522</th>
      <td>31632</td>
      <td>pt</td>
      <td>lagos</td>
      <td>37.101782</td>
      <td>-8.674242</td>
      <td>48.2</td>
      <td>66</td>
      <td>0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>523</th>
      <td>36596</td>
      <td>ru</td>
      <td>krasnoye</td>
      <td>52.729500</td>
      <td>39.162900</td>
      <td>23.47</td>
      <td>92</td>
      <td>80</td>
      <td>16.26</td>
    </tr>
    <tr>
      <th>524</th>
      <td>27794</td>
      <td>ph</td>
      <td>caningay</td>
      <td>9.829700</td>
      <td>122.644200</td>
      <td>83.86</td>
      <td>98</td>
      <td>32</td>
      <td>0.6</td>
    </tr>
    <tr>
      <th>525</th>
      <td>8293</td>
      <td>cz</td>
      <td>steti</td>
      <td>50.453141</td>
      <td>14.378383</td>
      <td>35.6</td>
      <td>74</td>
      <td>90</td>
      <td>12.75</td>
    </tr>
    <tr>
      <th>526</th>
      <td>9843</td>
      <td>de</td>
      <td>wertheim</td>
      <td>49.757500</td>
      <td>9.509444</td>
      <td>30.2</td>
      <td>92</td>
      <td>40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>527</th>
      <td>22318</td>
      <td>lk</td>
      <td>monaragala</td>
      <td>6.866667</td>
      <td>81.350000</td>
      <td>82.87</td>
      <td>89</td>
      <td>36</td>
      <td>2.17</td>
    </tr>
    <tr>
      <th>528</th>
      <td>19008</td>
      <td>in</td>
      <td>phaphund</td>
      <td>26.600000</td>
      <td>79.466667</td>
      <td>75.67</td>
      <td>52</td>
      <td>20</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>529</th>
      <td>16456</td>
      <td>id</td>
      <td>prambanan</td>
      <td>-7.750000</td>
      <td>110.494167</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>530</th>
      <td>23312</td>
      <td>mx</td>
      <td>ahuacatlan</td>
      <td>21.050000</td>
      <td>-104.483333</td>
      <td>52.67</td>
      <td>95</td>
      <td>8</td>
      <td>1.05</td>
    </tr>
    <tr>
      <th>531</th>
      <td>6509</td>
      <td>cn</td>
      <td>yushan</td>
      <td>31.377623</td>
      <td>120.954305</td>
      <td>50</td>
      <td>46</td>
      <td>64</td>
      <td>8.95</td>
    </tr>
    <tr>
      <th>532</th>
      <td>38381</td>
      <td>ru</td>
      <td>stoyba</td>
      <td>52.800000</td>
      <td>131.700000</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>533</th>
      <td>46499</td>
      <td>ws</td>
      <td>sapapalii</td>
      <td>-13.683333</td>
      <td>-172.116667</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>534</th>
      <td>42517</td>
      <td>us</td>
      <td>rubidoux</td>
      <td>33.996111</td>
      <td>-117.404722</td>
      <td>62.96</td>
      <td>13</td>
      <td>1</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>535</th>
      <td>229</td>
      <td>am</td>
      <td>dashtavan</td>
      <td>40.101667</td>
      <td>44.390556</td>
      <td>32</td>
      <td>89</td>
      <td>75</td>
      <td>2.73</td>
    </tr>
    <tr>
      <th>536</th>
      <td>16028</td>
      <td>hu</td>
      <td>szigetszentmiklos</td>
      <td>47.343819</td>
      <td>19.043351</td>
      <td>32</td>
      <td>88</td>
      <td>0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>537</th>
      <td>21909</td>
      <td>jp</td>
      <td>urayasu</td>
      <td>35.663338</td>
      <td>139.908548</td>
      <td>52.52</td>
      <td>50</td>
      <td>20</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>538</th>
      <td>46339</td>
      <td>ve</td>
      <td>la fria</td>
      <td>8.218889</td>
      <td>-72.248333</td>
      <td>77</td>
      <td>88</td>
      <td>40</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>539</th>
      <td>13021</td>
      <td>gb</td>
      <td>walkerburn</td>
      <td>55.633333</td>
      <td>-3.016667</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>540</th>
      <td>38961</td>
      <td>ru</td>
      <td>volokolamsk</td>
      <td>56.038968</td>
      <td>35.957021</td>
      <td>21.67</td>
      <td>92</td>
      <td>68</td>
      <td>10</td>
    </tr>
    <tr>
      <th>541</th>
      <td>34930</td>
      <td>rs</td>
      <td>mali zvornik</td>
      <td>44.395278</td>
      <td>19.115833</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>542</th>
      <td>7282</td>
      <td>co</td>
      <td>san andres</td>
      <td>6.903333</td>
      <td>-75.682500</td>
      <td>82.4</td>
      <td>88</td>
      <td>90</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>543</th>
      <td>141</td>
      <td>al</td>
      <td>vore</td>
      <td>41.390833</td>
      <td>19.655000</td>
      <td>32</td>
      <td>100</td>
      <td>0</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>544</th>
      <td>45403</td>
      <td>us</td>
      <td>salinas</td>
      <td>17.979444</td>
      <td>-66.298333</td>
      <td>46.76</td>
      <td>34</td>
      <td>1</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>545</th>
      <td>41315</td>
      <td>ua</td>
      <td>ispas</td>
      <td>48.297342</td>
      <td>25.274064</td>
      <td>42.8</td>
      <td>92</td>
      <td>90</td>
      <td>8.95</td>
    </tr>
    <tr>
      <th>546</th>
      <td>31069</td>
      <td>pl</td>
      <td>czechowice-dziedzice</td>
      <td>49.913416</td>
      <td>19.004789</td>
      <td>37.4</td>
      <td>88</td>
      <td>90</td>
      <td>16.11</td>
    </tr>
    <tr>
      <th>547</th>
      <td>16573</td>
      <td>id</td>
      <td>wonosari</td>
      <td>-7.306111</td>
      <td>110.773889</td>
      <td>86.02</td>
      <td>80</td>
      <td>24</td>
      <td>7.54</td>
    </tr>
    <tr>
      <th>548</th>
      <td>5631</td>
      <td>cl</td>
      <td>bulnes</td>
      <td>-36.733333</td>
      <td>-72.300000</td>
      <td>53.42</td>
      <td>93</td>
      <td>0</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>549</th>
      <td>46410</td>
      <td>vn</td>
      <td>ha giang</td>
      <td>22.833333</td>
      <td>104.983333</td>
      <td>58.39</td>
      <td>99</td>
      <td>92</td>
      <td>1.95</td>
    </tr>
  </tbody>
</table>
<p>550 rows × 9 columns</p>
</div>




```python
randomcitiesDF["Latitude"] = pd.to_numeric(randomcitiesDF["Latitude"])
randomcitiesDF["Longitude"] = pd.to_numeric(randomcitiesDF["Longitude"])
randomcitiesDF["Temperature"] = pd.to_numeric(randomcitiesDF["Temperature"])
randomcitiesDF["Humidity"] = pd.to_numeric(randomcitiesDF["Humidity"])
randomcitiesDF["Cloudiness"] = pd.to_numeric(randomcitiesDF["Cloudiness"])
randomcitiesDF["Wind Speed"] = pd.to_numeric(randomcitiesDF["Wind Speed"])

randomcitiesDF.to_csv("FinalWeather.csv", encoding = "utf-8", index=False)
```


```python
# temperature (F) vs. Latitude
# plt.scatter(randomcitiesDF["Latitude"], randomcitiesDF["Temperature"], marker = "o")
sns.lmplot(x = 'Latitude', y = 'Temperature', data = randomcitiesDF, fit_reg= False, size = 7.5)
plt.title("Temperature (F) vs. Latitude")
plt.ylabel("Temperature (F)")
plt.grid()
plt.savefig("temp_v_lat.png")


plt.show()
```


![png](output_6_0.png)



```python
# humidity (%) vs. Latitude
sns.lmplot(x = 'Latitude', y = 'Humidity', data = randomcitiesDF, fit_reg= False, size = 7.5)
plt.title("Humidity (%) vs. Latitude")
plt.ylabel("Humidity (%)")
plt.grid()
plt.savefig("humidity_v_lat.png")

plt.show()
```


![png](output_7_0.png)



```python
# cloudiness (%) vs Latitude

sns.lmplot(x = 'Latitude', y = 'Cloudiness', data = randomcitiesDF, fit_reg= False, size = 7.5)
plt.title("Cloudiness (%) vs. Latitude")
plt.ylabel("Cloudiness (%)")
plt.grid()
plt.savefig("cloudiness_v_lat.png")


plt.show()
```


![png](output_8_0.png)



```python
# Latitdue vs Longitdue Bubble Plot with Cloudiness
cloudinessPlot = plt.scatter(x = randomcitiesDF["Longitude"], y = randomcitiesDF["Latitude"], s = randomcitiesDF["Cloudiness"]*5, color = "blue", alpha = 0.5, edgecolor = "black", label = "Cloudiness", )
plt.title("Lat vs Long Bubble Plot Cloudiness")
plt.ylabel("Latitude")
plt.xlabel("Longitude")
plt.Figure = [7,7]
plt.grid()
plt.savefig("cloudiness_bubble.png")


plt.show()
```


![png](output_9_0.png)



```python
# wind speed (mph) vs Latitude
sns.lmplot(x = 'Latitude', y = 'Wind Speed', data = randomcitiesDF, fit_reg= True, size = 7.5)
plt.title("Wind Speed (mph) vs. Latitude")
plt.ylabel("Wind Speed (mph)")
plt.grid()
plt.savefig("wind_v_lat.png")


plt.show()
```


![png](output_10_0.png)


### Observable Trends
* The closer to 0 latitude the higher the temperature. Per the Temp vs Lat graph, we can see a clear trend that anything from -20 to 20 lat is above 60F. What's interesting is that when you hit 40 latitude or greater the temperature dips below to 40 degrees or lower but at -40 latitude it is still in the 60+ range.


* Humidity is at it's highest point of 80 - 100% at 0 to 20 latitude and 40 to 60 latitude.


* For the cloudiness vs latitude, there are clumps of 0% and 100% but no clear correlation to the latitude. I decided to create a bubble plot for lat vs longitde with the cloudiness being the size. From here there is a clearer correlation of cloudiness size and % with a large cluster of cloudiness from 0 to 50 longitude and 40 to 60 latitude. This trend can also be seen at -50 to -100 longitude.


* For Wind Speed, we can see that the higher the Latitude, the wind speed tends to pick up to a greater speed. There is an upward trend for wind speed as the Latitude is greater.
