---
redirect_from:
  - "/database/filmbase"
interact_link: content/database/FilmBase.ipynb
kernel_name: python3
has_widgets: false
title: 'The Film Database'
prev_page:
  url: /features/notebooks
  title: 'Jupyter notebooks'
next_page:
  url: 
  title: ''
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---


## Read File and Create Database



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
import os
import tkinter as tk
from tkinter import *
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

os.chdir("/Users/CzarStephen/Desktop/Program/FilmBase")

data = pd.read_csv("FilmData.csv")

```
</div>

</div>



## Add to File



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def addRow():
    global newData
    movieTitle = str(title.get())
    movieYear = int(year.get())
    
    movieSeen = str(seen.get())
    if movieSeen == "True":
        movieSeen = True
    else:
        movieSeen = False
    
    movieLastSeen = int(lastSeen.get())
    movieGenre = str(genre.get())
    movieDirs = str(dirs.get())
    movieDirs = movieDirs.replace(', ', '][')
    
    movieFav = str(favs.get())
    if movieFav == "True":
        movieFav = True
    else:
        movieFav = False
    
    row = {'Title' : movieTitle, 'Year' : movieYear, 'Seen' : movieSeen, 'Last Seen' : movieLastSeen, 'Genre' : movieGenre, 'Directors' : '[' + str(movieDirs) + ']', 'Favorite' : movieFav }
    newRow = pd.Series(data = row)
    newData = data.append(row, ignore_index=True)
    
    print("Added " + movieTitle + " (" + str(movieYear) + ") to the dataset")


```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
window = tk.Tk()

window.title("Filmbase GUI: Yipee")
window.resizable(False, False)

Label(window, text = 'Title').grid(row = 0)
Label(window, text = 'Year').grid(row = 1)
Label(window, text = 'Seen (True/False)').grid(row = 2)
Label(window, text = 'Last Seen (Year)').grid(row = 3)
Label(window, text = 'Genre').grid(row = 4)
Label(window, text = 'Director(s)').grid(row = 5)
Label(window, text = 'Favorite').grid(row = 6)

title = Entry(window)
year = Entry(window)
seen = Entry(window)
lastSeen = Entry(window)
genre = Entry(window)
dirs = Entry(window)
favs = Entry(window)

Button(window, text = 'submit', command = addRow).grid(row = 7)

title.grid(row = 0, column = 1)
year.grid(row = 1, column = 1)
seen.grid(row = 2, column = 1)
lastSeen.grid(row = 3, column = 1)
genre.grid(row = 4, column = 1)
dirs.grid(row = 5, column = 1)
favs.grid(row = 6, column = 1)

window.call('wm', 'attributes', '.', '-topmost', '1')
window.mainloop()

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_stream}
```
Added Jojo Rabbit (2019) to the dataset
```
</div>
</div>
</div>



### Save Data



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
data = newData
data.to_csv(path_or_buf = "/Users/CzarStephen/Desktop/Program/FilmBase/FilmData.csv", index = False)
data.tail()

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
      <th>Title</th>
      <th>Year</th>
      <th>Seen</th>
      <th>Last Seen</th>
      <th>Genre</th>
      <th>Directors</th>
      <th>Favorite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>397</th>
      <td>Uncut Gems</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Crime</td>
      <td>[Josh Safdie][Benny Safdie]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>398</th>
      <td>The Rise of Skywalker</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>SciFi/Fantasy</td>
      <td>[J.J. Abrams]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>399</th>
      <td>Spies in Disguise</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Animation/Spy</td>
      <td>[Nick Bruno][Troy Quane]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>400</th>
      <td>Cats</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Musical</td>
      <td>[Tom Hooper]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>401</th>
      <td>Jojo Rabbit</td>
      <td>2019</td>
      <td>True</td>
      <td>2020</td>
      <td>Comedy/Period</td>
      <td>[Taika Waititi]</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



***
## Functions
***



