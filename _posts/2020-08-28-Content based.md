---
title: "Content-Based Recommender"
date: 2020-03-20
tags: [Machine Learning, Data Science, Recommendation Engine]
header:
  image: "/images/rc1.jpg"
excerpt: "Machine Learning, Data Science, Recommendation Engine "
mathjax: "true"
---

## Machine Learning Based Recommendation Systems
## Nearest Neighbors Algorithm



```python
import numpy as np
import pandas as pd

import sklearn
from sklearn.neighbors import NearestNeighbors
```

*mtcars dataset source:* 
Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391–411.


```python
cars = pd.read_csv('mtcars.csv')
cars.columns = ['car_names', 'mpg', 'cyl', 'disp', 'hp', 'drat', 'wt', 'qsec', 'vs', 'am', 'gear', 'carb']
cars.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>car_names</th>
      <th>mpg</th>
      <th>cyl</th>
      <th>disp</th>
      <th>hp</th>
      <th>drat</th>
      <th>wt</th>
      <th>qsec</th>
      <th>vs</th>
      <th>am</th>
      <th>gear</th>
      <th>carb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mazda RX4</td>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.620</td>
      <td>16.46</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mazda RX4 Wag</td>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.875</td>
      <td>17.02</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Datsun 710</td>
      <td>22.8</td>
      <td>4</td>
      <td>108.0</td>
      <td>93</td>
      <td>3.85</td>
      <td>2.320</td>
      <td>18.61</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hornet 4 Drive</td>
      <td>21.4</td>
      <td>6</td>
      <td>258.0</td>
      <td>110</td>
      <td>3.08</td>
      <td>3.215</td>
      <td>19.44</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hornet Sportabout</td>
      <td>18.7</td>
      <td>8</td>
      <td>360.0</td>
      <td>175</td>
      <td>3.15</td>
      <td>3.440</td>
      <td>17.02</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
t = [15, 300, 160, 3.2]

X = cars.ix[:,(1, 3, 4, 6)].values
X[0:5]
```




    array([[  21.   ,  160.   ,  110.   ,    2.62 ],
           [  21.   ,  160.   ,  110.   ,    2.875],
           [  22.8  ,  108.   ,   93.   ,    2.32 ],
           [  21.4  ,  258.   ,  110.   ,    3.215],
           [  18.7  ,  360.   ,  175.   ,    3.44 ]])




```python
nbrs = NearestNeighbors(n_neighbors=1).fit(X)
```


```python
print(nbrs.kneighbors([t]))
```

    (array([[ 10.77474942]]), array([[22]], dtype=int64))
    


