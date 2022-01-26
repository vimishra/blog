---
date: "2021-07-16T11:46:36+05:30"
draft: false
title: "Plotting With Matplotlib"

---

[Matplotlib](https://www.wikiwand.com/en/Matplotlib) is the defacto Python
plotting library. The library was designed to look as similar to Matlab as
possible and have a very low entry barrier for people coming over from Matlab.
This also explains its name. Some other alternatives are [Plotly](https://plotly.com/python/getting-started) and [Seaborn](http://seaborn.pydata.org/introduction.html).

## Importing the matplotlib library

Before we start plotting, we need to import the matplotlib library. The way to do this is via the `import` command.


```python
import matplotlib.pyplot as plt
import numpy as np
%matplotlib widget
```

## Basic Plotting

The simplest \\((x,y)\\) plots can be plotted using the `plt.plot` method. With two iterables of the same length. Example is shown below.


```python
ax = [0., 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
ay = [0.0, 0.25, 1.0, 2.25, 4.0, 6.25 , 9.0]
plt.plot(ax, ay)
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_4_0.png)
    


Similarly a scatter plot can be created as shown below. This uses the `plt.scatter` method.


```python
import random 
ax, ay = [], []
for i in range(100):
    ax.append(random.random())
    ay.append(random.random())
    
plt.scatter(ax,ay)
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_6_0.png)
    


Let's say you want to plot \\(y=\\sin^2(x)\\) for \\(-2\\pi \\leq x \\leq 2\\pi\\). Then the easiest way to do this to create equally spaced points between \\(-2\\pi\\) and \\(2\\pi\\). And then compute the value of \\(\\sin^2(x)\\) at these points and plot them. This is shown below.


```python
import math
xmin, xmax = -2*math.pi, 2*math.pi
n = 1000
x = [0.] * n
y = [0.] * n
dx = (xmax-xmin)/(n-1)
for i in range(n):
    xpt = xmin + i*dx
    x[i] = xpt
    y[i] = math.sin(xpt)**2
    
plt.plot(x,y)
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_8_0.png)
    


Most of the code above is for actually creating the x andy that can then be plotted. This is simplified a lot using the `linspace` methods and vectorization. Let's look at that.

## Linspace and vectorization

`linspace` will create equally spaced points between the two ranges specified by the program. The code for achieving the above, can be reduced to as little as 


```python
import numpy as np
n = 1000
xmin, xmax = -2 * np.pi, 2 * np.pi
x = np.linspace(xmin, xmax, n)
y = np.sin(x)**2

plt.plot(x,y)
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_10_0.png)
    


As you can see, this is considerably less work than what was required before. Let's say we wanted to also plot \\(\\cos^2(x)\\) along with the \\(\\sin^2(x)\\). This will result in a trivial addition of two lines. 


```python
import numpy as np
n = 1000
xmin, xmax = -2 * np.pi, 2 * np.pi
x = np.linspace(xmin, xmax, n)
y1 = np.sin(x)**2
y2 = np.cos(x)**2

plt.plot(x,y1)
plt.plot(x,y2)
plt.savefig('matplotlib.png')
```


    
![png](/posts/plotting-with-matplotlib/output_12_0.png)
    


Let's plot the \\(sinc\\) function. 


```python
x = np.linspace(-20, 20 , 1001)
y = np.sin(x)/x
plt.plot(x,y)
plt.show()
```

    <ipython-input-11-2d066c76d442>:2: RuntimeWarning: invalid value encountered in true_divide
      y = np.sin(x)/x



    
![png](/posts/plotting-with-matplotlib/output_14_1.png)
    


Notice the divide by 0 warning at 0. Matplotlib will ignore the discontinuity and plot the other points.

## Labels, Legends and Customizations

We can add a legend using the `label` argument to `plt.plot`. It will also need a called to `plt.legend()` before the `plt.show()` call.,


```python
xmin, xmax = -2 * np.pi, 2 * np.pi
x = np.linspace(xmin, xmax, n)
y1 = np.sin(x)**2
y2 = np.cos(x)**2

plt.plot(x, y1, label='sin^2(x)')
plt.plot(x, y2, label='cos^2(x)')
plt.legend(loc='upper right')
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_16_0.png)
    


Now let's add axis labels and plot titles. Let's modify the above code. Note that \\(LaTeX\\) is used extensively in the snippet below.


```python
xmin, xmax = -2 * np.pi, 2 * np.pi
x = np.linspace(xmin, xmax, n)
y1 = np.sin(x)**2
y2 = np.cos(x)**2

plt.plot(x, y1, label='$\sin^2(x)$')
plt.plot(x, y2, label='$\cos^2(x)$')
plt.title('Plot of $\sin^2(x)$ and $\cos^2(x)$')
plt.xlabel('x')
plt.ylabel('$sin^2(x)$ and $cos^2(x)$')
plt.legend(loc='upper right')
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_18_0.png)
    


Note : If you want to use \\(LaTeX\\) in the plotting, it can be done easily by updating the Matplotlib's rc setting. 


```python
plt.rc('text',usetex=True)
```

Let's look at a slightly more involved example. Let's plot \\(f\_n(x) = x^n\\sin x\\) for \\(n=1,2,3,4\\).