##### Get Watchlist



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
toWatch = data[data['Seen'] == False]
print('Length of Watchlist: ' + str(len(toWatch)))
toWatch

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_stream}
```
Length of Watchlist: 51
```
</div>
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
      <th>Title</th>
      <th>Year</th>
      <th>Seen</th>
      <th>Last Seen</th>
      <th>Genre</th>
      <th>Directors</th>
      <th>Favorite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>Minions</td>
      <td>2015</td>
      <td>False</td>
      <td>0</td>
      <td>Animation</td>
      <td>[Kyle Balda][Pierre Coffin]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Do the Right Thing</td>
      <td>1989</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Spike Lee]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>75</th>
      <td>The Holy Mountain</td>
      <td>1973</td>
      <td>False</td>
      <td>0</td>
      <td>Fantasy</td>
      <td>[Alejandro Jodorowsky]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Ocean's Thirteen</td>
      <td>2007</td>
      <td>False</td>
      <td>0</td>
      <td>Crime</td>
      <td>[Steven Soderbergh]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Climax</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Gaspar Noé]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Anomalisa</td>
      <td>2015</td>
      <td>False</td>
      <td>0</td>
      <td>Animation</td>
      <td>[Duke Johnson][Charlie Kaufman]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>177</th>
      <td>The Nightmare Before Christmas</td>
      <td>1993</td>
      <td>False</td>
      <td>0</td>
      <td>Christmas/Animation</td>
      <td>[Henry Selick]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>185</th>
      <td>Lady Bird</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Greta Gerwig]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>188</th>
      <td>Barry Lyndon</td>
      <td>1975</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Period</td>
      <td>[Stanley Kubrick]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>189</th>
      <td>Full Metal Jacket</td>
      <td>1987</td>
      <td>False</td>
      <td>0</td>
      <td>War</td>
      <td>[Stanley Kubrick]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>190</th>
      <td>Lolita</td>
      <td>1962</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Stanley Kubrick]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>194</th>
      <td>Phantom Thread</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Paul Thomas Anderson]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>195</th>
      <td>Boogie Nights</td>
      <td>1997</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Comedy</td>
      <td>[Paul Thomas Anderson]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Punch-Drunk Love</td>
      <td>2002</td>
      <td>False</td>
      <td>0</td>
      <td>Romance/Thriller</td>
      <td>[Paul Thomas Anderson]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Shame</td>
      <td>2011</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Steve McQueen]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>208</th>
      <td>Enemy</td>
      <td>2013</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery/Thriller</td>
      <td>[Denis Villeneuve]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>209</th>
      <td>Prisoners</td>
      <td>2013</td>
      <td>False</td>
      <td>0</td>
      <td>Crime/Thriller</td>
      <td>[Denis Villeneuve]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>210</th>
      <td>Taxi Driver</td>
      <td>1976</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery/Crime</td>
      <td>[Martin Scorsese]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>217</th>
      <td>Hunt for the Wilderpeople</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Adventure</td>
      <td>[Taika Waititi]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>220</th>
      <td>The Handmaiden</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Thriller</td>
      <td>[Park Chan-wook]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>229</th>
      <td>Burning</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery/Drama</td>
      <td>[Lee Chang-dong]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>234</th>
      <td>Thoroughbreds</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Thriller</td>
      <td>[Cory Finley]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>235</th>
      <td>Suspiria</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Horror/Fantasy</td>
      <td>[Luca Guadagnino]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>236</th>
      <td>The Sisters Brothers</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Western/Crime</td>
      <td>[Jacques Audiard]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>237</th>
      <td>Mid90s</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Comedy</td>
      <td>[Jonah Hill]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>238</th>
      <td>Blindspotting</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Comedy</td>
      <td>[Carlos López Estrada]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>239</th>
      <td>American Animals</td>
      <td>2018</td>
      <td>False</td>
      <td>0</td>
      <td>Crime</td>
      <td>[Bart Layton]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>273</th>
      <td>A Ghost Story</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[David Lowery]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>274</th>
      <td>Brawl in Cell Block 99</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Mystery</td>
      <td>[S. Craig Zahler]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>275</th>
      <td>Colossal</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Fantasy</td>
      <td>[Nacho Vigalondo]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>276</th>
      <td>The Big Sick</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Romance/Comedy</td>
      <td>[Michael Showalter]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>277</th>
      <td>I Don’t Feel at Home in This World Anymore</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Crime</td>
      <td>[Macon Blair]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>278</th>
      <td>It Comes at Night</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery/Horror</td>
      <td>[Trey Edward Shults]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>279</th>
      <td>Loving Vincent</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Period</td>
      <td>[Dorota Kobiela][Hugh Welchman]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Okja</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>SciFi/Satire</td>
      <td>[Bong Joon-ho]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>282</th>
      <td>Personal Shopper</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery/Drama</td>
      <td>[Olivier Assayas]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>283</th>
      <td>Raw</td>
      <td>2017</td>
      <td>False</td>
      <td>0</td>
      <td>Horror</td>
      <td>[Julia Ducournau]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>284</th>
      <td>Silence</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Period/Drama</td>
      <td>[Martin Scorsese]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>285</th>
      <td>The Nice Guys</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery</td>
      <td>[Shane Black]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>286</th>
      <td>The Neon Demon</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Thriller</td>
      <td>[Nicolas Winding Refn]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>287</th>
      <td>Hail, Caeser!</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery</td>
      <td>[Ethan Coen][Joel Coen]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>288</th>
      <td>Green Room</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Crime/Thriller</td>
      <td>[Jeremy Saulnier]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>289</th>
      <td>Edge of Seventeen</td>
      <td>2016</td>
      <td>False</td>
      <td>0</td>
      <td>Highschool/Comedy</td>
      <td>[Kelly Fremon Craig]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>310</th>
      <td>Tangerine</td>
      <td>2015</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/Crime</td>
      <td>[Sean Baker]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>311</th>
      <td>Son of Saul</td>
      <td>2015</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[László Nemes]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>312</th>
      <td>Room</td>
      <td>2015</td>
      <td>False</td>
      <td>0</td>
      <td>Thriller/Drama</td>
      <td>[Lenny Abrahamson]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>331</th>
      <td>Inherent Vice</td>
      <td>2014</td>
      <td>False</td>
      <td>0</td>
      <td>Mystery</td>
      <td>[Paul Thomas Anderson]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>332</th>
      <td>Foxcatcher</td>
      <td>2014</td>
      <td>False</td>
      <td>0</td>
      <td>Sport/Drama</td>
      <td>[Bennett Miller]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>333</th>
      <td>Boyhood</td>
      <td>2014</td>
      <td>False</td>
      <td>0</td>
      <td>Drama</td>
      <td>[Richard Linklater]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>355</th>
      <td>The Wolf of Wall Street</td>
      <td>2013</td>
      <td>False</td>
      <td>0</td>
      <td>Crime/Comedy</td>
      <td>[Martin Scorsese]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>356</th>
      <td>Upstream Color</td>
      <td>2013</td>
      <td>False</td>
      <td>0</td>
      <td>Drama/SciFi</td>
      <td>[Shane Carruth]</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