```python
cars
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>car_names</th>
      <th>mpg</th>
      <th>cyl</th>
      <th>disp</th>
      <th>hp</th>
      <th>drat</th>
      <th>wt</th>
      <th>qsec</th>
      <th>vs</th>
      <th>am</th>
      <th>gear</th>
      <th>carb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mazda RX4</td>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.620</td>
      <td>16.46</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mazda RX4 Wag</td>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.875</td>
      <td>17.02</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Datsun 710</td>
      <td>22.8</td>
      <td>4</td>
      <td>108.0</td>
      <td>93</td>
      <td>3.85</td>
      <td>2.320</td>
      <td>18.61</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hornet 4 Drive</td>
      <td>21.4</td>
      <td>6</td>
      <td>258.0</td>
      <td>110</td>
      <td>3.08</td>
      <td>3.215</td>
      <td>19.44</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hornet Sportabout</td>
      <td>18.7</td>
      <td>8</td>
      <td>360.0</td>
      <td>175</td>
      <td>3.15</td>
      <td>3.440</td>
      <td>17.02</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Valiant</td>
      <td>18.1</td>
      <td>6</td>
      <td>225.0</td>
      <td>105</td>
      <td>2.76</td>
      <td>3.460</td>
      <td>20.22</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Duster 360</td>
      <td>14.3</td>
      <td>8</td>
      <td>360.0</td>
      <td>245</td>
      <td>3.21</td>
      <td>3.570</td>
      <td>15.84</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Merc 240D</td>
      <td>24.4</td>
      <td>4</td>
      <td>146.7</td>
      <td>62</td>
      <td>3.69</td>
      <td>3.190</td>
      <td>20.00</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Merc 230</td>
      <td>22.8</td>
      <td>4</td>
      <td>140.8</td>
      <td>95</td>
      <td>3.92</td>
      <td>3.150</td>
      <td>22.90</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Merc 280</td>
      <td>19.2</td>
      <td>6</td>
      <td>167.6</td>
      <td>123</td>
      <td>3.92</td>
      <td>3.440</td>
      <td>18.30</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Merc 280C</td>
      <td>17.8</td>
      <td>6</td>
      <td>167.6</td>
      <td>123</td>
      <td>3.92</td>
      <td>3.440</td>
      <td>18.90</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Merc 450SE</td>
      <td>16.4</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>4.070</td>
      <td>17.40</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Merc 450SL</td>
      <td>17.3</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>3.730</td>
      <td>17.60</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Merc 450SLC</td>
      <td>15.2</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>3.780</td>
      <td>18.00</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Cadillac Fleetwood</td>
      <td>10.4</td>
      <td>8</td>
      <td>472.0</td>
      <td>205</td>
      <td>2.93</td>
      <td>5.250</td>
      <td>17.98</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Lincoln Continental</td>
      <td>10.4</td>
      <td>8</td>
      <td>460.0</td>
      <td>215</td>
      <td>3.00</td>
      <td>5.424</td>
      <td>17.82</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chrysler Imperial</td>
      <td>14.7</td>
      <td>8</td>
      <td>440.0</td>
      <td>230</td>
      <td>3.23</td>
      <td>5.345</td>
      <td>17.42</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Fiat 128</td>
      <td>32.4</td>
      <td>4</td>
      <td>78.7</td>
      <td>66</td>
      <td>4.08</td>
      <td>2.200</td>
      <td>19.47</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Honda Civic</td>
      <td>30.4</td>
      <td>4</td>
      <td>75.7</td>
      <td>52</td>
      <td>4.93</td>
      <td>1.615</td>
      <td>18.52</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Toyota Corolla</td>
      <td>33.9</td>
      <td>4</td>
      <td>71.1</td>
      <td>65</td>
      <td>4.22</td>
      <td>1.835</td>
      <td>19.90</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Toyota Corona</td>
      <td>21.5</td>
      <td>4</td>
      <td>120.1</td>
      <td>97</td>
      <td>3.70</td>
      <td>2.465</td>
      <td>20.01</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Dodge Challenger</td>
      <td>15.5</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>2.76</td>
      <td>3.520</td>
      <td>16.87</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>22</th>
      <td>AMC Javelin</td>
      <td>15.2</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3.15</td>
      <td>3.435</td>
      <td>17.30</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Camaro Z28</td>
      <td>13.3</td>
      <td>8</td>
      <td>350.0</td>
      <td>245</td>
      <td>3.73</td>
      <td>3.840</td>
      <td>15.41</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Pontiac Firebird</td>
      <td>19.2</td>
      <td>8</td>
      <td>400.0</td>
      <td>175</td>
      <td>3.08</td>
      <td>3.845</td>
      <td>17.05</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Fiat X1-9</td>
      <td>27.3</td>
      <td>4</td>
      <td>79.0</td>
      <td>66</td>
      <td>4.08</td>
      <td>1.935</td>
      <td>18.90</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Porsche 914-2</td>
      <td>26.0</td>
      <td>4</td>
      <td>120.3</td>
      <td>91</td>
      <td>4.43</td>
      <td>2.140</td>
      <td>16.70</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Lotus Europa</td>
      <td>30.4</td>
      <td>4</td>
      <td>95.1</td>
      <td>113</td>
      <td>3.77</td>
      <td>1.513</td>
      <td>16.90</td>
      <td>1</td>
      <td>1</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Ford Pantera L</td>
      <td>15.8</td>
      <td>8</td>
      <td>351.0</td>
      <td>264</td>
      <td>4.22</td>
      <td>3.170</td>
      <td>14.50</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Ferrari Dino</td>
      <td>19.7</td>
      <td>6</td>
      <td>145.0</td>
      <td>175</td>
      <td>3.62</td>
      <td>2.770</td>
      <td>15.50</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Maserati Bora</td>
      <td>15.0</td>
      <td>8</td>
      <td>301.0</td>
      <td>335</td>
      <td>3.54</td>
      <td>3.570</td>
      <td>14.60</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Volvo 142E</td>
      <td>21.4</td>
      <td>4</td>
      <td>121.0</td>
      <td>109</td>
      <td>4.11</td>
      <td>2.780</td>
      <td>18.60</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
