

```python
import pandas as pd
import numpy as np
import os
import json

```


```python
data_file = os.path.join("purchase_data.json")
data_file
```




    'purchase_data.json'




```python
pymoli_df = pd.read_json('purchase_data.json')
pymoli_df.head()                     
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Player count

player_count = len(pymoli_df["SN"].value_counts())
player_count
```




    573




```python
#Purchasing Analysis
#Number of unique items
unique_items = len(pymoli_df["Item Name"].value_counts())
unique_items
```




    179




```python
#Average purchase price
average_pp = pymoli_df["Price"].mean()
average_pp
```




    2.931192307692303




```python
#Number of purchases.
number_of_purchases = pymoli_df["Item Name"].count()
number_of_purchases
```




    780




```python
#Total Revenue

total_revenue = pymoli_df["Price"].sum()
total_revenue
```




    2286.3299999999963




```python
#Number of purchases.
number_of_gender = pymoli_df["Gender"].value_counts()
number_of_gender
```




    Male                     633
    Female                   136
    Other / Non-Disclosed     11
    Name: Gender, dtype: int64




```python
#Males count

where_tuple = (pymoli_df["Gender"]=="Male")
males = pymoli_df.loc[where_tuple,:]
males.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
male_count = len(males)
male_count
```




    633




```python
#Female count

where_tuple = (pymoli_df["Gender"]=="Female")
females = pymoli_df.loc[where_tuple,:]
females.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
  </tbody>
</table>
</div>



#Female Count

where_tuple = (pymoli_df["Gender"]=="Female")
females = pymoli_df.loc[where_tuple,:]
females.head()


```python
female_count = len(females)
female_count
```




    136




```python
#number of Other / Non-Disclosed

where_tuple = (pymoli_df["Gender"]=="Other / Non-Disclosed")
others = pymoli_df.loc[where_tuple,:]
others.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
    </tr>
    <tr>
      <th>209</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>157</td>
      <td>Spada, Etcher of Hatred</td>
      <td>2.21</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>244</th>
      <td>21</td>
      <td>Other / Non-Disclosed</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Tyaerith73</td>
    </tr>
    <tr>
      <th>267</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>65</td>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>276</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>128</td>
      <td>Blazeguard, Reach of Eternity</td>
      <td>4.00</td>
      <td>Aillycal84</td>
    </tr>
  </tbody>
</table>
</div>




```python
others_count = len(others)
others_count
```




    11




```python
#sum of males, females and other
total_count = male_count + female_count + others_count

total_count
```




    780




```python
male_percent  = male_count / total_count * 100


male_percent

```




    81.15384615384616




```python
female_percent = female_count / total_count * 100

female_percent

```




    17.435897435897434




```python
others_percent = others_count / total_count * 100

others_percent
```




    1.4102564102564104




```python
Per = male_percent + female_percent + others_percent

Per
```




    100.0




```python
#Male average purchase price
male_ave = males["Price"].mean()
male_ave
```




    2.9505213270142154




```python
#Female average purchase price
female_ave = females["Price"].mean()
female_ave
```




    2.815514705882352




```python
#Others average purchase price
others_ave = others["Price"].mean()
others_ave

```




    3.2490909090909086




```python
#Male purchase value

male_pv = male_ave * male_count
male_pv
```




    1867.6799999999985




```python
#Female purchase value

female_pv = female_ave * female_count
female_pv
```




    382.90999999999985




```python
#Others purchase value

others_pv = others_ave * others_count
others_pv
```




    35.739999999999995




```python
#Male normalized total

nt_male = male_pv / male_count
nt_male
```




    2.9505213270142154




```python
#Female normalized total

nt_female = female_pv / female_count
nt_female
```




    2.815514705882352




```python
#Others normalized total

nt_others = others_pv / others_count
nt_others
```




    3.2490909090909086




