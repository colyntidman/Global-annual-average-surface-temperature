# NASA - Global annual average surface temperature

## Input

We found on a the NASA website : https://data.giss.nasa.gov/gistemp/graphs/graph_data/Global_Mean_Estimates_based_on_Land_and_Ocean_Data/graph.txt

```python
import pandas

url_nasa_termperatures = "https://data.giss.nasa.gov/gistemp/graphs/graph_data/Global_Mean_Estimates_based_on_Land_and_Ocean_Data/graph.txt"

df = pandas.read_csv(url_nasa_termperatures, sep=r'     ', skiprows=5, names=["Year", "Delta", "Detla (Smoothed)"], engine="python")
```

## Model

```python
df.tail(10)
```

Here we can see the evolution of the average surface temperature anomaly from the last 10 years. <br>
Now lets visualize this information with a graph using pyplot :

## Output

```python
import matplotlib.pyplot as plt

plt.plot(df["Year"], df["Detla (Smoothed)"], label = "Delta (Smoothed)", color='red')
plt.plot(df["Year"], df["Delta"], label = "Delta", color='l')

plt.xlabel('Year')
plt.ylabel('Temperature Anomaly (°C)')

plt.title('Land-Ocean Temperature Index (°C)')
plt.legend()
plt.show()
```

According to the Paris Agreement, the delta **should not be higher than 2**. As you can see here on the graph, it increasing quickly with the years specially since 1950

We can now add the dates of two Industrial Revolutions (1890-1910 and 1970-2000)

```python
plt.plot(df["Year"], df["Detla (Smoothed)"], label = "Delta (Smoothed)", color='red')
plt.plot(df["Year"], df["Delta"], label = "Delta", color='lightgray')

plt.xlabel('Year')
plt.ylabel('Temperature Anomaly (°C)')

plt.title('Land-Ocean Temperature Index (°C)')
plt.legend()


plt.annotate("Indus. Rev.", (1910, 0.0))
plt.annotate("Indus. Rev.", (1970, 0.4))
plt.show()
```

<br><br> **TODO :**
- *Predict with machine learning the delta for the next 50 years*

## Credits
Colyn TIDMAN<br>
Dylan PICHON