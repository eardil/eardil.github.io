---
layout:     post
title:      "Pandas time!"
subtitle:   "On data and visualization"
date:       2015-08-26 12:00:00
author:     "Eardil"
header-img: "img/post-bg-01.jpg"
---
Before I move on to trying more complicated things that I would do with MATLAB (e.g. 3D plotting), I want to learn the basics of the thing I would like to do on R, namely data crunching and visualization. 

For that I will use [mtcars](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html) database because:
* It's simple.
* It's standard.
* [Flowers](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/iris.html) are boring.
* Saddly, there's no simple, standard, motorcycles database.

So first I need to load the `Pandas` library. This library will introduce the `DataFrame` object much like R's own `data.frame`.

{% highlight python %}
import pandas as pd
{% endhighlight %}

There's a package that brings RDatasets to Python, but I saved mtcars as a CSV (comma separated values) file because reading my own data from Python is a very important step. Which by the way is very easy:

{% highlight python %}
cars = pd.read_csv("mtcars.csv")
{% endhighlight %}

To print what I just read, there's a `head` function. It will shows us the first bunch of rows. `head(n)` will give you the first `n` rows, but let's use the default.

{% highlight python %}
cars.head()
{% endhighlight %}



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
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
      <td>160</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.620</td>
      <td>16.46</td>
      <td>0</td>
      <td>Manual</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mazda RX4 Wag</td>
      <td>21.0</td>
      <td>6</td>
      <td>160</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.875</td>
      <td>17.02</td>
      <td>0</td>
      <td>Manual</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Datsun 710</td>
      <td>22.8</td>
      <td>4</td>
      <td>108</td>
      <td>93</td>
      <td>3.85</td>
      <td>2.320</td>
      <td>18.61</td>
      <td>1</td>
      <td>Manual</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hornet 4 Drive</td>
      <td>21.4</td>
      <td>6</td>
      <td>258</td>
      <td>110</td>
      <td>3.08</td>
      <td>3.215</td>
      <td>19.44</td>
      <td>1</td>
      <td>Automatic</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hornet Sportabout</td>
      <td>18.7</td>
      <td>8</td>
      <td>360</td>
      <td>175</td>
      <td>3.15</td>
      <td>3.440</td>
      <td>17.02</td>
      <td>0</td>
      <td>Automatic</td>
      <td>3</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



We can see that there's no name for the first column. We could add a name like "carname", but in this case the name of the car represents a single row, so maybe we should use it as a name for the row instead of just $1,2,3,\dots$

{% highlight python %}
cars = pd.read_csv("mtcars.csv",index_col=0)
cars.head()
{% endhighlight %}



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
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
      <th>Mazda RX4</th>
      <td>21.0</td>
      <td>6</td>
      <td>160</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.620</td>
      <td>16.46</td>
      <td>0</td>
      <td>Manual</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Mazda RX4 Wag</th>
      <td>21.0</td>
      <td>6</td>
      <td>160</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.875</td>
      <td>17.02</td>
      <td>0</td>
      <td>Manual</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Datsun 710</th>
      <td>22.8</td>
      <td>4</td>
      <td>108</td>
      <td>93</td>
      <td>3.85</td>
      <td>2.320</td>
      <td>18.61</td>
      <td>1</td>
      <td>Manual</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Hornet 4 Drive</th>
      <td>21.4</td>
      <td>6</td>
      <td>258</td>
      <td>110</td>
      <td>3.08</td>
      <td>3.215</td>
      <td>19.44</td>
      <td>1</td>
      <td>Automatic</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Hornet Sportabout</th>
      <td>18.7</td>
      <td>8</td>
      <td>360</td>
      <td>175</td>
      <td>3.15</td>
      <td>3.440</td>
      <td>17.02</td>
      <td>0</td>
      <td>Automatic</td>
      <td>3</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



