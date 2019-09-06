---
redirect_from:
  - "/mybook/jupyter-interactive-widget"
interact_link: content/Mybook/jupyter_interactive_widget.ipynb
kernel_name: venv06
has_widgets: false
title: 'interactive widget'
prev_page:
  url: /Mybook/Chapter_03_API.html
  title: 'chart test'
next_page:
  url: /intro.html
  title: 'Home'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---


* Interactive widget을 jupyter 에서 사용하기
* source: https://junpyopark.github.io/interactive_jupyter/?fbclid=IwAR25KAo65q0iQSmgU4oPLFPFGO6IAhTjG6IDcBzx2UKBD49BfrOf7HLVb3I



* library load



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
import numpy as np
import pandas as pd
from sklearn import datasets
import ipywidgets as widgets
from ipywidgets import interact, interact_manual
import cufflinks as cf
cf.go_offline(connected=True)

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

<div markdown="0" class="output output_html">
        <script type="text/javascript">
        window.PlotlyConfig = {MathJaxConfig: 'local'};
        if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
        if (typeof require !== 'undefined') {
        require.undef("plotly");
        requirejs.config({
            paths: {
                'plotly': ['https://cdn.plot.ly/plotly-latest.min']
            }
        });
        require(['plotly'], function(Plotly) {
            window._Plotly = Plotly;
        });
        }
        </script>
        
</div>

</div>
</div>
</div>



* 데이터 생성



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
df = pd.DataFrame(np.random.random([100,3]) * 10)
df.columns = ['Feature1','Feature2','Feature3']
df.head()

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">



<div markdown="0" class="output output_html">
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
      <th>Feature1</th>
      <th>Feature2</th>
      <th>Feature3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.943178</td>
      <td>2.259871</td>
      <td>7.119379</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.891338</td>
      <td>5.817663</td>
      <td>9.930809</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9.270286</td>
      <td>6.894064</td>
      <td>2.587213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.790515</td>
      <td>5.753323</td>
      <td>9.205287</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.967431</td>
      <td>0.057045</td>
      <td>3.039201</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
@interact
def show_data_more_than(column=['Feature2','Feature3'], 
                        x=(0,10,1)):
    return df.loc[df[column] > x]

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_data_text}
```
interactive(children=(Dropdown(description='column', options=('Feature2', 'Feature3'), value='Feature2'), IntS…
```

</div>
</div>
</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
@interact
def scatter_plot(x=list(df.select_dtypes('number').columns), 
                 y=list(df.select_dtypes('number').columns),
                 theme=list(cf.themes.THEMES.keys()), 
                 colorscale=list(cf.colors._scales_names.keys())):
    
    
    if x.title() == y.title():
        print('Can Not Use Same Value')
    else:
        title=f'{y.title()} vs {x.title()}'
        df.iplot(kind='scatter', x=x, y=y, mode='markers', 
                 xTitle=x.title(), yTitle=y.title(), 
                 #text='title',
                 title=f'{y.title()} vs {x.title()}',
                theme=theme, colorscale=colorscale)

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_data_text}
```
interactive(children=(Dropdown(description='x', options=('Feature1', 'Feature2', 'Feature3'), value='Feature1'…
```

</div>
</div>
</div>