##### Get Favorites



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
favorites = data[data['Favorite'] == True]
favorites

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
      <th>Title</th>
      <th>Year</th>
      <th>Seen</th>
      <th>Last Seen</th>
      <th>Genre</th>
      <th>Directors</th>
      <th>Favorite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>2001: A Space Odyssey</td>
      <td>1968</td>
      <td>True</td>
      <td>2016</td>
      <td>SciFi</td>
      <td>[Stanley Kubrick]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Black Dynamite</td>
      <td>2009</td>
      <td>True</td>
      <td>2019</td>
      <td>Comedy</td>
      <td>[Scott Sanders]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Call Me By Your Name</td>
      <td>2017</td>
      <td>True</td>
      <td>2018</td>
      <td>Romance</td>
      <td>[Luca Guadagnino]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Her</td>
      <td>2013</td>
      <td>True</td>
      <td>2015</td>
      <td>Romance</td>
      <td>[Spike Jonze]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Hot Fuzz</td>
      <td>2007</td>
      <td>True</td>
      <td>2018</td>
      <td>Comedy</td>
      <td>[Edgar Wright]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>117</th>
      <td>The Favourite</td>
      <td>2018</td>
      <td>True</td>
      <td>2018</td>
      <td>Drama</td>
      <td>[Yorgos Lanthimos]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>119</th>
      <td>City of God</td>
      <td>2002</td>
      <td>True</td>
      <td>2017</td>
      <td>Crime</td>
      <td>[Fernando Meirelles][Kátia Lund]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>120</th>
      <td>La haine</td>
      <td>1995</td>
      <td>True</td>
      <td>2017</td>
      <td>Crime</td>
      <td>[Mathieu Kassovitz]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>129</th>
      <td>Dr. Strangelove</td>
      <td>1964</td>
      <td>True</td>
      <td>2016</td>
      <td>Satire</td>
      <td>[Stanley Kubrick]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>145</th>
      <td>The Thing</td>
      <td>1982</td>
      <td>True</td>
      <td>2018</td>
      <td>Horror</td>
      <td>[John Carpenter]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>149</th>
      <td>Under the Skin</td>
      <td>2013</td>
      <td>True</td>
      <td>2017</td>
      <td>Horror</td>
      <td>[Jonathan Glazer]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Isle of Dogs</td>
      <td>2018</td>
      <td>True</td>
      <td>2018</td>
      <td>Animation</td>
      <td>[Wes Anderson]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>187</th>
      <td>Children of Men</td>
      <td>2006</td>
      <td>True</td>
      <td>2017</td>
      <td>Drama/SciFi</td>
      <td>[Alfonso Cuarón]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>211</th>
      <td>Spider-Man: Into the Spider-Verse</td>
      <td>2018</td>
      <td>True</td>
      <td>2019</td>
      <td>Comic/Animation</td>
      <td>[Peter Ramsey][Bob Persichetti][Rodney Rothman]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>216</th>
      <td>What We Do in the Shadows</td>
      <td>2014</td>
      <td>True</td>
      <td>2018</td>
      <td>Comedy/Horror</td>
      <td>[Taika Waititi][Jemaine Clement]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>219</th>
      <td>Nocturnal Animals</td>
      <td>2016</td>
      <td>True</td>
      <td>2017</td>
      <td>Drama/Crime</td>
      <td>[Tom Ford]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>281</th>
      <td>Paddington 2</td>
      <td>2017</td>
      <td>True</td>
      <td>2019</td>
      <td>Children/Adventure</td>
      <td>[Paul King]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>365</th>
      <td>Inside Llewyn Davis</td>
      <td>2013</td>
      <td>True</td>
      <td>2018</td>
      <td>Drama</td>
      <td>[Ethan Coen][Joel Coen]</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