```python
#Age breakdown
bins = [4,8,12,16,20,24,28,32,36,40,44,48,52,56,60,64,68,72,76,80,84,88,92,96,100]
pymoli_df["Age Group"] = pd.cut(pymoli_df["Age"], bins)
pymoli_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>(36, 40]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>(20, 24]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>(32, 36]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>(20, 24]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>(20, 24]</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Creating a group based off of the bins
age_groups = pymoli_df.groupby("Age Group")
age_groups.min().head()

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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Age Group</th>
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
      <th>(4, 8]</th>
      <td>7.0</td>
      <td>Female</td>
      <td>10.0</td>
      <td>Alpha, Oath of Zeal</td>
      <td>1.03</td>
      <td>Eosurdru76</td>
    </tr>
    <tr>
      <th>(8, 12]</th>
      <td>9.0</td>
      <td>Female</td>
      <td>11.0</td>
      <td>Aetherius, Boon of the Blessed</td>
      <td>1.27</td>
      <td>Aillycal84</td>
    </tr>
    <tr>
      <th>(12, 16]</th>
      <td>13.0</td>
      <td>Female</td>
      <td>2.0</td>
      <td>Abyssal Shard</td>
      <td>1.21</td>
      <td>Aeral97</td>
    </tr>
    <tr>
      <th>(16, 20]</th>
      <td>17.0</td>
      <td>Female</td>
      <td>4.0</td>
      <td>Aetherius, Boon of the Blessed</td>
      <td>1.03</td>
      <td>Adairialis76</td>
    </tr>
    <tr>
      <th>(20, 24]</th>
      <td>21.0</td>
      <td>Female</td>
      <td>1.0</td>
      <td>Alpha</td>
      <td>1.03</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
Age_groups = pymoli_df.groupby("Age Group")
Age_groups.min().head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Age Group</th>
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
      <th>(4, 8]</th>
      <td>7.0</td>
      <td>Female</td>
      <td>10.0</td>
      <td>Alpha, Oath of Zeal</td>
      <td>1.03</td>
      <td>Eosurdru76</td>
    </tr>
    <tr>
      <th>(8, 12]</th>
      <td>9.0</td>
      <td>Female</td>
      <td>11.0</td>
      <td>Aetherius, Boon of the Blessed</td>
      <td>1.27</td>
      <td>Aillycal84</td>
    </tr>
    <tr>
      <th>(12, 16]</th>
      <td>13.0</td>
      <td>Female</td>
      <td>2.0</td>
      <td>Abyssal Shard</td>
      <td>1.21</td>
      <td>Aeral97</td>
    </tr>
    <tr>
      <th>(16, 20]</th>
      <td>17.0</td>
      <td>Female</td>
      <td>4.0</td>
      <td>Aetherius, Boon of the Blessed</td>
      <td>1.03</td>
      <td>Adairialis76</td>
    </tr>
    <tr>
      <th>(20, 24]</th>
      <td>21.0</td>
      <td>Female</td>
      <td>1.0</td>
      <td>Alpha</td>
      <td>1.03</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
pur_count = Age_groups["Age Group"].count()
AvePurPrice = Age_groups["Price"].mean()
Pur_Value = pur_count * AvePurPrice
Norm_Total = pur_count / AvePurPrice


```


