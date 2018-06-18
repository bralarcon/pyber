# pyber

```python
#Observable trend 1:
#The data clearly demonstrates the urban areas provide the most rides for the Pyber drivers.
```


```python
#Observable trend 2:
#The urban areas account for more than half of all the fares for the total population accounted for.
```


```python
#Observable trend 3:
#The least profitable segment for Pyber is clearly the rural areas.  The rural areas generate the least in fares, drivers 
# and total rides.

```


```python
#dependencies
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
%matplotlib inline
```


```python
# Load in csv
c_df = pd.read_csv("city_data.csv")
m_df = pd.read_csv("ride_data.csv")
pd.merge = c_df.merge(m_df, on='city', how='left')
df = pd.merge
df.head(10)
```




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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-24 08:40:38</td>
      <td>13.93</td>
      <td>5628545007794</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-13 12:46:07</td>
      <td>14.00</td>
      <td>910050116494</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-16 13:52:19</td>
      <td>17.92</td>
      <td>820639054416</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-01 20:18:28</td>
      <td>10.26</td>
      <td>9554935945413</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-04-17 02:26:37</td>
      <td>23.00</td>
      <td>720020655850</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-04-21 03:44:04</td>
      <td>9.54</td>
      <td>3698147103219</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-03 00:14:26</td>
      <td>29.04</td>
      <td>4982665519010</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-08 15:50:12</td>
      <td>16.55</td>
      <td>2270463070874</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-04-03 15:07:34</td>
      <td>40.77</td>
      <td>9496210735824</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-19 14:09:20</td>
      <td>27.11</td>
      <td>8690324801449</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Fare per City
avg_fare = df.groupby('city').fare.mean().reset_index()
avg_fare.head(5)
```




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
      <th>city</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Amandaburgh</td>
      <td>24.641667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Barajasview</td>
      <td>25.332273</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Barronchester</td>
      <td>36.422500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bethanyland</td>
      <td>32.956111</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bradshawfurt</td>
      <td>40.064000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Number of Rides per City
rides_per_city = df.groupby('city').city.count()
rides_per_city.head()
```




    city
    Amandaburgh      18
    Barajasview      22
    Barronchester    16
    Bethanyland      18
    Bradshawfurt     10
    Name: city, dtype: int64




```python
#Total Number of Drivers Per City
drivers_per_city = df.groupby('city').driver_count.sum().reset_index()
drivers_per_city.head(5)
```




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
      <th>city</th>
      <th>driver_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Amandaburgh</td>
      <td>216</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Barajasview</td>
      <td>572</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Barronchester</td>
      <td>176</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bethanyland</td>
      <td>396</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bradshawfurt</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>




```python
#City Type
city_type = df.groupby('type').count().reset_index()
city_type.head()

```




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
      <th>type</th>
      <th>city</th>
      <th>driver_count</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python

x=df['type']
y=df['fare']
z=df['driver_count']
colors = ["gold", "lightcoral", "lightskyblue"]



plt.title('Pyber Ride Sharing Data')
plt.xlabel('total # of rides')
plt.ylabel('avg fare $')

plt.scatter(x, y, s=z, alpha=0.5, c=colors)
plt.show()

```


![png](output_9_0.png)



```python
# % of fares by city type

df.groupby(['fare','type']).count().reset_index()['type'].value_counts(normalize=True)*100
```




    Urban       65.594542
    Suburban    28.460039
    Rural        5.945419
    Name: type, dtype: float64




```python
# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
sizes = [65.594542, 28.460039, 5.945419]

# The colors of each section of the pie chart
colors = ["gold", "lightcoral", "lightskyblue"]

plt.title('% of fares by city type')

plt.pie(sizes, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
```




    ([<matplotlib.patches.Wedge at 0x1d12d633ba8>,
      <matplotlib.patches.Wedge at 0x1d12d63c588>,
      <matplotlib.patches.Wedge at 0x1d12d647048>],
     [Text(-0.227385,-1.07624,'Urban'),
      Text(0.423285,1.0153,'Suburban'),
      Text(-0.696693,0.851246,'Rural')],
     [Text(-0.124028,-0.587041,'65.6%'),
      Text(0.230882,0.553799,'28.5%'),
      Text(-0.380014,0.464316,'5.9%')])




![png](output_11_1.png)



```python
#% of total rides by city type

df.groupby(['city','type']).count().reset_index()['type'].value_counts(normalize=True)*100
```




    Urban       55.0
    Suburban    30.0
    Rural       15.0
    Name: type, dtype: float64




```python
# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
sizes = [55.0, 30.0, 15.0]

# The colors of each section of the pie chart
colors = ["gold", "lightcoral", "lightskyblue"]

plt.title('% of total rides by city type')

plt.pie(sizes, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
```




    ([<matplotlib.patches.Wedge at 0x1d12d6975c0>,
      <matplotlib.patches.Wedge at 0x1d12d69f048>,
      <matplotlib.patches.Wedge at 0x1d12d69fac8>],
     [Text(-0.566542,-0.942884,'Urban'),
      Text(0.932853,0.582911,'Suburban'),
      Text(-0.429804,1.01256,'Rural')],
     [Text(-0.309023,-0.5143,'55.0%'),
      Text(0.508829,0.317952,'30.0%'),
      Text(-0.234439,0.552303,'15.0%')])




![png](output_13_1.png)



```python
#% of total drivers by city type

df.groupby(['driver_count', 'type']).count().reset_index()['type'].value_counts(normalize=True)*100
```




    Urban       64.285714
    Suburban    25.714286
    Rural       10.000000
    Name: type, dtype: float64




```python
# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
sizes = [64.285714, 25.714286, 10.0]

# The colors of each section of the pie chart
colors = ["gold", "lightcoral", "lightskyblue"]

plt.title('% of total drivers by city type')

plt.pie(sizes, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
```




    ([<matplotlib.patches.Wedge at 0x1d12d6e7b00>,
      <matplotlib.patches.Wedge at 0x1d12d6ee588>,
      <matplotlib.patches.Wedge at 0x1d12d6f9048>],
     [Text(-0.271433,-1.06599,'Urban'),
      Text(0.587556,0.929935,'Suburban'),
      Text(-0.582911,0.932853,'Rural')],
     [Text(-0.148054,-0.581446,'64.3%'),
      Text(0.320485,0.507237,'25.7%'),
      Text(-0.317952,0.508829,'10.0%')])




![png](output_15_1.png)

