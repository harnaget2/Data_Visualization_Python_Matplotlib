

```python
import csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
#import plotly.plotly as py
```


```python
csv_1 = pd.read_csv("city_data.csv")
csv_2 = pd.read_csv("ride_data.csv")
```


```python
city_groups = csv_2.groupby("city").sum()
num_cities = len(csv_2['city'].unique())

city_groups_2 = csv_2.groupby("city").count()
city_groups["Num Riders"] = city_groups_2["fare"]
city_groups["Average Fare"] = (city_groups["fare"]/city_groups["Num Riders"])
#city_groups.index = range(len(city_groups.index))
merge_1 = csv_1.set_index("city")
merge_1
merged_cities = city_groups.merge(merge_1, how='outer', left_index=True, right_index=True)
merged_cities["color"] = "Light Sky Blue"
merged_cities["color"][merged_cities["type"] == "Urban"] = "lightcoral"
merged_cities["color"][merged_cities["type"] == "Suburban"] = "lightskyblue"
merged_cities["color"][merged_cities["type"] == "Rural"] = "gold"
merged_cities
```

    C:\Users\harna\Anaconda3\envs\PythonData\lib\site-packages\ipykernel_launcher.py:12: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if sys.path[0] == '':
    C:\Users\harna\Anaconda3\envs\PythonData\lib\site-packages\ipykernel_launcher.py:13: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      del sys.path[0]
    C:\Users\harna\Anaconda3\envs\PythonData\lib\site-packages\ipykernel_launcher.py:14: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fare</th>
      <th>ride_id</th>
      <th>Num Riders</th>
      <th>Average Fare</th>
      <th>driver_count</th>
      <th>type</th>
      <th>color</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adamschester</th>
      <td>266.35</td>
      <td>45858404807271</td>
      <td>9</td>
      <td>29.594444</td>
      <td>27</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Alexisfort</th>
      <td>903.11</td>
      <td>150011666742656</td>
      <td>33</td>
      <td>27.366970</td>
      <td>24</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Amberberg</th>
      <td>457.99</td>
      <td>89722450773007</td>
      <td>16</td>
      <td>28.624375</td>
      <td>13</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Anthonyfurt</th>
      <td>501.35</td>
      <td>74520143331135</td>
      <td>17</td>
      <td>29.491176</td>
      <td>17</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Boyleberg</th>
      <td>161.98</td>
      <td>27303868891934</td>
      <td>5</td>
      <td>32.396000</td>
      <td>13</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Brianfurt</th>
      <td>539.15</td>
      <td>124943014145666</td>
      <td>22</td>
      <td>24.506818</td>
      <td>4</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Campbellmouth</th>
      <td>273.42</td>
      <td>40159572556105</td>
      <td>8</td>
      <td>34.177500</td>
      <td>2</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>Catherinebury</th>
      <td>791.93</td>
      <td>173331601121887</td>
      <td>29</td>
      <td>27.307931</td>
      <td>7</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Curtismouth</th>
      <td>776.61</td>
      <td>167418987160442</td>
      <td>31</td>
      <td>25.051935</td>
      <td>40</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Davidbury</th>
      <td>616.68</td>
      <td>78707241318680</td>
      <td>20</td>
      <td>30.834000</td>
      <td>13</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Davidsonfurt</th>
      <td>64.17</td>
      <td>10145228903926</td>
      <td>2</td>
      <td>32.085000</td>
      <td>1</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>East Amanda</th>
      <td>597.48</td>
      <td>104537083767957</td>
      <td>21</td>
      <td>28.451429</td>
      <td>20</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>East April</th>
      <td>479.82</td>
      <td>89198272935478</td>
      <td>16</td>
      <td>29.988750</td>
      <td>9</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>East James</th>
      <td>743.42</td>
      <td>148768506360587</td>
      <td>28</td>
      <td>26.550714</td>
      <td>49</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>East Jermaine</th>
      <td>419.22</td>
      <td>90324892755066</td>
      <td>16</td>
      <td>26.201250</td>
      <td>29</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>East Johnnyborough</th>
      <td>606.32</td>
      <td>84543317116083</td>
      <td>20</td>
      <td>30.316000</td>
      <td>15</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>East Karenmouth</th>
      <td>832.23</td>
      <td>174762968511087</td>
      <td>35</td>
      <td>23.778000</td>
      <td>46</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>East Rose</th>
      <td>460.54</td>
      <td>117806860535199</td>
      <td>22</td>
      <td>20.933636</td>
      <td>7</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Elizabethland</th>
      <td>597.30</td>
      <td>75432318477943</td>
      <td>20</td>
      <td>29.865000</td>
      <td>20</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Evansburgh</th>
      <td>540.08</td>
      <td>121988043885731</td>
      <td>23</td>
      <td>23.481739</td>
      <td>44</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Fergusonburgh</th>
      <td>670.01</td>
      <td>108451240191842</td>
      <td>21</td>
      <td>31.905238</td>
      <td>11</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Floresbury</th>
      <td>519.18</td>
      <td>108290455709626</td>
      <td>25</td>
      <td>20.767200</td>
      <td>14</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Gatesborough</th>
      <td>346.66</td>
      <td>67290263162337</td>
      <td>14</td>
      <td>24.761429</td>
      <td>5</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Hallmouth</th>
      <td>614.42</td>
      <td>101742187530256</td>
      <td>19</td>
      <td>32.337895</td>
      <td>10</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Heatherland</th>
      <td>443.50</td>
      <td>44384647328282</td>
      <td>14</td>
      <td>31.678571</td>
      <td>17</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Hillstad</th>
      <td>359.75</td>
      <td>52567338101982</td>
      <td>11</td>
      <td>32.704545</td>
      <td>4</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Hoganfort</th>
      <td>340.84</td>
      <td>44898795811143</td>
      <td>11</td>
      <td>30.985455</td>
      <td>5</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>Jamesbury</th>
      <td>789.34</td>
      <td>171312984492737</td>
      <td>30</td>
      <td>26.311333</td>
      <td>41</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Jamesland</th>
      <td>542.09</td>
      <td>80976217676211</td>
      <td>19</td>
      <td>28.531053</td>
      <td>22</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Jillmouth</th>
      <td>480.01</td>
      <td>105986190609096</td>
      <td>22</td>
      <td>21.818636</td>
      <td>42</td>
      <td>Urban</td>
      <td>lightcoral</td>
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
    </tr>
    <tr>
      <th>Robertsonhaven</th>
      <td>760.41</td>
      <td>90146085382205</td>
      <td>21</td>
      <td>36.210000</td>
      <td>1</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Russellfurt</th>
      <td>349.89</td>
      <td>58862178389214</td>
      <td>13</td>
      <td>26.914615</td>
      <td>9</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Scottside</th>
      <td>586.06</td>
      <td>149226519220102</td>
      <td>26</td>
      <td>22.540769</td>
      <td>48</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Sheltonhaven</th>
      <td>113.35</td>
      <td>28290942625961</td>
      <td>5</td>
      <td>22.670000</td>
      <td>1</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>Smithland</th>
      <td>709.51</td>
      <td>135133141471038</td>
      <td>28</td>
      <td>25.339643</td>
      <td>38</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Smithville</th>
      <td>152.52</td>
      <td>26358866997660</td>
      <td>6</td>
      <td>25.420000</td>
      <td>8</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>South Angela</th>
      <td>203.76</td>
      <td>32073511015087</td>
      <td>6</td>
      <td>33.960000</td>
      <td>9</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>South Brittany</th>
      <td>157.77</td>
      <td>29284192814020</td>
      <td>5</td>
      <td>31.554000</td>
      <td>9</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>South Jacobside</th>
      <td>411.89</td>
      <td>58774530409008</td>
      <td>9</td>
      <td>45.765556</td>
      <td>7</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>South John</th>
      <td>428.13</td>
      <td>81665493189034</td>
      <td>18</td>
      <td>23.785000</td>
      <td>24</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>South Lisaport</th>
      <td>536.77</td>
      <td>68257712780386</td>
      <td>16</td>
      <td>33.548125</td>
      <td>11</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>South Mariahaven</th>
      <td>371.43</td>
      <td>99637892955003</td>
      <td>17</td>
      <td>21.848824</td>
      <td>52</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>South Mary</th>
      <td>717.19</td>
      <td>152045221817656</td>
      <td>29</td>
      <td>24.730690</td>
      <td>20</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>South Samanthafurt</th>
      <td>201.37</td>
      <td>38665701583914</td>
      <td>7</td>
      <td>28.767143</td>
      <td>8</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>South Stephen</th>
      <td>192.70</td>
      <td>26238274938355</td>
      <td>6</td>
      <td>32.116667</td>
      <td>6</td>
      <td>Rural</td>
      <td>gold</td>
    </tr>
    <tr>
      <th>Suzanneborough</th>
      <td>813.89</td>
      <td>147848781166553</td>
      <td>30</td>
      <td>27.129667</td>
      <td>33</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Tammyburgh</th>
      <td>455.81</td>
      <td>106597117481781</td>
      <td>22</td>
      <td>20.718636</td>
      <td>11</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Theresaland</th>
      <td>669.19</td>
      <td>126145662129413</td>
      <td>26</td>
      <td>25.738077</td>
      <td>69</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Thomashaven</th>
      <td>617.98</td>
      <td>124362253346882</td>
      <td>25</td>
      <td>24.719200</td>
      <td>60</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Turnershire</th>
      <td>527.04</td>
      <td>116586728187511</td>
      <td>20</td>
      <td>26.352000</td>
      <td>23</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>West Darrellmouth</th>
      <td>402.72</td>
      <td>86153635637905</td>
      <td>18</td>
      <td>22.373333</td>
      <td>10</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>West Kennethland</th>
      <td>508.15</td>
      <td>98756044288412</td>
      <td>21</td>
      <td>24.197619</td>
      <td>23</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>West Lanceview</th>
      <td>410.81</td>
      <td>75049717841083</td>
      <td>18</td>
      <td>22.822778</td>
      <td>17</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>West Michaelfurt</th>
      <td>369.43</td>
      <td>69862924666206</td>
      <td>12</td>
      <td>30.785833</td>
      <td>27</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>West Nancy</th>
      <td>765.64</td>
      <td>142458120023730</td>
      <td>29</td>
      <td>26.401379</td>
      <td>40</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>West Nathanville</th>
      <td>537.37</td>
      <td>113992370634059</td>
      <td>21</td>
      <td>25.589048</td>
      <td>62</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>West Robertchester</th>
      <td>516.00</td>
      <td>107921133323954</td>
      <td>21</td>
      <td>24.571429</td>
      <td>8</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Whitneyfurt</th>
      <td>693.11</td>
      <td>154234339458383</td>
      <td>30</td>
      <td>23.103667</td>
      <td>53</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Williamsonville</th>
      <td>377.96</td>
      <td>66509515670814</td>
      <td>13</td>
      <td>29.073846</td>
      <td>3</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Xavierborough</th>
      <td>289.55</td>
      <td>49155393456488</td>
      <td>11</td>
      <td>26.322727</td>
      <td>8</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
  </tbody>