##### Search



***
Genres: Thriller|Action|Comedy|Horror|SciFi|Animation|Children|Comic|Adventure|Fantasy|Drama|Crime|Romance|Highschool|Mystery|Blaxpoitation|Satire|Period|War|Documentary|Spy|Biopic|Musical|Suspense
***





<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
search = data[data['Title'].str.contains('Hat')]
search

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
      <th>Title</th>
      <th>Year</th>
      <th>Seen</th>
      <th>Last Seen</th>
      <th>Genre</th>
      <th>Directors</th>
      <th>Favorite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>72</th>
      <td>The Hateful Eight</td>
      <td>2015</td>
      <td>True</td>
      <td>2019</td>
      <td>Period/Mystery</td>
      <td>[Quentin Tarantino]</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



##### Search by Year/Last Seen



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
searchYear = data[data['Year'] == 2019]
searchYear

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
      <th>Title</th>
      <th>Year</th>
      <th>Seen</th>
      <th>Last Seen</th>
      <th>Genre</th>
      <th>Directors</th>
      <th>Favorite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>John Wick: Chapter 3</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Action</td>
      <td>[Chad Stahelski]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Midsommar</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror</td>
      <td>[Ari Aster]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Captain Marvel</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Comic</td>
      <td>[David F. Sandberg]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Avengers: Endgame</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Comic</td>
      <td>[Anthony Russo][Joe Russo]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Booksmart</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Highschool</td>
      <td>[Olivia Wilde]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Spider-Man: Far From Home</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Comic</td>
      <td>[Jon Watts]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Godzilla: King of the Monsters</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Shlock</td>
      <td>[Michael Dougherty]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Avengers: Endgame</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Comic</td>
      <td>[Anthony Russo][Joe Russo]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>162</th>
      <td>Toy Story 4</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Animation</td>
      <td>[Josh Cooley]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>183</th>
      <td>The Lighthouse</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Thriller/Horror</td>
      <td>[Robert Eggers]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>372</th>
      <td>Velvet Buzzsaw</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror/Thriller</td>
      <td>[Dan Gilroy]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>373</th>
      <td>Us</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror</td>
      <td>[Jordan Peele]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>374</th>
      <td>Pet Sematary</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror</td>
      <td>[Kevin Kolsch][Dennis Widmyer]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>378</th>
      <td>Pokémon Detective Pikachu</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Mystery/Children</td>
      <td>[Rob Letterman]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>379</th>
      <td>Aladdin</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Musical/Adventure</td>
      <td>[Guy Ritchie]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>381</th>
      <td>The Art of Self-Defense</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Comedy/Satire</td>
      <td>[Riley Stearns]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>382</th>
      <td>Once Upon a Time In Hollywood</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Drama/Thriller</td>
      <td>[Quentin Tarantino]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>384</th>
      <td>The Farewell</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Drama</td>
      <td>[Lulu Wang]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>385</th>
      <td>Ready or Not</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Mystery/Thriller</td>
      <td>[Matt Bettinelli-Olpin][Tyler Gillett]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>387</th>
      <td>IT Chapter Two</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror</td>
      <td>[Andrés Muschietti]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>388</th>
      <td>Ad Astra</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>SciFi/Drama</td>
      <td>[James Gray]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>391</th>
      <td>Joker</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Drama/Thriller</td>
      <td>[Todd Phillips]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>393</th>
      <td>Parasite</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Mystery</td>
      <td>[Bong Joon-ho]</td>
      <td>True</td>
    </tr>
    <tr>
      <th>395</th>
      <td>Doctor Sleep</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Horror</td>
      <td>[Mike Flanagan]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>396</th>
      <td>Queen &amp; Slim</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Thriller/Drama</td>
      <td>[Melina Matsoukas]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>397</th>
      <td>Uncut Gems</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Crime</td>
      <td>[Josh Safdie][Benny Safdie]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>398</th>
      <td>The Rise of Skywalker</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>SciFi/Fantasy</td>
      <td>[J.J. Abrams]</td>
      <td>False</td>
    </tr>
    <tr>
      <th>399</th>
      <td>Spies in Disguise</td>
      <td>2019</td>
      <td>True</td>
      <td>2019</td>
      <td>Animation/Spy</td>
      <td>[Nick Bruno][Troy Quane]</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
