In this project, Tableau is used to analyze Citi Bike trip histories data for Jersey City in 2018.  Each csv contained data for a specific month, so Dask was used to 
merge the twelve datasets for 2018.

## Citi Bike Trip History Data Resource Link
https://www.citibikenyc.com/system-data


## Tableau Link
https://public.tableau.com/profile/orlando8029#!/vizhome/CitiBikeTrips-Year/StartStationMap

## Findings

* The most popular start station is Grove St Path and the least popular start station is Columbia Park.
* The popular start stations are close to the river.  Sip Avenue is an exception.  The least popular start stations are far from the river.
* Bikers travel primarily close to the popular start stations, but they also travel to NY and spots far from the popular start station.
* Grove St PATH is also the most popular end station.  6 Ave & Canal St is the least popular end station.
* Popular end stations are around Grove St Path and close to the river.  The least popular end stations are far from Grove St Path or in New York.
* Bikers end their bike trips primarily near the river in Jersey City.

* Bike ridership by men are much higher than bike ridership by women in 2018.
* Bike ridership by men increases during the summer months much more significantly than bike ridership by women.
* The number of subscriber bikers increases much more significantly during the summer months than the number of customer bikers.
* Bike trips during the summer happen mainly at 8 AM and 5 PM.  The trend for bike trips during particular hours is similar during the winter months.
* Adolescents have the highest average trip duration, but bikers aged 50, 72, and 80 also have significantly high average trip durations.
* The most used bikes are bikes with ID 26000-27000, 29000-29700, 31151, and 33500-33600. These bikes likely need to be repaired or replaced. Bikes with ID below 25000 and above 34000 were rarely used.


## Jupyter Notebook: Dask Dataset Merge Code

```python
import dask.dataframe as dd
import pandas as pd
```


```python
# Read the csvs for the 12 months in 2018 and create Dask dataframes
df1 = dd.read_csv('resources/JC-201801-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df2 = dd.read_csv('resources/JC-201802-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df3 = dd.read_csv('resources/JC-201803-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df4 = dd.read_csv('resources/JC-201804-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df5 = dd.read_csv('resources/JC-201805-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df6 = dd.read_csv('resources/JC-201806-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df7 = dd.read_csv('resources/JC-201807-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df8 = dd.read_csv('resources/JC-201808-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df9 = dd.read_csv('resources/JC-201809-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df10 = dd.read_csv('resources/JC-201810-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df11 = dd.read_csv('resources/JC-201811-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})

df12 = dd.read_csv('resources/JC-201812-citibike-tripdata.csv', dtype={'end station id': 'float64',
      'start station id': 'float64'})
```


```python
# Merge the 12 dataframes to create one dataframe containing data for 2018
year_df = df1.merge(df2,how='outer').merge(df3,how='outer').merge(df4,how='outer').\
        merge(df5,how='outer').merge(df6,how='outer').merge(df7,how='outer').\
        merge(df8,how='outer').merge(df9,how='outer').merge(df10,how='outer').\
        merge(df11,how='outer').merge(df12,how='outer')
```