</table>
<p>126 rows × 7 columns</p>
</div>




```python
color = merged_cities["color"]
tot_drivers = (merged_cities["driver_count"]*5)
label = merged_cities.groupby("type").count()

tot_rides = merged_cities["Num Riders"]
avg_fare = merged_cities["Average Fare"]
tot_fare = merged_cities["fare"]
for x,y,c,lb in zip(tot_rides,avg_fare,color,label.index):
    plt.scatter(tot_rides, avg_fare, s=tot_drivers, facecolors=color, edgecolors="black", alpha=.5)

plt.ylim(15, 50, 5)

type_1 = mpatches.Patch(color='lightskyblue', label='Suburban')
type_2 = mpatches.Patch(color='lightcoral', label='Urban')
type_3 = mpatches.Patch(color='gold', label='Rural')

leg=plt.legend(handles=[type_2, type_1, type_3], title="City Types", loc='best')
plt.xlabel('Total Number of Rider (Per City)')
plt.ylabel('Average Fare ($)')
plt.title('Pyber Ride Sharing Data (2016)')
for l in leg.get_lines():
    l.set_alpha(0)
    l.set_marker('.')
plt.savefig('bubbleplot.png')
plt.show()
```


![png](output_3_0.png)



```python
city_type = merged_cities["type"].value_counts()
amt_per_type = merged_cities.groupby("type").sum()
fare_per_type = amt_per_type['fare']
labels = ["Urban", "Suburban", "Rural"]
tot_fares = merged_cities["fare"].sum()
data_1 = tot_fares/fare_per_type
explode = (0.1,0,0)

plt.pie(data_1, explode=explode, labels=labels, autopct="%1.1f%%", shadow=True, startangle=220)
plt.axis("equal")
plt.title("% of fares by city type")
plt.savefig('Pie1.png')
plt.show()
```


![png](output_4_0.png)



```python
riders_per_type = amt_per_type['Num Riders']
tot_riders = merged_cities["Num Riders"].sum()
data_2 = tot_riders/riders_per_type
explode = (0.1,0,0)

plt.pie(data_2, explode=explode, labels=labels, autopct="%1.1f%%", shadow=True, startangle=220)
plt.axis("equal")
plt.title("% of total riders by city type")
plt.savefig('Pie2.png')
plt.show()
```


![png](output_5_0.png)



```python
tot_dri_per_type = amt_per_type['driver_count']
tot_drivers = merged_cities["driver_count"].sum()
data_3 = tot_drivers/tot_dri_per_type
explode = (0.1,0,0)

plt.pie(data_3, explode=explode, labels=labels, autopct="%1.1f%%", shadow=True, startangle=220)
plt.axis("equal")
plt.title("% of total drivers by city type")
plt.savefig('Pie3.png')
plt.show()
```


![png](output_6_0.png)