</div>


</div>
</div>
</div>



##### Modify Information



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
data.loc[221, 'Last Seen'] = 2019
data.to_csv(path_or_buf = "/Users/CzarStephen/Desktop/Program/FilmBase/FilmData.csv", index = False)

```
</div>

</div>



***
## Display/Graph Data
***



###### Pie Chart [Total Data]



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
actionCount = len(data[data['Genre'].str.contains('Action')])
scifiCount = len(data[data['Genre'].str.contains('SciFi')])
horrorCount = len(data[data['Genre'].str.contains('Horror')])
dramaCount = len(data[data['Genre'].str.contains('Drama')])
comedyCount = len(data[data['Genre'].str.contains('Comedy')])
romanceCount = len(data[data['Genre'].str.contains('Romance')])

labels = 'Action', 'SciFi', 'Horror', 'Drama', 'Comedy', 'Romance'
sizes = [actionCount, scifiCount, horrorCount, dramaCount, comedyCount, romanceCount]
explode = (0, 0, 0.1, 0, 0, 0)

fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.

plt.show()

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

{:.output_png}
![png](/Users/CzarStephen/Desktop/Program/Film%20Database%20Project/FilmbaseBook/_build/images/database/FilmBase_21_0.png)

</div>
</div>
</div>



##### Pie Chart [Favorites Data]



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
favorite_data = data[data['Favorite'] == True]

actionCount = len(favorite_data[favorite_data['Genre'].str.contains('Action')])
scifiCount = len(favorite_data[favorite_data['Genre'].str.contains('SciFi')])
horrorCount = len(favorite_data[favorite_data['Genre'].str.contains('Horror')])
dramaCount = len(favorite_data[favorite_data['Genre'].str.contains('Drama')])
comedyCount = len(favorite_data[favorite_data['Genre'].str.contains('Comedy')])
romanceCount = len(favorite_data[favorite_data['Genre'].str.contains('Romance')])

labels = 'Action', 'SciFi', 'Horror', 'Drama', 'Comedy', 'Romance'
sizes = [actionCount, scifiCount, horrorCount, dramaCount, comedyCount, romanceCount]
explode = (0, 0, 0.1, 0, 0, 0)

fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.

plt.show()

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

{:.output_png}
![png](/Users/CzarStephen/Desktop/Program/Film%20Database%20Project/FilmbaseBook/_build/images/database/FilmBase_23_0.png)

</div>
</div>
</div>



###### Bar Graph [Movies per Year]



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
objects = ('2014', '2015', '2016', '2017', '2018', '2019')
y_pos = np.arange(len(objects))

data_watched = data[data['Seen'] == True]
data_watchlist = data[data['Seen'] == False]

fourteen_count = len(data_watched[data_watched['Year'] == 2014])
fifteen_count = len(data_watched[data_watched['Year'] == 2015])
sixteen_count = len(data_watched[data_watched['Year'] == 2016])
seventeen_count = len(data_watched[data_watched['Year'] == 2017])
eighteen_count = len(data_watched[data_watched['Year'] == 2018])
nineteen_count = len(data_watched[data_watched['Year'] == 2019])
performance = [fourteen_count, fifteen_count, sixteen_count, seventeen_count, eighteen_count, nineteen_count]

wl_fourteen_count = len(data_watchlist[data_watchlist['Year'] == 2014])
wl_fifteen_count = len(data_watchlist[data_watchlist['Year'] == 2015])
wl_sixteen_count = len(data_watchlist[data_watchlist['Year'] == 2016])
wl_seventeen_count = len(data_watchlist[data_watchlist['Year'] == 2017])
wl_eighteen_count = len(data_watchlist[data_watchlist['Year'] == 2018])
wl_nineteen_count = len(data_watchlist[data_watchlist['Year'] == 2019])
wl_performance = [wl_fourteen_count, wl_fifteen_count, wl_sixteen_count, wl_seventeen_count, wl_eighteen_count, wl_nineteen_count]

p1 = plt.bar(y_pos, performance, alpha=0.5)
p2 = plt.bar(y_pos, wl_performance, bottom = performance, alpha=0.5)

plt.xticks(y_pos, objects)
plt.legend((p1[0], p2[0]), ('Watched', 'On Watchlist'))
plt.ylabel('Number of Movies')
plt.title('Movies Watched By Year')

plt.show()

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

{:.output_png}
![png](/Users/CzarStephen/Desktop/Program/Film%20Database%20Project/FilmbaseBook/_build/images/database/FilmBase_25_0.png)

</div>
</div>
</div>