```python
x = np.linspace(-10, 10, 1001)
for n in range(1,5):
    y = x**n * np.sin(x)
    y /= max(y)
    plt.plot(x, y, label = r'$x^{}\sin x$'.format(n))
plt.legend(loc='lower center')
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_22_0.png)
    


## Markers

By default matplotlib plots don't have any markers. But you can easily add them. The legend for markers can be seen at https://matplotlib.org/stable/api/markers_api.html

Commnon ones that you will use most often are 

| Code | Description       |
| ---- | ----------------- |
| .    | Point             |
| o    | Circle            |
| +    | Plus              |
| x    | Cross             |
| D    | Diamond           |
| v    | Downword Triangle |
| ^    | Upward Triangle   |
| s    | Square            |
| *    |                   |

## Colors 

Colors can be specified by using the color specifiers. Example is shown below

| Basic Color Code | Tableau Colors |
| ---------------- | -------------- |
| b = blue         | tab:blue       |
| g = green        | tab:orange     |
| r  = red         | tab:green      |
| c = cyan         | tab:red        |
| m = magenta      | tab:purple     |
| y = yellow       | tab:brown      |
| k = black        | tab:pink       |
| w = white        | tab:gray       |
|                  | tab:olive      |
|                  | tab:cyan       |


## Line Style and Width 

Line styles and width can be specified using the `linestyle` and `linewidth` parameter of the `plot` method. Here is an example that shows all of the above.

| Code | Line Style |
| ---- | ---------- |
| -    | Solid      |
| --   | Dashed     |
| :    | Dotted     |
| -.   | Dash Dot   |


```python
x = np.linspace(0.1, 1., 100)
yi = 1./x
ye = 10*np.exp(-2*x)

plt.plot(x, yi, color='tab:purple', linestyle=':', linewidth=4.)
plt.plot(x, ye, color='tab:orange', linestyle='--', linewidth=4.)
```




    [<matplotlib.lines.Line2D at 0x7ffd325533a0>]




    
![png](/posts/plotting-with-matplotlib/output_24_1.png)
    


`color` can be abbreviated to `c`, `linewidth` to `lw` and `linestyle` to `ls`. The above example becomes.


```python
x = np.linspace(0.1, 1., 100)
yi = 1./x
ye = 10*np.exp(-2*x)

plt.plot(x, yi, c='tab:purple', ls=':', lw=4.)
plt.plot(x, ye, c='tab:orange', ls='--', lw=4.)
```




    [<matplotlib.lines.Line2D at 0x7ffd32617e80>]




    
![png](/posts/plotting-with-matplotlib/output_26_1.png)
    


### Example - Moore's Law

Moore's law can be expressed mathematically as follows

\\[n\_i = n\_02^{(y\_i - y\_0)/T\_2}\\]

where \\(n\_i, n\_0\\) is the number of transistor in the year \\(y\_i, y\_0\\) . \\(T\_2\\) is the number of years it will take to double the transistor count and is equal to 2. 

Since there can be many orders of magnitude on both the years and the transistor count, a log plot is better. Taking \\(log\_10\\) on both sides we get

\\[log\_{10}(n\_i) = log\_{10}(n\_0) + \\frac{y\_i - y\_0}{T\_2}log\_{10} 2 \\]


```python
# List of years
year = [1972, 1974, 1978, 1982, 1985, 1989, 1993, 1997, 1999, 2000, 2003, 2004, 2007, 2008, 2012]
# Number of transistors (ntrans) on the CPU in Millions
ntrans = [0.0025, 0.005, 0.029, 0.12, 0.275, 1.18, 3.1, 7.5, 24.0, 42.0, 220.0, 592.0, 1720.0, 2046.0, 3100]
# Turn ntrans list into a numpy array and multiply by 1e6 
ntrans = np.array(ntrans) * 1.e6

y0, n0 = year[0], ntrans[0]
# Create a linear array of years 
y = np.linspace(y0, year[-1], year[-1] - y0 +1)
# Time taken for trans count to double 
T2 = 2

moore = np.log10(n0) + (y-y0)/T2 * np.log10(2)

plt.plot(year, np.log10(ntrans), '*', markersize=12, color = 'tab:red', markeredgecolor='tab:red', label='observed')
plt.plot(y, moore, linewidth=2, color='tab:purple', ls = '--', label='predicted')
plt.legend(fontsize=16, loc='upper left')
plt.xlabel('year')
plt.ylabel('log(ntrans)')
plt.title("Moore's Law")
plt.show()
```


    
![png](/posts/plotting-with-matplotlib/output_28_0.png)
    



```python
k1 = 300
k2 = 100
A0 = 2

t = np.linspace(0,0.015, 100)
temp = np.exp(-1 * (k1+k2) * t)

A = A0*temp
B = (k1/(k1+k2))*A0*(1-temp)
C = (k2/(k1+k2))*A0*(1-temp)

plt.plot(t, A, label='A')
plt.plot(t, B, label='B')
plt.plot(t, C, label='C')
plt.title("Concentration of A, B, and C")
plt.xlabel("Time (in s)")
plt.ylabel("Concentration (in $mol dm^{-3}$)")
plt.legend(loc='upper right')
plt.show()

```


    Canvas(toolbar=Toolbar(toolitems=[('Home', 'Reset original view', 'home', 'home'), ('Back', 'Back to previous …



    
![png](/posts/plotting-with-matplotlib/output_29_1.png)
    

