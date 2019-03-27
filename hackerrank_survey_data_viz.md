

![Hackerrank-code-like-a-girl](https://camo.githubusercontent.com/bcb153b5a4eaa2bf3f97776188c6d0d9f2ff6ce5/68747470733a2f2f64336b65757a6562326372686b6e2e636c6f756466726f6e742e6e65742f6861636b657272616e6b2f6173736574732f7374796c6567756964652f6c6f676f5f776f72646d61726b2d66356335656236316162306131353463336564396564613234643062396533312e737667)

Hackerrank is a programming community platform for coders ! It helds competition and programming challenges to brush up/hone coding skills in various languages  (including Java, C++, PHP, Python, SQL, JavaScript)  ! Not unlike Kaggle which is focused on Data Scientist/Machine Learning engineers, Hackerrank is a good way to practice and show your skills to potential employers.
It is part of the growing gamification trend within competitive computer programming. We could ask ourselves what insights about women in tech the data provided by Hackerrank survey reveal !

As a young 2017 Graduate in Computer Science and Data Science and Woman in Tech myself, I am curious to see which trends we'll uncover :) Plus, I also wanted to gain more experience in data viz with Python. ^^

**RECAP **
The data set we are releasing here is the full dataset of 25K responses from Hackerrank developer survey, which includes both students and professionals.

**Methodology for the survey **
* A total of 25,090 professional and student developers completed our 10-minute online survey.
* The survey was live from October 16 through November 1, 2017.
* The survey was hosted by SurveyMonkey and we recruited respondents via email from our community of over 3.4 million members and through social media sites.
* We removed responses that were incomplete as well as obvious spam submissions.
* Not every question was shown to every respondent, as some questions were specifically for those involved in hiring. The codebook (HackerRank-Developer-Survey-2018-Codebook.csv) highlights under what conditions some questions were shown.
* The Women In Tech 2018 report is based only on the 14K responses from professionals
* Respondents who identified as students (q8Student=1; N=10351) were excluded from this report.
* Respondents who identify as “non-binary” (q3Gender=3; N=76) were excluded from the male-female comparisons.



**Women in Tech**


We know that Women in Tech are a minority, but what is the current situation in the past years ? More and more countries are putting effort into making women go into tech, has the situation improved from the past ? Let us get more in depth with this quick survey dataset !

![](https://i1.wp.com/nmtechcouncil.org/wp-content/uploads/cover-graphic.jpeg?resize=700%2C367&ssl=1)

Summary

* [Q1 - Which languages are the most popular ?](#Q1)
* [Q2 - Age distribution ?](#Q2)
* [Q3 - At which age do they begin coding, differences between genders ?](#Q2)
* [Q4 - Countries of Respondents ?](#Q3)
* [Q5 - Top countries characteristics - age began coding ?](#Q5)






```python
import os
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('ggplot')
import plotly
import  plotly.offline as py
py.init_notebook_mode(connected=True)
#import plotly.plotly as py
import plotly.graph_objs as go
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



```python
df=pd.read_csv('HackerRank-Developer-Survey-2018-Values.csv', parse_dates=['StartDate','EndDate'])
df_n = pd.read_csv('HackerRank-Developer-Survey-2018-Numeric.csv', parse_dates=['StartDate','EndDate'])
df_women = df[df.q3Gender == 'Female']
df_men = df[df.q3Gender != 'Female']
```

    C:\ProgramData\Anaconda3\lib\site-packages\IPython\core\interactiveshell.py:2717: DtypeWarning:
    
    Columns (10,19,137,138) have mixed types. Specify dtype option on import or set low_memory=False.
    
    C:\ProgramData\Anaconda3\lib\site-packages\IPython\core\interactiveshell.py:2717: DtypeWarning:
    
    Columns (10,19,137,138,250) have mixed types. Specify dtype option on import or set low_memory=False.
    
    


```python
df.shape
```




    (25093, 251)




```python
df = df.dropna(axis=0, how='all')
df.shape
```




    (25092, 251)




```python
#c = 0 
#for i in df.columns : 
#    print(i + " "+ str(c))
#    c+= 1

df.head(1)
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
      <th>RespondentID</th>
      <th>StartDate</th>
      <th>EndDate</th>
      <th>CountryNumeric</th>
      <th>q1AgeBeginCoding</th>
      <th>q2Age</th>
      <th>q3Gender</th>
      <th>q4Education</th>
      <th>q0004_other</th>
      <th>q5DegreeFocus</th>
      <th>...</th>
      <th>q30LearnCodeOther</th>
      <th>q0030_other</th>
      <th>q31Level3</th>
      <th>q32RecommendHackerRank</th>
      <th>q0032_other</th>
      <th>q33HackerRankChallforJob</th>
      <th>q34PositiveExp</th>
      <th>q34IdealLengHackerRankTest</th>
      <th>q0035_other</th>
      <th>q36Level4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6.464454e+09</td>
      <td>2017-10-19 11:51:00</td>
      <td>2017-10-20 12:05:00</td>
      <td>South Korea</td>
      <td>16 - 20 years old</td>
      <td>18 - 24 years old</td>
      <td>Female</td>
      <td>Some college</td>
      <td>NaN</td>
      <td>Computer Science</td>
      <td>...</td>
      <td>Other (please specify)</td>
      <td>datacamp</td>
      <td>num%2 == 0</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>#NULL!</td>
      <td>NaN</td>
      <td>Queue</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 251 columns</p>
</div>



<a id='Q1'></a>
## **Let's explore which languages are the most popular amongst the respondents classified by gender ! **

I will go back to think about this section later...


```python
prog = df[df.columns[139:163]]
prog['Gender'] = df['q3Gender']
prog = prog.dropna(axis=0, how='all')
prog.columns
```

    C:\ProgramData\Anaconda3\lib\site-packages\ipykernel_launcher.py:2: SettingWithCopyWarning:
    
    
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    
    




    Index(['q25LangC', 'q25LangCPlusPlus', 'q25LangJava', 'q25LangPython',
           'q25LangRuby', 'q25LangJavascript', 'q25LangCSharp', 'q25LangGo',
           'q25Scala', 'q25LangPerl', 'q25LangSwift', 'q25LangPascal',
           'q25LangClojure', 'q25LangPHP', 'q25LangHaskell', 'q25LangLua',
           'q25LangR', 'q25LangRust', 'q25LangTypescript', 'q25LangKotlin',
           'q25LangJulia', 'q25LangErlang', 'q25LangOcaml', 'q25LangOther',
           'Gender'],
          dtype='object')




```python
prog[0:5]
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
      <th>q25LangC</th>
      <th>q25LangCPlusPlus</th>
      <th>q25LangJava</th>
      <th>q25LangPython</th>
      <th>q25LangRuby</th>
      <th>q25LangJavascript</th>
      <th>q25LangCSharp</th>
      <th>q25LangGo</th>
      <th>q25Scala</th>
      <th>q25LangPerl</th>
      <th>...</th>
      <th>q25LangLua</th>
      <th>q25LangR</th>
      <th>q25LangRust</th>
      <th>q25LangTypescript</th>
      <th>q25LangKotlin</th>
      <th>q25LangJulia</th>
      <th>q25LangErlang</th>
      <th>q25LangOcaml</th>
      <th>q25LangOther</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>...</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>NaN</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Know</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Will Learn</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>...</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>NaN</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>Will Learn</td>
      <td>Know</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Know</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Female</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>




```python
for i in prog.columns[:-1] :
    print(i + ": "+str(prog[i].isnull().sum()))
```

    q25LangC: 5904
    q25LangCPlusPlus: 6218
    q25LangJava: 3847
    q25LangPython: 3440
    q25LangRuby: 14793
    q25LangJavascript: 4695
    q25LangCSharp: 12500
    q25LangGo: 14665
    q25Scala: 16921
    q25LangPerl: 18456
    q25LangSwift: 16734
    q25LangPascal: 19084
    q25LangClojure: 19958
    q25LangPHP: 12663
    q25LangHaskell: 18584
    q25LangLua: 19888
    q25LangR: 15862
    q25LangRust: 19340
    q25LangTypescript: 16449
    q25LangKotlin: 17186
    q25LangJulia: 20517
    q25LangErlang: 19933
    q25LangOcaml: 20503
    q25LangOther: 24011
    


```python

```


```python
colors = ["blue", "orange", "greyish", "faded green", "dusty purple"]
fig, ax = plt.subplots(figsize=(20,20), ncols=5, nrows=5)
count = 0
times = 0
for i in prog.columns[:-1]:
    #sns.regplot(x='value', y='wage', data=df_melt, ax=axs[count])
    sns.countplot(x=str(i), hue="Gender", data=prog, palette = sns.xkcd_palette(colors), ax=ax[times][count])
    count += 1
    if count == 5 :
        times += 1
        count = 0

    
```

**To be continued**

<a id='Q2'></a>
# Let's see how many women there are and the age distribution for both. The AgeBeginCoding value might also be interesting 


```python
trace1 = go.Bar(
    x=df_men['q2Age'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_men['q2Age'].value_counts().tolist(),np.sum(df_men['q2Age'].value_counts().tolist())).tolist(),100).tolist(),
    name='Men Respondents'
)
trace2 = go.Bar(
    x=df_women['q2Age'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_women['q2Age'].value_counts().tolist(),np.sum(df_women['q2Age'].value_counts().tolist())).tolist(),100).tolist(),
    name='Female Respondents'
)

data = [trace1, trace2]
layout = go.Layout(
    barmode='group'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='grouped-bar')
```


<div id="9dbf70d4-a0b6-4f05-8f16-fd1a9548c7d7" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("9dbf70d4-a0b6-4f05-8f16-fd1a9548c7d7", [{"type": "bar", "x": ["18 - 24 years old", "25 - 34 years old", "35 - 44 years old", "12 - 18 years old", "45 - 54 years old", "55 - 64 years old", "#NULL!", "Under 12 years old", "65 - 74 years old", "75 years or older"], "y": [48.33078977489508, 34.85310950019077, 10.091568103777185, 3.9536436474628003, 2.0078214421976344, 0.43399465852727964, 0.18599771079740557, 0.05723006486074017, 0.05246089278901182, 0.03338420450209844], "name": "Men Respondents"}, {"type": "bar", "x": ["18 - 24 years old", "25 - 34 years old", "35 - 44 years old", "12 - 18 years old", "45 - 54 years old", "55 - 64 years old", "#NULL!", "Under 12 years old", "75 years or older"], "y": [59.55846676370694, 29.257641921397383, 5.264434740417273, 4.4153323629306165, 1.1402231926249393, 0.26686074721009223, 0.048520135856380396, 0.024260067928190198, 0.024260067928190198], "name": "Female Respondents"}], {"barmode": "group"}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



```python
trace1 = go.Bar(
    x=df_men['q1AgeBeginCoding'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_men['q1AgeBeginCoding'].value_counts().tolist(),np.sum(df_men['q1AgeBeginCoding'].value_counts().tolist())).tolist(),100).tolist(),
    name='Men Respondents'
)
trace2 = go.Bar(
    x=df_women['q1AgeBeginCoding'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_women['q1AgeBeginCoding'].value_counts().tolist(),np.sum(df_women['q1AgeBeginCoding'].value_counts().tolist())).tolist(),100).tolist(),
    name='Female Respondents'
)

data = [trace1, trace2]
layout = go.Layout(
    barmode='group'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='grouped-bar')
```


<div id="3c726772-73c8-4340-bb45-4c0aea380301" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("3c726772-73c8-4340-bb45-4c0aea380301", [{"type": "bar", "x": ["16 - 20 years old", "11 - 15 years old", "21 - 25 years old", "5 - 10 years old", "26 - 30 years old", "31 - 35 years old", "36 - 40 years old", "#NULL!", "41 - 50 years old", "50+ years or older"], "y": [55.494086226631055, 22.391262876764596, 14.388592140404427, 4.111026325829836, 2.4418161007249144, 0.6915299504006105, 0.22892025944296068, 0.12399847386493704, 0.10492178557802365, 0.02384586035864174], "name": "Men Respondents"}, {"type": "bar", "x": ["16 - 20 years old", "21 - 25 years old", "11 - 15 years old", "26 - 30 years old", "5 - 10 years old", "31 - 35 years old", "36 - 40 years old", "41 - 50 years old", "#NULL!", "50+ years or older"], "y": [64.45900048520136, 14.77438136826783, 13.803978651140222, 3.153808830664726, 1.7224648229015043, 1.1644832605531297, 0.4609412906356138, 0.2911208151382824, 0.09704027171276079, 0.0727802037845706], "name": "Female Respondents"}], {"barmode": "group"}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


## We can see that women tend to learn later on compared to men, especially regarding the "11-15 years-old" (22% for men and 13.8% for women) begineers category. More than the half of women learn between 16-20 years old. 


```python
#df['time']=(df['EndDate']-df['StartDate']).astype('timedelta64[m]')

```

<a id='Q3'></a>
# Let's draw a global map to see from where are the majority of our respondents


```python
focus_country = df['CountryNumeric'].value_counts().to_frame()
print("our TOP 10 country respondents is :") 
print(focus_country.head(10).index)
```

    our TOP 10 country respondents is :
    Index(['Ghana', 'India', 'United States', 'Sudan', 'Malaysia', 'Brazil',
           'Russian Federation', 'United Kingdom', 'Canada', 'Indonesia'],
          dtype='object')
    


```python
data = [ dict(
        type = 'choropleth',
        locations = focus_country.index,
        locationmode = 'country names',
        z = focus_country['CountryNumeric'],
        text = focus_country['CountryNumeric'],
        colorscale = [[0,"rgb(5, 10, 172)"],[0.35,"rgb(40, 60, 190)"],[0.5,"rgb(70, 100, 245)"],\
            [0.6,"rgb(90, 120, 245)"],[0.7,"rgb(106, 137, 247)"],[1,"rgb(220, 220, 220)"]],
        autocolorscale = False,
        reversescale = True,
        marker = dict(
            line = dict (
                color = 'rgb(180,180,180)',
                width = 1
            ) ),
        colorbar = dict(
            autotick = False,
            tickprefix = '',
            title = 'Respondents'),
      ) ]

layout = dict(
    title = 'Number of respondents by country',
    geo = dict(
        showframe = True,
        showcoastlines = True,
        projection = dict(
            type = 'Mercator'
        )
    )
)

fig = dict( data=data, layout=layout )
py.iplot( fig, validate=False, filename='d3-world-map' )
```


<div id="8c28ea43-13f2-45ac-b3d6-506639763abe" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("8c28ea43-13f2-45ac-b3d6-506639763abe", [{"type": "choropleth", "locations": ["Ghana", "India", "United States", "Sudan", "Malaysia", "Brazil", "Russian Federation", "United Kingdom", "Canada", "Indonesia", "Poland", "Netherlands", "Mexico", "Spain", "Germany", "Sri Lanka", "Turkey", "Guatemala", "Philippines", "Egypt", "Ukraine", "France", "Romania", "Australia", "South Korea", "Italy", "Azerbaijan", "Hungary", "Argentina", "Republic of Moldova", "Portugal", "Singapore", "Colombia", "Somalia", "Taiwan", "Nigeria", "Bulgaria", "Bangladesh", "Pakistan", "Belize", "Israel", "South Africa", "Vietnam", "Cyprus", "Montenegro", "Sweden", "Palestine", "Chile", "Greece", "Belarus", "Dominican Republic", "Asia/Pacific Region", "New Zealand", "Czech Republic", "Ireland", "Hong Kong", "Latvia", "Panama", "Switzerland", "Peru", "Finland", "Lithuania", "Denmark", "Iran", "Serbia", "Kenya", "Japan", "Slovakia", "Cambodia", "Austria", "Croatia", "Malta", "Qatar", "Kazakhstan", "Republic of Lithuania", "Venezuela", "Cote D'Ivoire", "Belgium", "Macedonia", "China", "Bolivia", "Maldives", "Algeria", "Nepal", "Norway", "Palestinian Territory", "Estonia", "Cameroon", "Senegal", "Mauritius", "Thailand", "Costa Rica", "Chennai", "United Arab Emirates", "Armenia", "Morocco", "Mongolia", "Slovenia", "Ecuador", "El Salvador", "Cuba", "Jordan", "Puerto Rico", "Uruguay", "Barbados", "Tunisia", "Kuwait", "Albania", "Haiti", "Papua New Guinea", "CN", "Luxembourg", "Jamaica", "Uganda", "Europe", "Georgia", "Paraguay", "Bosnia and Herzegovina", "Uzbekistan", "Moldova", "Lebanon", "Ethiopia", "Oman", "Syrian Arab Republic", "Swaziland", "Zimbabwe", "Libya", "Madagascar", "Saudi Arabia", "Honduras", "Nigerian", "Namibia", "Tanzania", "Macedonia, The Former Yugoslav Republic of", "Andorra", "Guinea", "Kosovo", "Afghanistan", "British Indian Ocean Territory"], "locationmode": "country names", "z": [4402, 3734, 3186, 1753, 1120, 766, 371, 326, 311, 233, 202, 186, 184, 173, 170, 168, 167, 163, 153, 149, 143, 130, 124, 122, 112, 110, 109, 109, 106, 96, 95, 92, 89, 84, 83, 80, 80, 79, 78, 74, 73, 70, 67, 64, 63, 60, 59, 57, 55, 55, 53, 53, 52, 51, 50, 49, 48, 40, 39, 38, 37, 36, 35, 34, 33, 32, 32, 32, 31, 30, 30, 29, 28, 27, 26, 26, 26, 26, 25, 25, 24, 23, 22, 22, 22, 20, 19, 19, 18, 17, 17, 17, 14, 14, 14, 14, 13, 13, 12, 12, 11, 10, 10, 9, 9, 9, 8, 8, 8, 8, 7, 7, 7, 6, 6, 6, 6, 6, 6, 5, 5, 5, 5, 4, 4, 3, 3, 3, 3, 3, 3, 3, 2, 2, 2, 2, 2, 2, 2], "text": [4402, 3734, 3186, 1753, 1120, 766, 371, 326, 311, 233, 202, 186, 184, 173, 170, 168, 167, 163, 153, 149, 143, 130, 124, 122, 112, 110, 109, 109, 106, 96, 95, 92, 89, 84, 83, 80, 80, 79, 78, 74, 73, 70, 67, 64, 63, 60, 59, 57, 55, 55, 53, 53, 52, 51, 50, 49, 48, 40, 39, 38, 37, 36, 35, 34, 33, 32, 32, 32, 31, 30, 30, 29, 28, 27, 26, 26, 26, 26, 25, 25, 24, 23, 22, 22, 22, 20, 19, 19, 18, 17, 17, 17, 14, 14, 14, 14, 13, 13, 12, 12, 11, 10, 10, 9, 9, 9, 8, 8, 8, 8, 7, 7, 7, 6, 6, 6, 6, 6, 6, 5, 5, 5, 5, 4, 4, 3, 3, 3, 3, 3, 3, 3, 2, 2, 2, 2, 2, 2, 2], "colorscale": [[0, "rgb(5, 10, 172)"], [0.35, "rgb(40, 60, 190)"], [0.5, "rgb(70, 100, 245)"], [0.6, "rgb(90, 120, 245)"], [0.7, "rgb(106, 137, 247)"], [1, "rgb(220, 220, 220)"]], "autocolorscale": false, "reversescale": true, "marker": {"line": {"color": "rgb(180,180,180)", "width": 1}}, "colorbar": {"autotick": false, "tickprefix": "", "title": "Respondents"}}], {"title": "Number of respondents by country", "geo": {"showframe": true, "showcoastlines": true, "projection": {"type": "Mercator"}}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Source here : https://plot.ly/python/choropleth-maps/

### **It's surprising to see Ghana winning the race, a map of beginning of code per country would be useful to see if every country needs to put on efforts (?) I will also explore the career/ school degrees and specialty of the individuals #To follow**

<a id='Q5'></a>
## **Let's see the age at which the top countries respondents learned to code **


```python
df_men_c = [0,0,0]
df_women_c = [0,0,0]
count = 0
for i in focus_country.head(3).index : 
    df_men_c[count] = df_men[df_men['CountryNumeric'] == i]
    df_women_c[count] = df_women[df_women['CountryNumeric'] == i]
    print('N° of Male respondents for '+ i + ' is : '+ str(df_men_c[count].shape[0]))
    print('N° of Female respondents for '+ i + ' is : '+ str(df_women_c[count].shape[0]))
    
    trace1 = go.Bar( 
    x=df_men_c[count]['q1AgeBeginCoding'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_men_c[count]['q1AgeBeginCoding'].value_counts().tolist(),np.sum(df_men_c[count]['q1AgeBeginCoding'].value_counts().tolist())).tolist(),100).tolist(),
    name='Men Respondents in '+i
    )
    trace2 = go.Bar(
    x=df_women_c[count]['q1AgeBeginCoding'].value_counts().index.tolist(),
    y=np.multiply(np.divide(df_women_c[count]['q1AgeBeginCoding'].value_counts().tolist(),np.sum(df_women_c[count]['q1AgeBeginCoding'].value_counts().tolist())).tolist(),100).tolist(),
    name='Female Respondents in '+i
    )

    data = [trace1, trace2]
    layout = go.Layout(
        barmode='group'
    )

    fig = go.Figure(data=data, layout=layout)
    py.iplot(fig, filename='grouped-bar')
    count = count + 1

```

    N° of Male respondents for Ghana is : 3510
    N° of Female respondents for Ghana is : 892
    


<div id="5a38aefd-dce5-47d5-b965-f6acda592aa0" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("5a38aefd-dce5-47d5-b965-f6acda592aa0", [{"type": "bar", "x": ["16 - 20 years old", "11 - 15 years old", "21 - 25 years old", "5 - 10 years old", "#NULL!", "26 - 30 years old", "36 - 40 years old", "31 - 35 years old"], "y": [77.43589743589745, 15.669515669515668, 5.954415954415954, 0.6267806267806267, 0.11396011396011395, 0.08547008547008547, 0.056980056980056974, 0.056980056980056974], "name": "Men Respondents in Ghana"}, {"type": "bar", "x": ["16 - 20 years old", "11 - 15 years old", "21 - 25 years old", "5 - 10 years old", "#NULL!", "26 - 30 years old", "31 - 35 years old", "36 - 40 years old"], "y": [83.5201793721973, 11.434977578475337, 4.0358744394618835, 0.336322869955157, 0.2242152466367713, 0.2242152466367713, 0.11210762331838565, 0.11210762331838565], "name": "Female Respondents in Ghana"}], {"barmode": "group"}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


    N° of Male respondents for India is : 3167
    N° of Female respondents for India is : 567
    


<div id="247584ce-b925-415c-9683-f26d87e8711b" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("247584ce-b925-415c-9683-f26d87e8711b", [{"type": "bar", "x": ["16 - 20 years old", "21 - 25 years old", "11 - 15 years old", "26 - 30 years old", "5 - 10 years old", "31 - 35 years old", "36 - 40 years old", "41 - 50 years old", "50+ years or older", "#NULL!"], "y": [59.55162614461636, 26.870855699400064, 10.451531417745501, 1.6735080517840228, 1.1682980738869593, 0.0947268708556994, 0.06315124723713293, 0.06315124723713293, 0.031575623618566466, 0.031575623618566466], "name": "Men Respondents in India"}, {"type": "bar", "x": ["16 - 20 years old", "21 - 25 years old", "11 - 15 years old", "26 - 30 years old", "5 - 10 years old", "31 - 35 years old", "41 - 50 years old"], "y": [63.66843033509701, 25.749559082892414, 8.289241622574956, 1.0582010582010581, 0.7054673721340388, 0.3527336860670194, 0.1763668430335097], "name": "Female Respondents in India"}], {"barmode": "group"}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


    N° of Male respondents for United States is : 2640
    N° of Female respondents for United States is : 546
    


<div id="eac0c6a8-ef8d-46cc-89b0-3dbd54fa8501" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("eac0c6a8-ef8d-46cc-89b0-3dbd54fa8501", [{"type": "bar", "x": ["16 - 20 years old", "11 - 15 years old", "21 - 25 years old", "5 - 10 years old", "26 - 30 years old", "31 - 35 years old", "36 - 40 years old", "41 - 50 years old", "#NULL!", "50+ years or older"], "y": [43.29545454545455, 25.757575757575758, 16.28787878787879, 6.0606060606060606, 5.681818181818182, 1.893939393939394, 0.4924242424242424, 0.3787878787878788, 0.11363636363636363, 0.03787878787878788], "name": "Men Respondents in United States"}, {"type": "bar", "x": ["16 - 20 years old", "21 - 25 years old", "11 - 15 years old", "26 - 30 years old", "31 - 35 years old", "5 - 10 years old", "41 - 50 years old", "36 - 40 years old", "50+ years or older"], "y": [47.8021978021978, 21.611721611721613, 13.91941391941392, 8.424908424908425, 3.47985347985348, 2.380952380952381, 1.098901098901099, 0.9157509157509158, 0.3663003663003663], "name": "Female Respondents in United States"}], {"barmode": "group"}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


We observe that most people learn to code between 16 and 20 years old. However, we also notice that in India the 2nd most represented group of beginners is 21-25 years old ! that is not the case in Ghana and USA where 2nd most seems to be 11-15 years. however girls are underrepresented in the USA for the 11-15 years old category. Maybe USA and India should put effort to make them learn to code earlier ?

## Let's see if people who started to code continued. to be continued :) Don't hesitate to comment and upvote if you liked this kernel !


```python

```
