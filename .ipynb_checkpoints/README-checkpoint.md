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

### Land-Ocean Temperature Index - Visualization

```python
import plotly.graph_objects as go

fig = go.Figure(layout_title="Land-Ocean Temperature Index (°C)")
fig.add_trace(go.Scatter(
    x = df["Year"],
    y = df["Delta"],
    name="Delta",
))

fig.add_trace(go.Scatter(
    x = df["Year"],
    y = df["Detla (Smoothed)"],
    name="Delta (Smoothed)"
))

fig.update_layout(
    autosize=False,
    width=1300,
    height=700,
    xaxis = dict(
    tickmode = 'linear',
    tick0 = 2,
    dtick = 5,
    ),
)
fig.update_yaxes(title_text="Temperature anomaly (°C)")
fig.update_xaxes(title_text="Year")

fig.show()
```

According to the Paris Agreement, the delta **should not be higher than 2**. As you can see here on the graph, it increasing quickly with the years specially since 1950

### Land-Ocean Temperature Index - Visualization with Industrial Revolution Dates

We can now add the dates of the three last Industrial Revolutions 

    - Second : gaz and petrol
    - Third : internet
    - Forth : AI

```python
fig.add_vrect(x0="1910", x1="1911", annotation_text="2nd IR", annotation_position="top left",
annotation=dict(font_size=20, font_family="Times New Roman"),
fillcolor="black", opacity=0.25, line_width=0)

fig.add_vrect(x0="1970", x1="1971", annotation_text="3rd IR", annotation_position="top left",
annotation=dict(font_size=20, font_family="Times New Roman"),
fillcolor="yellow", opacity=0.25, line_width=0)

fig.add_vrect(x0="2000", x1="2001", annotation_text="4th IR", annotation_position="top left",
annotation=dict(font_size=20, font_family="Times New Roman"),
fillcolor="green", opacity=0.25, line_width=0)

fig.show()
```

<br><br> **TODO :**
- *Predict with machine learning the delta for the next 50 years*

## Credits
Colyn TIDMAN<br>
Dylan PICHON