If you happen to know the dataset, you'll notice that I changed the variable `am` from binary to text. I did this to explore `pandas` use of categorical data from text.

Speaking of that, let's see how the data was saved in our variable.

{% highlight python %}
cars.info()
{% endhighlight %}

    <class 'pandas.core.frame.DataFrame'>
    Index: 32 entries, Mazda RX4 to Volvo 142E
    Data columns (total 11 columns):
    mpg     32 non-null float64
    cyl     32 non-null int64
    disp    32 non-null float64
    hp      32 non-null int64
    drat    32 non-null float64
    wt      32 non-null float64
    qsec    32 non-null float64
    vs      32 non-null int64
    am      32 non-null object
    gear    32 non-null int64
    carb    32 non-null int64
    dtypes: float64(5), int64(5), object(1)
    memory usage: 3.0+ KB
    

We can see some important data on the...data (Metadata?). How each variable is stored and the memory size of the DataFrame. This is a *really* small dataset, but with bigger files this would be more and more important to be aware of.

Other function that seems very useful is `describe`, which summarizes the columns in the most standard statistics: count,mean, standard deviation and quartiles.

{% highlight python %}
cars.describe()
{% endhighlight %}



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mpg</th>
      <th>cyl</th>
      <th>disp</th>
      <th>hp</th>
      <th>drat</th>
      <th>wt</th>
      <th>qsec</th>
      <th>vs</th>
      <th>gear</th>
      <th>carb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.0000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>20.090625</td>
      <td>6.187500</td>
      <td>230.721875</td>
      <td>146.687500</td>
      <td>3.596563</td>
      <td>3.217250</td>
      <td>17.848750</td>
      <td>0.437500</td>
      <td>3.687500</td>
      <td>2.8125</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.026948</td>
      <td>1.785922</td>
      <td>123.938694</td>
      <td>68.562868</td>
      <td>0.534679</td>
      <td>0.978457</td>
      <td>1.786943</td>
      <td>0.504016</td>
      <td>0.737804</td>
      <td>1.6152</td>
    </tr>
    <tr>
      <th>min</th>
      <td>10.400000</td>
      <td>4.000000</td>
      <td>71.100000</td>
      <td>52.000000</td>
      <td>2.760000</td>
      <td>1.513000</td>
      <td>14.500000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>1.0000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>15.425000</td>
      <td>4.000000</td>
      <td>120.825000</td>
      <td>96.500000</td>
      <td>3.080000</td>
      <td>2.581250</td>
      <td>16.892500</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>2.0000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>19.200000</td>
      <td>6.000000</td>
      <td>196.300000</td>
      <td>123.000000</td>
      <td>3.695000</td>
      <td>3.325000</td>
      <td>17.710000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>2.0000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>22.800000</td>
      <td>8.000000</td>
      <td>326.000000</td>
      <td>180.000000</td>
      <td>3.920000</td>
      <td>3.610000</td>
      <td>18.900000</td>
      <td>1.000000</td>
      <td>4.000000</td>
      <td>4.0000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>33.900000</td>
      <td>8.000000</td>
      <td>472.000000</td>
      <td>335.000000</td>
      <td>4.930000</td>
      <td>5.424000</td>
      <td>22.900000</td>
      <td>1.000000</td>
      <td>5.000000</td>
      <td>8.0000</td>
    </tr>
  </tbody>
</table>
</div>



As a shortcut for visualization, there's another cool feature of pandas: we can call plot directly to the DataFrame. This allows to plot a histogram (or whatever) of some columns directly to see what we are doing. For this we need the plotting library. 

{% highlight python %}
import matplotlib.pyplot as plt
%matplotlib inline
{% endhighlight %}

To select a single column of our data, pandas uses `[]`. So for example we can get the `mpg` variable and get the histogram right out of the DataFrame object with:

{% highlight python %}
cars['mpg'].hist()
plt.show()


![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_15_0.png)