```python
#Age Demographic Table

age_demo = pd.DataFrame({"Purchase Count":pur_count,
                          "Average Purchase Price":AvePurPrice,
                          "Total Purchase Value":Pur_Value,
                          "Normalized Total":Norm_Total
                        
})
    
age_demo.head()
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
      <th>Average Purchase Price</th>
      <th>Normalized Total</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>(4, 8]</th>
      <td>2.788182</td>
      <td>7.890447</td>
      <td>22</td>
      <td>61.34</td>
    </tr>
    <tr>
      <th>(8, 12]</th>
      <td>3.385417</td>
      <td>7.089231</td>
      <td>24</td>
      <td>81.25</td>
    </tr>
    <tr>
      <th>(12, 16]</th>
      <td>2.745862</td>
      <td>31.684039</td>
      <td>87</td>
      <td>238.89</td>
    </tr>
    <tr>
      <th>(16, 20]</th>
      <td>2.907019</td>
      <td>55.383202</td>
      <td>161</td>
      <td>468.03</td>
    </tr>
    <tr>
      <th>(20, 24]</th>
      <td>2.924748</td>
      <td>81.374535</td>
      <td>238</td>
      <td>696.09</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Creating a group based off of the bins
spenders_groups = pymoli_df.groupby("SN")
spenders_groups.min().head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age Group</th>
    </tr>
    <tr>
      <th>SN</th>
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
      <th>Adairialis76</th>
      <td>20</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>(16, 20]</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>37</td>
      <td>Male</td>
      <td>79</td>
      <td>Alpha, Oath of Zeal</td>
      <td>1.36</td>
      <td>(36, 40]</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>26</td>
      <td>Male</td>
      <td>39</td>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>1.16</td>
      <td>(24, 28]</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>25</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>(24, 28]</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>(20, 24]</td>
    </tr>
  </tbody>
</table>
</div>




```python
pur_count = spenders_groups["SN"].count()
AvePurPrice = spenders_groups["Price"].mean()
Pur_Value = spenders_groups["Price"].sum()
```


```python
#Top Spenders

TopSpender = pd.DataFrame({"Purchase Count":pur_count,
                          "Average Purchase Price":AvePurPrice,
                          "Total Purchase Value":Pur_Value,
                          })
    
TopSpender.head()
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
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.460000</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>2.233333</td>
      <td>3</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>1.933333</td>
      <td>3</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.460000</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.270000</td>
      <td>1</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Sorting for top spenders

TopFive = TopSpender.sort_values("Total Purchase Value", ascending=False)
TopFive.head(5)
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
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>3.412000</td>
      <td>5</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>3.390000</td>
      <td>4</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>3.185000</td>
      <td>4</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>4.243333</td>
      <td>3</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3.860000</td>
      <td>3</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
#5 most popular items

pop_items = pymoli_df.groupby("Item ID")
pop_items.min().head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Group</th>
    </tr>
    <tr>
      <th>Item ID</th>
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
      <th>0</th>
      <td>30</td>
      <td>Male</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
      <td>(28, 32]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>Crucifer</td>
      <td>2.28</td>
      <td>Assylla81</td>
      <td>(20, 24]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15</td>
      <td>Male</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>(12, 16]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>Male</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>(12, 16]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>Male</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>Thryallym62</td>
      <td>(16, 20]</td>
    </tr>
  </tbody>
</table>
</div>




```python
pur_countA = pop_items["Item ID"].count()
AvePurPriceA = pop_items["Price"].mean()
Pur_ValueA = pop_items["Price"].sum()
```


```python
#Popular Items

PopularItems = pd.DataFrame({"Purchase Count":pur_countA,
                          "Item Price": AvePurPriceA,
                          "Total Purchase Value":Pur_ValueA,                    
                           })
                          
    
PopularItems.head()
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
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
      <td>1</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.28</td>
      <td>4</td>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
      <td>1</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
      <td>1</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
      <td>1</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top five popular items 
TopFivePopularItems = PopularItems.sort_values("Purchase Count", ascending=False)
TopFivePopularItems.head(5)
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
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>2.35</td>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>2.23</td>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2.07</td>
      <td>9</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1.24</td>
      <td>9</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1.49</td>
      <td>9</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top five profitable items 
TopFiveProfitableItems = PopularItems.sort_values("Total Purchase Value", ascending=False)
TopFiveProfitableItems.head(5)
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
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>4.14</td>
      <td>9</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>4.25</td>
      <td>7</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>4.95</td>
      <td>6</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>4.87</td>
      <td>6</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>3.61</td>
      <td>8</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>