```python
year_df.tail()
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
      <th>tripduration</th>
      <th>starttime</th>
      <th>stoptime</th>
      <th>start station id</th>
      <th>start station name</th>
      <th>start station latitude</th>
      <th>start station longitude</th>
      <th>end station id</th>
      <th>end station name</th>
      <th>end station latitude</th>
      <th>end station longitude</th>
      <th>bikeid</th>
      <th>usertype</th>
      <th>birth year</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>353887</th>
      <td>1081</td>
      <td>2018-12-22 11:51:46.0600</td>
      <td>2018-12-22 12:09:47.4730</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3269.0</td>
      <td>Brunswick &amp; 6th</td>
      <td>40.726012</td>
      <td>-74.050389</td>
      <td>29586</td>
      <td>Subscriber</td>
      <td>1993</td>
      <td>1</td>
    </tr>
    <tr>
      <th>353888</th>
      <td>344</td>
      <td>2018-12-25 21:40:09.8660</td>
      <td>2018-12-25 21:45:54.2670</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3280.0</td>
      <td>Astor Place</td>
      <td>40.719282</td>
      <td>-74.071262</td>
      <td>26241</td>
      <td>Subscriber</td>
      <td>1983</td>
      <td>2</td>
    </tr>
    <tr>
      <th>353889</th>
      <td>1233</td>
      <td>2018-12-29 12:55:45.9690</td>
      <td>2018-12-29 13:16:19.5960</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3186.0</td>
      <td>Grove St PATH</td>
      <td>40.719586</td>
      <td>-74.043117</td>
      <td>29294</td>
      <td>Subscriber</td>
      <td>1988</td>
      <td>1</td>
    </tr>
    <tr>
      <th>353890</th>
      <td>1057</td>
      <td>2018-12-30 15:32:09.3320</td>
      <td>2018-12-30 15:49:46.3510</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3213.0</td>
      <td>Van Vorst Park</td>
      <td>40.718489</td>
      <td>-74.047727</td>
      <td>29475</td>
      <td>Subscriber</td>
      <td>1991</td>
      <td>2</td>
    </tr>
    <tr>
      <th>353891</th>
      <td>301</td>
      <td>2018-12-31 16:34:11.9340</td>
      <td>2018-12-31 16:39:13.8340</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3277.0</td>
      <td>Communipaw &amp; Berry Lane</td>
      <td>40.714358</td>
      <td>-74.066611</td>
      <td>26270</td>
      <td>Subscriber</td>
      <td>1991</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Compute the count of the number of records
final_year_df = year_df.compute()

# Save the dataframe into a csv
final_year_df.to_csv("resources/JC-2018-citibike-tripdata.csv")
```


```python
# Read the 2018 data csv and create a Pandas dataframe
data_df = pd.read_csv("resources/JC-2018-citibike-tripdata.csv")
data_df.tail()
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
      <th>Unnamed: 0</th>
      <th>tripduration</th>
      <th>starttime</th>
      <th>stoptime</th>
      <th>start station id</th>
      <th>start station name</th>
      <th>start station latitude</th>
      <th>start station longitude</th>
      <th>end station id</th>
      <th>end station name</th>
      <th>end station latitude</th>
      <th>end station longitude</th>
      <th>bikeid</th>
      <th>usertype</th>
      <th>birth year</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>353887</th>
      <td>353887</td>
      <td>1081</td>
      <td>2018-12-22 11:51:46.0600</td>
      <td>2018-12-22 12:09:47.4730</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3269.0</td>
      <td>Brunswick &amp; 6th</td>
      <td>40.726012</td>
      <td>-74.050389</td>
      <td>29586</td>
      <td>Subscriber</td>
      <td>1993</td>
      <td>1</td>
    </tr>
    <tr>
      <th>353888</th>
      <td>353888</td>
      <td>344</td>
      <td>2018-12-25 21:40:09.8660</td>
      <td>2018-12-25 21:45:54.2670</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3280.0</td>
      <td>Astor Place</td>
      <td>40.719282</td>
      <td>-74.071262</td>
      <td>26241</td>
      <td>Subscriber</td>
      <td>1983</td>
      <td>2</td>
    </tr>
    <tr>
      <th>353889</th>
      <td>353889</td>
      <td>1233</td>
      <td>2018-12-29 12:55:45.9690</td>
      <td>2018-12-29 13:16:19.5960</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3186.0</td>
      <td>Grove St PATH</td>
      <td>40.719586</td>
      <td>-74.043117</td>
      <td>29294</td>
      <td>Subscriber</td>
      <td>1988</td>
      <td>1</td>
    </tr>
    <tr>
      <th>353890</th>
      <td>353890</td>
      <td>1057</td>
      <td>2018-12-30 15:32:09.3320</td>
      <td>2018-12-30 15:49:46.3510</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3213.0</td>
      <td>Van Vorst Park</td>
      <td>40.718489</td>
      <td>-74.047727</td>
      <td>29475</td>
      <td>Subscriber</td>
      <td>1991</td>
      <td>2</td>
    </tr>
    <tr>
      <th>353891</th>
      <td>353891</td>
      <td>301</td>
      <td>2018-12-31 16:34:11.9340</td>
      <td>2018-12-31 16:39:13.8340</td>
      <td>3694.0</td>
      <td>Jackson Square</td>
      <td>40.71113</td>
      <td>-74.0789</td>
      <td>3277.0</td>
      <td>Communipaw &amp; Berry Lane</td>
      <td>40.714358</td>
      <td>-74.066611</td>
      <td>26270</td>
      <td>Subscriber</td>
      <td>1991</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