Now we can visualize some `pandas` functionality. For example, we can easily group by type of transmission using the `groupby` function. I take cars, select the columns 'mpg' and 'am', then apply the `groupby` function to tell `pandas` I want to group by 'am', and that I want to summarize the rest using the function mean. Finally I plot it.

{% highlight python %}
cars[['am','mpg']].groupby('am').mean().plot(kind='bar')
plt.show()
{% endhighlight %}

![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_17_0.png)


How about a scatter plot? Maybe I would want to see the relationship between miles per gallon vs the horse power.

{% highlight python %}
plt.scatter(cars['mpg'],cars['hp'])
plt.show()
{% endhighlight %}

![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_19_0.png)


### What about beautiful plots?

By this time some may be missing ggplot because of its elegant style. Well, matplotlib has different possible styles, included the beloved ggplot, only by setting `style.use`

{% highlight python %}
plt.style.use('ggplot')
plt.scatter(cars['mpg'],cars['hp'])
plt.show()
{% endhighlight %}

![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_21_0.png)


There is also another library called `seaborn` that brings new styles to matplotlib and more visualization functions. It doesn't come with the Anaconda distribution, but it's really easy to get. You just open a terminal (cmd/powershell on windows), type `conda install seaborn` and you're done. Now you just load it to get more beautiful plots and can begin to use fun plots like the `regplot`, which performs linear regression directly in the plot. Plot, plot. I'm setting the figure size because seaborn figures come out a little bigger and 

{% highlight python %}
import seaborn as sns
plt.figure(figsize=(5, 4))

sns.regplot('mpg','hp',data=cars)
{% endhighlight %}



    <matplotlib.axes._subplots.AxesSubplot at 0xc96cc88>




![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_23_1.png)


The dependence doesn't seem to be linear, let's try a polinomial regression.

{% highlight python %}
plt.figure(figsize=(5, 4))
sns.regplot('mpg','hp',data=cars,order=2)
{% endhighlight %}



    <matplotlib.axes._subplots.AxesSubplot at 0xc679908>




![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_25_1.png)


One of the things I didn't like about R, or more specifically R on Windows, is that plots don't seem to have any anti-aliasing. I haven't had that problem in Python, although you wouldn't notice anyway since these graphs are all un PNG format now, which would look equally great if I generated them in R. I took a screenshot with an equivalent plot generated in RStudio:

{% highlight R %}
library(ggplot2)

cars <- mtcars

ggplot(data = cars, aes(x=mpg,y=hp)) + geom_point() + 
  stat_smooth(method="lm",formula = y ~ poly(x,2,raw=TRUE))
{% endhighlight %}

![ew](http://eardil.github.io/img/2015-08-26-pandas-time_files/Rsmooth.png)

*Look at that horrible line!*

If you have a workaround for turning on antialiasing on R for Windows I would very much appreciate it, since I've searched hungrily for it.

There's a ggplot library for Python too, although I read that it is a little buggy still. It would be really convenient to use the same graphic language when moving between Python and R. I needed to install it too by running `pip install ggplot` in the terminal. Notice that the `gsize` variable is just format and it's not necessary.

{% highlight python %}
from ggplot import *
gsize = theme_matplotlib(rc={"figure.figsize": "5, 4"}, matplotlib_defaults=False)

ggplot(aes(x='mpg',y='hp'),data = cars) + geom_point() + gsize
{% endhighlight %}

![png](http://eardil.github.io/img/2015-08-26-pandas-time_files/2015-08-26-pandas-time_27_0.png)





    <ggplot: (-9223372036841740621)>



I dropped the `stat_smooth` because there's no way to specify the model yet, apparently. Anyway there it is.

---

Remember that you can get this [IPython Notebook](https://github.com/eardil/Blog_Code/blob/master/2015-08-26-pandas-time/2015-08-26-pandas-time.ipynb) and others at my [Github Page](https://github.com/eardil).