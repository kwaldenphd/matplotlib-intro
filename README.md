# Introduction to `matplotlib`

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab covers the fundamentals of creating plots in Python using `matplotlib`. It covers the basic anatomy of a `matplotlib` figure and the customization and styling options available. It provides an overview of common plot types, as well as image export options. It provides a comparison and overview of `matplotlib`'s two interfaces: object-oriented and `pyplot`. 

By the end of this lab, students will be able to:
- Understand the core components of a `matplotlib` figure
- Be able to write code that generates a `matplotlib` figure
- Understand the customization and styling options available in `matplotlib`
- Be able to customize a `matplotlib` figure using available styling options
- Understand the range of plot types available in `matplotlib`
- Be comfortable navigating `matplotlib` documentation
- Be able to save a `matplotlib` figure as a static image file

## Acknowledgements

The author consulted the following materials when building this tutorial:
- `matplotlib`, ["Usage Guide"](https://matplotlib.org/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py)
- `matplotlib`, ["Tutorials"](https://matplotlib.org/tutorials/index.html)
- `pandas` documentation, ["Getting Started: Plotting"](https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html)
- Chapter 9 "Plotting and Visualization" from Wes McKinney, [*Python for Data Analysis: Data Wrangling With pandas, Numpy, and IPython*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017)
- Ventsislav Yordanov, ["Data Science with Python: Intro to Data Visualization with Matplotlib"](https://towardsdatascience.com/data-science-with-python-intro-to-data-visualization-and-matplotlib-5f799b7c6d82) *Towards Data Science* (21 July 2018)
- Chapter 15 "Generating Data" from Eric Matthes, [*Python Crash Course: A Hands-On, Project-Based Introduction to Programming*](https://ehmatthes.github.io/pcc_2e/) (No Starch Press, 2019).
- Chapter 4 "Visualization with Matplotlib" from Jake VanderPlas, [*Python Data Science Handbook: Essential Tools for Working with Data*](https://jakevdp.github.io/PythonDataScienceHandbook/) (O'Reilly, 2016)

All figures in this lab come from the `matplotlib` documentation and tutorials.

# Table of Contents

- [Lab notebook template](#lab-notebook-template)
- [Getting started with `matplotlib`](#getting-started-with-matplotlib)
- [Anatomy of a `matplotlib` figure](#anatomy-of-a-matplotlib-figure)
- [Customizing in `matplotlib`](#customizing-in-matplotlib)
  * [Title and Axis Labels](#title-and-axis-labels)
  * [Font Size and Line Thickness](#font-size-and-line-thickness)
  * [Ticks and Ticklabels](#ticks-and-ticklabels)
  * [Colors, Markers, and Line Styles](#colors-markers-and-line-styles)
  * [Making Style Choices](#making-style-choices)
  * [Legends](#legends)
  * [Additional Resources](#additional-resources)
- [Other Types of Plots](#other-types-of-plots)
  * [Subplots](#subplots)
  * [Scatterplots](#scatterplots)
  * [Histograms](#histograms)
  * [Bar Charts](#bar-charts)
  * [Pie Charts](#pie-charts)
  * [Boxplots](#boxplots)
  * [Tables](#tables)
  * [Other Types of Plots](#other-types-of-plots)
- [Lab Notebook Question 4](#lab-notebook-question-4)
- [Saving or Exporting Plots](#saving-or-exporting-plots)
  * [Lab Notebook Question 5](#lab-notebook-question-5)
- [`OO` vs. `pyplot`](#OO-vs-pyplot)
- [What's Next](#whats-next)
- [Best Practices for Data Visualization](#best-practices-for-data-visualization)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here to access the lab procedure as a Jupyter Notebook](https://drive.google.com/file/d/1UYQXwdI3VVlO3eyN1dgTqRoAIrF8chnc/view?usp=sharing)

# Lab Notebook Template

[Link to access lab notebook template (Jupyter Notebook)](https://drive.google.com/file/d/1mKVWgMdmdQ6H7ZF4lpAOVM16tTQRX_gO/view?usp=sharing)

# Getting started with `matplotlib`

1. For our purposes, a plot is defined as "a graphic representation (such as a chart)" (Merriam Webster).

2. These graphic representations of data are often called charts, graphs, figures, etc. 

3. In the context of programming, computer science, and data science, we refer to these as plots.

4. We can generate plots for data stored in `pandas` using the `matplotlib` package.

5. `matplotlib` was developed in 2002 as a MATLAB-like plotting interface for Python.

6. "Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python...Matplotlib produces publication-quality figures in a variety of hardcopy formats and interactive environments across platforms. Matplotlib can be used in Python scripts, the Python and IPython shell, web application servers, and various graphical user interface toolkits" ([Matplotlib documentation, Github](https://github.com/matplotlib/matplotlib))

7. As described [by the original developer John Hunter](https://matplotlib.org/users/history.html), "Matplotlib is a library for making 2D plots of arrays in Python. Although it has its origins in emulating the MATLAB graphics commands, it is independent of MATLAB, and can be used in a Pythonic, object oriented way. Although Matplotlib is written primarily in pure Python, it makes heavy use of NumPy and other extension code to provide good performance even for large arrays. Matplotlib is designed with the philosophy that you should be able to create simple plots with just a few commands, or just one! If you want to see a histogram of your data, you shouldn't need to instantiate objects, call methods, set properties, and so on; it should just work."

8. For more on `matplotlib`'s development and history: John Hunter, ["History"](https://matplotlib.org/users/history.html) *Matplotlib* (2008)

9. To be able to call the `matplotlib` API (application programming interface) within Python, we need to make sure the package is installed and loaded.
- To install at the command line: `pip install matplotlib`
- To load in a `.py` script: `import matplotlib.pyplot as plot`
- To work with `matplotlib` from a Jupyter notebook: `%matplotlib notebook`

NOTE: If your kernel dies when you try to run the code below, run `conda install freetype=2.10.4` in a terminal and restart the Jupyter Notebook kernel. You will need to launch the terminal as an administrator to be able to run the command successfully.

10. The default `matplotlib` plot is a line plot.

```Python
# import matplotlib
import matplotlib.pyplot as plt

# import numpy
import numpy as np

# create dataset of numbers 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
data = np.arange(10)

# create line plot of data 
plt.plot(data)
```

11. We pass our data to `plt.plot()` and a line plot is generated.

12. Plots in `matplotlib` reside within a `Figure` object.

13. These figures contain one or more `Axes`, which are the area where points can be added or specified usign x-y coordinates for 2-D plots.

14. Once the `Figure` object has been created, we can add start adding elements to the plot.

15. The easiest way to create a figure is using `pyplot.subplots()`.

16. NOTE: Because we have loaded the package using `import matplotlib.pyplot as plot`, we can use `plt` as shorthand for `pyplot`.

17. We can then use `axes.plot()` to create axes and add data.

18. Another line plot using a list of number values:
```Python
# import package
import matplotlib.pyplot as plt

# create figure with axes
fig, ax = plt.subplots()

# plot data on axes
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])
```

19. We can see the first list of `1, 2, 3, 4` is shown on the `X` axis.

20. The second list `1, 4, 2, 3` is shown on the `Y` axis.

21. NOTE: The `Y` axis values are plotted in the original order--for this type of plot (a line plot), `matplotlib` keeps the list data in its original order.

22. Let's generate a line plot using a square number sequence

```Python
# import matplotlib
import matplotlib.pyplot as plt

# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares)

# show plot
plt.show()
```

23. In this example, we import `matplotlib` and create two lists, `squares` and `input_values` that hold the data that will be plotted.

24. NOTE: We need to specify `input_values`, because the default in `matplotlib` will start the axis at `0`.

25. We then create a new variable `fig` that represents the entire figure or collection of plots.

26. The variable `ax` represents a single plot in the `fig` figure.

27. We then pass `squares` to the `plot()` method to create the plot.

28. And `plt.show()` opens the `matplotlib` viewer to show us the newly-generated plot.

29. From within the `matplotlib` viewer, we can zoom in and navigate the plot, as well as save images of the plot.

# Anatomy of a `matplotlib` figure

30. Before we start customizing plots or generating more complex plots, it's useful to know the components of a `matplotlib` figure.

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_1.png?raw=true" /></a></p>

## `Figure`

31. `Figure`: A figure object that can include multiple `Axes` or plots; a `Figure` contains at least one `Axes`

```Python
# create an empty figure with no axes
fig = plt.figure()

# create a figure with a single axes
fig, ax = plt.subplots()

# create a figure with a 2x2 grid of axes
fig, axs = plt.subplots(2, 2)
```

32. Having multiple `Axes` in the same `Figure` is useful when creating side-by-side visualizations or a dashboard-style collection of visualizations.

## `Axes`

33. In `matplotlib` syntax, `Axes` are what we would think of as a single plot, where data is plotted.

34. A `Figure` can contain many `Axes`, but a given `Axes` object can only be in one `Figure`.

35. For cartesian coordinate plane visualizations, an `Axes` contains two `Axis` objects.

## `Axis`

36. `matplotlib` works in a Cartesian coordinate system, with an `X` (horizontal) and `Y` (vertical) axis.

37. In a `matplotlib` plot, the `Axis` objects set graph limits and generate tick marks and labels.

38. The location of ticks is determined by a `Locator` object.

39. Tick labels are strings formatted using `Formatter`.

## Everything Else (`Artists`)

40. The other components of the `Figure` include things like axis labels, marker or line style, tick labels, figure title, etc.

41. These are all referred to as `Artists` in `matplotlib` documentation.

42. Knowing how to configure or customize these plot components is not just about aesthetics--in many cases, customizing a plot is necessary for readability.

<blockquote>Q1: Describe in your own words the core components of a matplotlib figure. What is the general sequence of steps involved in generating a matplotlib figure?</blockquote>

# Customizing in `matplotlib`

## Title and Axis Labels

43. We can start by adding a plot title, and axis labels to our square root line plot.
```Python
# import matplotlib
import matplotlib.pyplot as plt

# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares)

# add title
ax.set_title("Square Numbers")

# add x axis label
ax.set_xlabel("Value")

# add y axis label
ax.set_ylabel("Square of Value") 

# show plot
plt.show()
```

44. We now see a title and axis labels.

45. As we'll see later, this basic title and axis label syntax applies across different types of `matplotlib` plots.

## Font Size and Line Thickness

46. We can also customize the font size for title and labels, as well as the line thickness.

```Python
# import matplotlib
import matplotlib.pyplot as plt

# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares, linewidth=3)

# add title
ax.set_title("Square Numbers", fontsize=24)

# add x axis label
ax.set_xlabel("Value", fontsize=14)

# add y axis label
ax.set_ylabel("Square of Value", fontsize=14) 

# show plot
plt.show()
```

47. The updated plot includes these size and thickness modifications.

## Ticks and Ticklabels

48. By default, `matplotlib` will use the tick locations as labels.

49. We can use `.set_xticks()` and `.set_xticklabels()` to set tick values and labels for the `X` axis.

50. `.set_yticks()` and `.set_yticklabels()` do the same for the `Y` axis.

51. Tick values work within the data range for each axis.

52. Let's say we wanted number words as tick labels for our square root plot.
```Python
# import matplotlib
import matplotlib.pyplot as plot

# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares)

# add title
ax.set_title("Square Numbers")

# add x axis label
ax.set_xlabel("Value")

# add y axis label
ax.set_ylabel("Square of Value") 

# set x axis tick locations
ax.set_xticks([0, 1, 2, 3, 4, 5])

# set x axis  tick labels
ax.set_xticklabels(['zero', 'one', 'two', 'three', 'four', 'five'])

# set y axis tick locations
ax.set_yticks([0, 5, 10, 15, 20, 25, 30])

# set y axis tick labels
ax.set_yticklabels(['zero', 'five', 'ten', 'fifteen', 'twenty', 'twenty five', 'thirty'])

# show plot
plt.show()
```

53. We could also adjust the font size and rotation for those tick labels by modifying the `.set_ticklabels()` lines.
```Python
# set x axis  tick labels
ax.set_xticklabels(['zero', 'one', 'two', 'three', 'four', 'five'], rotation=30, fontsize='small')

# set y axis tick labels
ax.set_yticklabels(['zero', 'five', 'ten', 'fifteen', 'twenty', 'twenty five', 'thirty'], fontsize='small')
```

54. These modifications set the ticklabel font size as `small` and for the `X` axis tick labels rotate the text by 30 degrees.

55. We could also adjust the tick label style without adjusting the actual tick labels using `.tick_params()`. For example, to change the font size for major tick marks on both axis:
```Python
# add title
ax.set_title("Square Numbers")

# add x axis label
ax.set_xlabel("Value")

# add y axis label
ax.set_ylabel("Square of Value") 

# set tick label size
ax.tick_params(axis='both', which='major', labelsize=14)
```

56. In this example, the default tick values and labels will be used. 

57. `.tick_params()` modifies the label size for major tick marks on both the `X` and `Y` axis.

## Colors, Markers, and Line Styles

58. The `.plot()` function can take additional arguments that specify line style and color.

59. For plots that have points or markers, these same characters are used to specify point type and color.

### Line Style

60. The following table includes characters and descriptions for line style keyword arguments.

Character | String Representation | Description
--- | --- | ---
`-` | `solid` | Dash; solid line style
`--` | `dashed` | Double dash; dashed line style
`-.` | `dashdot` | Dash dot; dash-dot line style
`:` | `dotted` | Colon; dotted line style

61. For more on customizing line styles:
- [Linestyles](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/linestyles.html)

### Marker Style

62. The following table includes characters and descriptions for marker style keyword arguments.

Character | Description
--- | ---
`.` | Period; point marker
`,` | Comma; pixel marker
`o` | Lower-case letter o; circle marker
`v` | Lower-case letter v; triangle_down marker
`^` | Vertical caret symbol; triangle_up marker
`<` | Less-than sign; triangle_left marker
`>` | Greater-than sign; triangle_right marker
`1` | Number 1; tri_down marker
`2` | Number 2; tri_up marker
`3` | Number 3; tri_left marker
`4` | Number 4; tri_right marker
`s` | Lower-case letter s; square marker
`p` | Lower-case letter p; pentagon marker
`*` | Asterisk; star marker
`h` | Lower-case letter h; hexagon1 marker
`H` | Upper-case letter h, hexagon2 marker
`+` | Plus sign; plus marker
`x` | Lower-case letter x; x marker
`D` | Upper-case letter d; diamond marker
`d` | Lower-case letter d; thin_diamond marker
`|` | Vertical line or pipe symbol; vline marker
`_` | Underscore symbol; hline marker

### Colors

63. The following table includes characters and descriptions for color keyword arguments.

Character | Color
--- | ---
`b` | blue
`g` | green
`r` | red
`c` | cyan
`m` | magenta
`y` | yellow
`k` | black
`w` | white

64. You can also specify colors using full color names (`green`) or hex strings (`#008000`).

65. `matplot` lib supports the following named color pallets:
- Base colors (character keyword arguments)
- Tableau (named color from default Tableau 10 pallette; uses `tab:blue` syntax)
- CSS (named colors from CSS; uses `black`, `dimgray`, `antiquewhite` syntax)

66. For more on colors in `matplotlib`:
- [List of named colors](https://matplotlib.org/3.1.1/gallery/color/named_colors.html)
- [Specifying Colors](https://matplotlib.org/3.1.1/tutorials/colors/colors.html#sphx-glr-tutorials-colors-colors-py)
- [`matplotlib.colors`](https://matplotlib.org/3.1.1/api/colors_api.html#module-matplotlib.colors)
- [Color Demo](https://matplotlib.org/3.1.1/gallery/color/color_demo.html)

## Making Style Choices

67. When building a plot that will have multiple lines or types of markers, line/marker style (along with color) can help distinguish each component.

68. In a situation where the plot will be presented or printed in black-and-white only, or viewed by an audience that may include individuals with visual impairments, intentional use of line/marker style is essential for accessibility.

69. When building a plot that will have multiple lines or types of markers, color (along with line/marker style) can help distinguish each component.

70. But relying only on color to convey meaning in a plot runs the risks of making the visual inaccessible or not meaningful to those with visual impairments.

71. Axis Maps's [Colorbrewer2.0](https://colorbrewer2.org/) is a useful tool for finding accessible color palletes.

### Colormaps

72. As described by Kenneth Moreland, "One of the most fundamental features of scientific visualiation is the process of mapping scalar values to colors" (Moreland, "Diverging Color Maps for Scientific Visualization," in *Proceedings of the 5th International Symposium on Visual Computing*, December 2009. http://dx.doi.org/10.1007/978-3-642-10520-3_9)

73. The color scheme or pallette for a plot is most often referred to as a colormap.

74. Colormaps generally fall into a few categories.

75. `matplotlib` includes [a wide range of built-in colormaps](https://matplotlib.org/tutorials/colors/colormaps.html), some of which are shown in the images below.

#### Sequential

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_3.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_3.png?raw=true" /></a></p>

76. Sequential colormaps show change in lightness or color saturation incrementally. 

78. They are generally comprised of a single hue.

#### Diverging

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_4.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_4.png?raw=true" /></a></p>

79. Diverging colormaps show change in lightness and possibly saturation for two different colors that meet in the middle at an unsaturated color. 

80. This type of colormap is most effective when data being plotted has a critical middle value, or deviates around zero.

#### Cyclic

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_5.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_5.png?raw=true" /></a></p>

81. Cyclic colormaps show change in lightness for two different colors that meet in the middle and begin or end at an unsaturated color.

82. This type of colormap is most effective for data values that wrap around at the endpoints (i.e. phase angle, wind direction, time of day).

#### Qualitative

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_6.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_6.png?raw=true" /></a></p>

83. Qualitative colormaps are miscellaneous colors.

84. This type of colormap is most effective for information that does not have ordering or relationships.

85. For more on colormaps in `matplotlib`:
- [Colormaps](https://matplotlib.org/3.1.1/tutorials/colors/colormaps.html)
- [Choosing Colormaps in Matplotlib](https://matplotlib.org/tutorials/colors/colormaps.html#sphx-glr-tutorials-colors-colormaps-py)
- [Creating Colormaps in Matplotlib](https://matplotlib.org/3.1.1/tutorials/colors/colormap-manipulation.html)

<blockquote>Q2: Describe the different types of colormaps in your own words. What are the parameters or factors to consider when choosing a colormap?</blockquote>

## Putting It All Together

86. So how would we use these arguments when generating a plot?

87. Line or marker styles and colors can be combined in a single string format.

88. Combining these characters opens up a wide range of customization options.

89. A few examples:
- `bo`: blue circle marker
- `k--`: black dashed line
- `rp`: red pentagon marker
- `cD`: cyan diamond marker

90. You can also specify line style using named stings.

91. These arguments are invoked as part of the `.plot()` function (or the equivalent function when generating other kinds of plots).

92. A few examples for customizing line color and style:
```Python
# set line color using named color
ax.plot(x, y, color='blue')

# set line color using color character
ax.plot(x, y, color='b')

# set line color using hex
ax.plot(x, y, color="#0000FF")

# set color using tab notation
ax.plot(x, y, color='tab:blue')
```

```Python
# set line style using character
ax.plot(x, y, linestyle='--')

# set line style using style name
ax.plot(x, y, linestyle='dashed')
```

```Python
# set line style and color using characters
ax.plot(x, y, 'b--')

# set line style and color separately
ax.plot(x, y, color='blue', linestyle='--')
```

```Python
# set marker style and color using characters
ax.plot(x, y, 'bo')

# set marker style and color separately
ax.plot(x, y, color='green', marker='o')
```

Some Python examples that combine these elements.

```Python
# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares)

# add title
ax.set_title("Square Numbers")

# add x axis label
ax.set_xlabel("Value")

# add y axis label
ax.set_ylabel("Square of Value") 

# set x axis tick locations
ax.set_xticks([0, 1, 2, 3, 4, 5])

# set line style and color using characters
ax.plot(input_values, squares, 'b--')

# show plot
plt.show()
```

```Python
# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares)

# add title
ax.set_title("Square Numbers")

# add x axis label
ax.set_xlabel("Value")

# add y axis label
ax.set_ylabel("Square of Value") 

# set x axis tick locations
ax.set_xticks([0, 1, 2, 3, 4, 5])

# set line style and color using characters
ax.plot(input_values, squares, color="blue")

# show plot
plt.show()
```

An example that draws a bar chart and uses a color map to assign unique bar colors.

```Python
# set x and y values
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

# assign colormap
my_cmap = plt.get_cmap("viridis")

# scale colormap
rescale = lambda y: (y - np.min(y)) / (np.max(y) - np.min(y))

# generate plot
plt.bar(x, y, color=my_cmap(rescale(y)))

# show plot
plt.show()
```

An example that uses a for loop and color map to assign unique bin colors.
```Python
# import matplotlib components
from matplotlib import colors
from matplotlib.ticker import PercentFormatter

# create figure and axes
fig, axs = plt.subplots(1, 2, tight_layout=True)

# set values and number of bins 
N_points = 100000
n_bins = 20

# set normal distribution
x = np.random.randn(N_points)
y = .4 * x + np.random.randn(100000) + 5

# N is the count in each bin, bins is the lower-limit of the bin
N, bins, patches = axs[0].hist(x, bins=n_bins)

# We'll color code by height, but you could use any scalar
fracs = N / N.max()

# we need to normalize the data to 0..1 for the full range of the colormap
norm = colors.Normalize(fracs.min(), fracs.max())

# Now, we'll loop through our objects and set the color of each accordingly
for thisfrac, thispatch in zip(fracs, patches):
    color = plt.cm.viridis(norm(thisfrac))
    thispatch.set_facecolor(color)

# We can also normalize our inputs by the total number of counts
axs[1].hist(x, bins=n_bins, density=True)

# Now we format the y-axis to display percentage
axs[1].yaxis.set_major_formatter(PercentFormatter(xmax=1))

# show plot
plt.show()
```

### Style Sheets

93. The prospect of having to make choices about font, style, color, and formatting for every component of your plot can be daunting.

94. `matplotlib` includes a wide range of predefined styles.

<p align="center"><a href="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_2.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/matplotlib-intro/blob/main/figures/Figure_2.png?raw=true" /></a></p>

95. Similar to how `CSS` (cascading style sheets) interact with `HTML` (hyper-text markup language), these style sheets cover style and formatting elements like background colors, gridlines, line widths, fonts, font sizes, and more.

96. To use one of these styles, we can add a single line of code before starting to generate the plot.

```Python
# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# set plot style
plt.style.use('ggplot')

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares, linewidth=3)

# add title
ax.set_title("Square Numbers", fontsize=24)

# add x axis label
ax.set_xlabel("Value", fontsize=14)

# add y axis label
ax.set_ylabel("Square of Value", fontsize=14) 

# set tick label size
ax.tick_params(axis='both', labelsize=14)

# show plot
plt.show()
```

97. Consult the `matplotlib` ["Style sheets reference" page](https://matplotlib.org/3.2.1/gallery/style_sheets/style_sheets_reference.html) to learn more.

98. For those interested in data journalism, most large publications have an internal style guide. And since 2017, the AP Stylebook has included a chapter on data journalism.
- Daniel Funke, ["The updated 'Bloomberg Way' s tyle guide focuses on best practices for data and multiplatform journalism"](https://www.poynter.org/reporting-editing/2017/the-updated-bloomberg-way-style-guide-focuses-on-best-practices-for-data-and-multiplatform-journalism/) *Poynter* (18 July 2017)
- Lauren Easton, ["Digging into data journalism"](https://blog.ap.org/industry-insights/digging-into-data-journalism) *Associated Press* (26 July 2017)

## Legends

99. When building more complex plots with multiple lines, comparisons, etc. plot legends are essential.

100. Some key terms for working with `.legend()`:
- ***legend entry***: exactly one key and one label
- ***legend key***: colored/patterned marker to the left of each legend label
- ***legend label***: text which describes the handle represented by the key
- ***legend handle***: original object used to generate an appropriate entry in the legend

101. We can create a legend in `matplotlib` using `.legend()`.

102. The basic options for creating a legend:
```Python
# calling legend with automatic detection
legend()

# calling legend from existing plot element labels
legend(labels)

# calling legend by defining legend elements
legend(handles, labels)
```

103. For some types of visualizations, the default legend in `matplotlib` will be sufficient.

104. One way to build a legend is to use the `label` argument for each piece of the plot.

105. Using `.legend()` means the elements to be added to the legend are determined automatically.

106. No additional arguments are passed to the function.

107. Labels are set using the `.set_label()` method when creating the original handle.

108. Elements with an empty string as the label or a label that starts with the undescore character `_` will not be included in the legend.

```Python
# create figure for new plot
fig, ax = plt.subplots()

# create handle for first line
line_1, = ax.plot([LINE DATA], 'b--')

# set label for line_1
line_1.set_label('Line One')

# create handle for second line
line_2, = ax.plot([LINE DATA], color='green', linestyle='-.')

# set label for line_2
line_2.set_label('Line Two')

# create handle for third line that will NOT be included in the legend
line_3, = ax.plot([LINE DATA], color='#000000', linestyle='-')
line_3.set_label('_Line Three')

# show plot
plt.show()
```

109. In this example, `ax.legend()` will use the `label` attributes for each line to add it to the legend.

110. Line three will not be added because its label begins with the underscore character `_`.

111. We can also pass the list of handles directly to `.legend()`:

```Python
# create figure for new plot
fig, ax = plt.subplots()

# create handle for first line
line_1, = ax.plot([LINE DATA], 'b--')

# set label for line_1
line_1.set_label('Line One')

# create handle for second line
line_2, = ax.plot([LINE DATA], color='green', linestyle='-.')

# set label for line_2
line_2.set_label('Line Two')

# create legend
ax.legend(handles=[line_1, line_2])

# show plot
plt.show()
```

Another example that uses labeled handles to create a legend.

```Python
# create figure for new plot
fig, ax = plt.subplots()

# create line 1
line_up, = plt.plot([1,2,3], label='Line 2')

# create line 2
line_down, = plt.plot([3,2,1], label='Line 1')

# create plot with legend
plt.legend(handles=[line_up, line_down])

# show plot
plt.show()
```

112. In a situation where our handles do not have labels, we can pass both the handles and labels to `.legend()`.

```Python
# create figure for new plot
fig, ax = plt.subplots()

# create line 1
line_up, = plt.plot([1,2,3], label='Line 2')

# create line 2
line_down, = plt.plot([3,2,1], label='Line 1')

# create plot with legend
plt.legend([line_up, line_down], ['Line Up', 'Line Down'])

# show plot
plt.show()
```

113. In some situations, we might want to create a legend with handles that don't exist in our Figure or Axes.

114. For example, in a situation where color has meaning, we want a legend that takes color values as handles, rather than values for data associated with a specific color.

115. We can create a handle just for the legend.

116. That is, there is no requirement for handles included in the legend to exist in the Figure or Axes.

117. An example where the color red is a handle for our legend.

```Python
# import matplotlib
import matplotlib.patches as mpatches

# create figure for new plot
fig, ax = plt.subplots()

# set patch handle and label
red_patch = mpatches.Patch(color='red', label='The red data')

# create legend
ax.legend(handles=[red_patch])

# show plot
plt.show()
```

118. The same is true for line styles or marker symbols.

119. An example where blue lines with stars are a handle for our legend.

```Python
# import mlines
import matplotlib.lines as mlines

# create figure for new plot
fig, ax = plt.subplots()

# set blue line handle
blue_line = mlines.Line2D([], [], color='blue', marker='*', markersize=15, label='Blue stars')

# create legend
ax.legend(handles=[blue_line])

# show plot
plt.show()
```

### Customizing Legends

#### `loc`

120. We can also customize where a legend is located for a plot using the `loc` keyword argument.

121. String arguments for `loc`:

Location String | Location Code
--- | ---
`'best'` | 0
`'upper right'` | 1
`'upper left'` | 2
`'lower left'` | 3
`'lower right'` | 4
`'right'` | 5
`'center left'` | 6
`'center right'` | 7
`'lower center'` | 8
`'upper center'` | 9
`'center'` | 10

122. To invoke these keyword arguments when calling the `.legend()` function:

```Python
# best location
ax.legend(loc='best')

# upper right loc
ax.legend(handles=[line_1, line_2], loc='upper right')

# loc 2, upper-left
ax.legend([line_1, line_2], ['Line One', 'Line Two'], loc=2)

# loc 7, center right
ax.legend(handles=[red_patch], loc=7)

# upper center loc
ax.legend(handles=[blue_line], loc='upper center')
```

Going back to our example of a legend with blue lines and stars:

```Python
# create figure for new plot
fig, ax = plt.subplots()

# assign blue line
blue_line = mlines.Line2D([], [], color='blue', marker='*',
                          markersize=15, label='Blue stars')

# create legend in upper left corner
plt.legend(handles=[blue_line], loc="upper left")

# show plot
plt.show()
```

#### `bbox_to_anchor`

123. In situations where we want to customize where the legend is located, we can use `bbox_to_anchor` in conjunction with `loc`.

124. This argument allows arbitrary placement of the legend.

125. `bbox` coordinates are interpreted in a coordinate system, which uses the default `Axes` or `Figure` coordinates.

126. A few examples:

```Python
# example that puts the legend's upper-right hand corner in the center of the axes
plt.legend(loc='upper right', bbox_to_anchor=(0.5, 0.5))

# example that puts the legend in the best location in the bottom right quadrant of the axes
plt.legend(loc='best', bbox_to_anchor=(0.5, 0., 0.5, 0.5))

# example that places legend above plot and expands legend to full given bounding box
plt.legend(loc='lower left', bbox_to_anchor=(0., 1.02, 1., .102), ncol=2, mode='expand', borderaxespad=0.))

# example that places a legend to the right of a plot
plt.legend(loc='upper left', bbox_to_anchor=(1.05, 1), borderaxespad=0.))
```

127. A Python example that combines these elements:

```Python
# create figure for new plot
fig, ax = plt.subplots()

# assign blue line
blue_line = mlines.Line2D([], [], color='blue', marker='*',
                          markersize=15, label='Blue stars')

# create legend in upper left corner
plt.legend(handles=[blue_line], loc='upper left', bbox_to_anchor=(0.5, 0., 0.5, 0.5))

# show plot
plt.show()
```

### Additional Resources

128. For more on these parameters and other `.legend()` customization options:
- [`matplotlib.pyplot.legend`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)
- [`matplotlib` "Legend guide"](https://matplotlib.org/3.3.3/tutorials/intermediate/legend_guide.html)

## Lab Notebook Question 3

Q3: Create your own matplotlib figure and include the following style elements. Include code + comments.
- Title
- Axis labels
- Tick marks
- Tick labels
- Line or marker style
- Line or marker color
- Legend

# Other Types of Plots

## Subplots

129. As mentioned previously, a single `Figure` object can contain multiple `Axes` or plots.

130. To create a `Figure` with two subplots, we pass number arguments to `plt.subplots()`.

131. An example that compares dampened and undampened oscillation over time (in seconds).

```Python
# create x axis for first subplot
x1 = np.linspace(0.0, 5.0)

# create x axis for second subplot
x2 = np.linspace(0.0, 2.0)

# create y axis for first subplot
y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)

# create y axis for second subplot
y2 = np.cos(2 * np.pi * x2)

# create figure with two axes/subplots, stacked vertically on top of each other
fig, (ax1, ax2) = plt.subplots(2, 1)

# set figure title
fig.suptitle('A tale of 2 subplots')

# create first subplot 
ax1.plot(x1, y1, 'o-')
ax1.set_ylabel('Damped oscillation')

# create  second subplot
ax2.plot(x2, y2, '.-')
ax2.set_xlabel('time (s)')
ax2.set_ylabel('Undamped')

#show plot
plt.show()
```
### Additional Resources

132. For more on subplots:
- [`matplotlib`, Multiple subplots](https://matplotlib.org/gallery/subplots_axes_and_figures/subplot.html)
- [`matplotlib`, Subplots, axes, and figures](https://matplotlib.org/gallery/index.html#subplots-axes-and-figures)
- [Jake VanderPlas, "Multiple Subplots" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.08-multiple-subplots.html)

## Scatterplots

### `.scatter()`

133. The `.scatter()` function creates basic scatter plot visualizations.

134. `.scatter()` can take additional optional size, style, and color arguments.

135. To plot a single point using `.scatter()`:

```Python
# create figure and axes
fig, ax = plt.subplots()

# plot data
ax.scatter(2, 4)

# show plot
plt.show()
```

136. We can plot a series of points by passing lists of `X` and `Y` values to `.scatter()`:
```Python
# set x values
x_values = [1, 2, 3, 4, 5]

# set y values
y_values = [1, 4, 9, 16, 25]

# create figure with axes
fig, ax = plt.subplots()

# create scatter plot
ax.scatter(x_values, y_values, s=100)

#show plot
plt.show()
```

137. We could use the syntax outlined previously to set labels, titles, tick marks, etc.

138. We can also combine elements of a scatter plot and line plot to have points connected by a line:
```Python
# set x values
x = np.linspace(0, 10, 30)

# set y values
y = np.sin(x)

# create figure with axis
fig, ax = plt.subplots()

# create scatter plot
ax.scatter(x, y)

# show plot
plt.show()
```

### `.plt.scatter()`

139. We can create more highly customized scatter plots using `plt.scatter()`.

```Python
# set x values
x = np.linspace(0, 10, 30)

# set y values
y = np.sin(x)

# create figure with axis
fig, ax = plt.subplots()

# create scatter plot
ax.scatter(x, y, marker='o')

# show plot
plt.show()
```

140. `plt.scatter()` allows us to customize each individual point in the scatter plot, through individual customization or mapping to data.

141. An example random scatter plot with points of different colors and sizes.

```Python
# set random state
rng = np.random.RandomState(0)

# set x values
x = rng.randn(100)

# set y values
y = rng.randn(100)

# set colors
colors = rng.rand(100)

# set size
sizes = 1000 * rng.rand(100)

# create figure with axes
fig, ax = plt.subplots()

# create scatter plot
plot = ax.scatter(x, y, c=colors, s=sizes, alpha=0.3, cmap='viridis')

# show color scale
plt.colorbar(plot)

# show plot
plt.show()
```

142. Another `plt.scatter()` example using data on flower petal and sepal size from `scikit-learn`.

```Python
#import scikit-Learn
from sklearn.datasets import load_iris

# load data 
iris = load_iris()

# create data object
features = iris.data.T

# create figure with axes
fig, ax = plt.subplots()

# create scatter plot
plot_2 = ax.scatter(features[0], features[1], alpha=0.2, s=100*features[3], c=iris.target, cmap='viridis')

# set x axis label
ax.set_xlabel(iris.feature_names[0])

# set y axis label
ax.set_ylabel(iris.feature_names[1])

# show color scale
plt.colorbar(plot_2)

# show plot
plt.show()
```

143. For smaller datasets where a high level of customization is important, `plt.scatter()` will be the better option.

144. For larger datasets, `plt.plot` will perform more effectively (because the program is not styling each individual point when creating the plot).

### Additional Resources

145. For more on scatterplots:
- [`matplotlib`, "Scatter plot"](https://matplotlib.org/gallery/shapes_and_collections/scatter.html#sphx-glr-gallery-shapes-and-collections-scatter-py)
- [`matplotlib`, "Scatter Demo2"](https://matplotlib.org/gallery/lines_bars_and_markers/scatter_demo2.html)
- [`matplotlib.pyplot.scatter`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.scatter.html)
- [Jake VanderPlas, "Simple Scatter Plots" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.02-simple-scatter-plots.html)

## Histograms

146. A histogram is a type of plot that approximates the distribution of numerical data.

147. The first step in constructing a histogram is to `bin` or `bucket` the range of values.

148. In other words, we need to divide the entire range of values into a series of intervals.

149. The second step in constructing a histogram is to count how many values fall into each interval.

150. In a histogram, the bins are usually consecutive, non-overlapping intervals. 

151. The bins must be adjacent and are often (but not necessarily) of equal size.

152. To plot a 1D histogram, we only need a single vector of numbers.

153. 2D histograms require a second vector.

154. A basic 1D histogram:
```Python
# set data
data = np.random.randn(1000)

# create figure and axes
fig, ax = plt.subplots()

# create histogram with no specified bins
ax.hist(data)

# show plot
plt.show()
```

155. Another example of a 1D histogram, this time with a `bins` keyword argument:

```Python
# import statements
from matplotlib import colors
from matplotlib.ticker import PercentFormatter

# Fixing random state for reproducibility
np.random.seed(19680801)

# set number of points
N_points = 100000

# set number of bins
n_bins = 20

# generate normal distribution, centered at x=0 and y=5
x = np.random.randn(N_points)
y = .4 * x + np.random.randn(100000) + 5

# create figure and axes
fig, axs = plt.subplots(1, 2, sharey=True, tight_layout=True)

# set number of bins and generate histograms
axs[0].hist(x, bins=n_bins)
axs[1].hist(y, bins=n_bins)

# show plot
plt.show()
```

156. We could use the syntax outlined previously to set labels, titles, tick marks, etc.

157. The default type of histogram in `matplotlib` is a tranditional `bar`-type histogram.

158. We can use the `histtype` attribute to draw other kinds of histograms.
- `barstacked`: bar-type histogram with stacked data
- `step`: generates an unfilled lineplot
- `stepfilled`: generates a filled lineplot

159. We can also customize our histogram by specifying colors, based on `Y` axis values.

160. An example of a `stepfilled` histogram with no edges and a customized color:
```Python
ax.hist(x, bins=n_bins, histtype='stepfilled', color='steelblue', edgecolor='none')
```

161. For more keyword arguments and attributes that can be passed to `.hist()`: [`matplotlib.pyplot.hist`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.hist.html)

162. An example that color codes by height and uses the data range to set the color map.

```Python
# create figure and axes
fig, axs = plt.subplots(1, 2, tight_layout=True)

# N is the count in each bin, bins is the lower-limit of the bin
N, bins, patches = axs[0].hist(x, bins=n_bins)

# We'll color code by height, but you could use any scalar
fracs = N / N.max()

# we need to normalize the data to 0..1 for the full range of the colormap
norm = colors.Normalize(fracs.min(), fracs.max())

# Now, we'll loop through our objects and set the color of each accordingly
for thisfrac, thispatch in zip(fracs, patches):
    color = plt.cm.viridis(norm(thisfrac))
    thispatch.set_facecolor(color)

# We can also normalize our inputs by the total number of counts
axs[1].hist(x, bins=n_bins, density=True)

# Now we format the y-axis to display percentage
axs[1].yaxis.set_major_formatter(PercentFormatter(xmax=1))
```

### Additional Resources

163. For more on histograms:
- [`matplotlib` "Some features of the histogram (hist) function"](https://matplotlib.org/gallery/statistics/histogram_features.html)
- [`matplotlib`, "Histograms"](https://matplotlib.org/gallery/statistics/hist.html#sphx-glr-gallery-statistics-hist-py)
- [`matplotlib.pyplot.hist`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.hist.html)
- [Jake VanderPlas, "Histograms, Binnings, and Density" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.05-histograms-and-binnings.html)

## Bar Charts

164. One of the common uses for bar charts is to plot categorial variables.

165. A bar chart presents categorical data with rectangular bars with heights or lengths porportional to the values they represent.

166. We can create a basic vertical bar chart using `.bar()`.
```Python
# set dictionary with data categories and amounts
data = {'apple': 10, 'orange': 15, 'lemon': 5, 'lime': 20}

# get category names from dictionary keys
names = list(data.keys())

# get category values from dictionary values
values = list(data.values())

# create figure
fig, axs = plt.subplots()

# create bar chart
axs.bar(names, values) 

# show plot
plt.show()
```

167. This kind of categorical data can be plotted different ways, depending on the type of data and purpose or intent for the visualization.

168. For example, we could plot the fruit data from the previous example as a bar chart, scatter plot, and line plot.

169. An example of those three types side-by-side:
```Python
# set dictionary with data categories and amounts
data = {'apple': 10, 'orange': 15, 'lemon': 5, 'lime': 20}

# get category names from dictionary keys
names = list(data.keys())

# get category values from dictionary values
values = list(data.values())

# create figure with 3 subplots 
fig, axs = plt.subplots(1, 3, figsize=(9, 3), sharey=True)

# create bar chart
axs[0].bar(names, values)

# create scatter plot
axs[1].scatter(names, values)

# create line plot
axs[2].plot(names, values)

# figure title
fig.suptitle('Categorical Plotting')

# show plot
plt.show()
```

170. We could use the syntax outlined previously to set labels, titles, tick marks, etc.

### Horizontal Bar Chart

171. We can also create a horizontal bar chart using `.barh()`.
```Python
# set dictionary with data categories and amounts
data = {'apple': 10, 'orange': 15, 'lemon': 5, 'lime': 20}

# get category names from dictionary keys
names = list(data.keys())

# get category values from dictionary values
values = list(data.values())

# create figure
fig, axs = plt.subplots()

# create horizontal bar chart
axs.barh(names, values) 

# show plot
plt.show()
```

172. You'll notice when we call `.barh()`, the general `x, y` syntax is the same. 

173. The first variable passed to the function is the `X` axis data, and the second variable passed to the function is the `Y` axis data.

174. We could use the syntax outlined previously to set labels, titles, tick marks, etc.

175. For a horizontal bar chart, you may need to invert the `Y` axis labels using `.invert_yaxis()` to read the `Y` axis labels top-to-bottom.

### Stacked Bar Chart

176. Just like we can create a stacked histogram, we can also create a stacked bar chart.

177. This is especially useful when wanting to represent categorical data and multiple levels of abstractions.

178. An example of data well-suited to a stacked bar chart might be population data in which a bar chart with country-level data might also need to be disaggregated by gender or race.

179. To create a stacked bar chart, you create two sets of bars for the plot and assign one to the `bottom` parameter.

180. The `bottom` parameter sets the `Y` axis coordinates of the bottom bars.

181. Error bars can also be useful to deliniate components of a stacked bar chart.

182. In `matplotlib` error bars are vertical or horizontal solid lines added to bar tips. 

183. The error bar values are +/- sizes relative to the data.

184. The `yerr` parameter is used to set error bars for the `Y` axis.

185. Putting this all together in an example that shows score data for 5 different groups, disaggregated by test time:
```Python
# set x axis labels
labels = ['G1', 'G2', 'G3', 'G4', 'G5']

# mean scores for morning test takers, by group
morning_means = [20, 35, 30, 35, 27]

# mean scores for afternoon test takers, by group
afternoon_means = [25, 32, 34, 20, 25]

# number of test takers for morning time, by group
morning_std = [2, 3, 4, 1, 2]

# number of afternoon test takers, by group
afternoon_std = [3, 5, 2, 3, 3]

# sets bar width
width = 0.35

# creates figure and axes
fig, ax = plt.subplots()

# creates first set of bars for morning test scores
ax.bar(labels, morning_means, width, yerr=morning_std, label='Morning')

# creates second set of bars for afternoon test scores, stacked on morning bars
ax.bar(labels, afternoon_means, width, yerr=afternoon_std, bottom=morning_means,
       label='Afternoon')

# sets y axis label
ax.set_ylabel('Scores')

# set title
ax.set_title('Scores by test time')

# create legend
ax.legend()

# show plot
plt.show()
```

### Grouped Bar Chart

186. Grouped bar charts can also be useful for showing disaggregated data, or data at multiple levels of abstraction.

187. When creating a grouped bar chart, we have to set label locations for each of the bars.

188. And the rectangles that are drawn as the bars will need to be half as wide so everything fits on the `X` axis.

189. We can also add a custom annotation to show the value for each bar in the chart, displaying its height.

190. To put that all together, modifying the previous stacked bar example to create a grouped bar chart.
```Python
# set x axis labels
labels = ['G1', 'G2', 'G3', 'G4', 'G5']

# mean scores for morning test takers, by group
morning_means = [20, 35, 30, 35, 27]

# mean scores for afternoon test takers, by group
afternoon_means = [25, 32, 34, 20, 25]

# set label locations
x = np.arange(len(labels))

# set bar width
width = 0.35

# create figure and axes
fig, ax = plt.subplots()

# draw first set of bars/rectangles
rects1 = ax.bar(x - width/2, morning_means, width, label='Morning')

# draw second set of bars/rectangles
rects2 = ax.bar(x + width/2, afternoon_means, width, label='Afternoon')

# set y axis label, figure title, tick marks, and tickmark labels
ax.set_ylabel('Scores')
ax.set_title('Scores by test time')
ax.set_xticks(x)
ax.set_xticklabels(labels)

# create legend
ax.legend()

# create named function that adds custom annotation showing rectangle height value above each bar 
def autolabel(rects):
    """Attach a text label above each bar in *rects*, displaying its height."""
    for rect in rects:
        height = rect.get_height()
        ax.annotate('{}'.format(height),
                    xy=(rect.get_x() + rect.get_width() / 2, height),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')

# applies autolabel function to each group of bars
autolabel(rects1)
autolabel(rects2)

# adjust figure layout
fig.tight_layout()

# show plot
plt.show()
```

### Additional Resources

191. For more on bar charts and plotting categorical data:
- [`matplotlib`, Plotting categorical variables](https://matplotlib.org/gallery/lines_bars_and_markers/categorical_variables.html#sphx-glr-gallery-lines-bars-and-markers-categorical-variables-py)
- [`matplotlib`, Horizontal bar chart](https://matplotlib.org/gallery/lines_bars_and_markers/barh.html)
- [`matplotlib`, Stacked bar chart](https://matplotlib.org/gallery/lines_bars_and_markers/bar_stacked.html)
- [`matplotlib`, Percentiles as horizontal bar chart](https://matplotlib.org/gallery/statistics/barchart_demo.html)


## Pie Charts

192. A pie chart is a circular graphic, divided into slices to illustrate numerical portion.

193. The arc length of each slice (and thus its central angle and area) is proportional to the quantity it represents.

194. Data visualization and information perception research suggests that, while useful in some cases, making visual comparisons within a pie chart or across pie charts is challenging.

195. This research recommends pie charts be replaced by other types of plots (scatter plots, density plots, bar charts, box plots, etc).

196. To learn more:
- Leland Wilkinson, [*The Grammar of Graphics*](https://www.springer.com/gp/book/9780387245447) (Springer, 2005). [Link to electronic access through Hesburgh Libraries](https://onesearch.library.nd.edu/permalink/f/1phik6l/ndu_aleph003079467).
- Edward Tufte, [*The Visual Display of Quantitative Information*](dd) (Graphics Press, 1983). [Link to catalog entry for Hesburgh Library physical copy](https://onesearch.library.nd.edu/permalink/f/1phik6l/ndu_aleph000623770).
- Stephen Few, ["Save the Pies for Dessert"](www.perceptualedge.com/articles/08-21-07.pdf) *Perceptual Edge* (21 August 2007)
- Steve Fenton, ["Pie Charts are Bad"](https://www.stevefenton.co.uk/2009/04/pie-charts-are-bad/) *personal blog* (17 April 2009)
- Dipanjan Sarkar, ["A Comprehensive  Guide to the Grammar of Graphics for Effective Visualization of Multi-dimensional Data"](https://towardsdatascience.com/a-comprehensive-guide-to-the-grammar-of-graphics-for-effective-visualization-of-multi-dimensional-1f92b4ed4149) *Towards Data Science* (12 September 2018)

197. But, as Google's design lead Manuel Lima has noted, humans love pie charts.
- Manuel Lima, ["Why humans love pie charts: An historical and evolutionary perspective"](https://blog.usejournal.com/why-humans-love-pie-charts-9cd346000bdc) *Noteworthy: The Journal Blog* (23 July 2018)

198. So we'll cover them.

199. Sample code for a basic pie chart:
```Python
# set slice labels
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'

# set slice sizes 
sizes = [15, 30, 45, 10]

# create figure and axes
fig1, ax1 = plt.subplots()

# create pie chart 
ax1.pie(sizes, labels=labels)

# set equal aspect ratio to ensure pie is a circle
ax1.axis('equal')

# show plot
plt.show()
```

200. We can customize this pie chart to auto-label each slice's percentage.
```Python
# create pie chart with percent formatting
ax1.pie(sizes, labels=labels, autopct='%1.1f%%')
```

201. The default start angle is `0`, which we can also modify.
```Python
# create pie chart with percent formatting and start angle
ax1.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)
```

202. We can also add a drop shadow to our pie chart.
```Python
# create pie chart with percent formatting, start angle, and drop shadow
ax1.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90, shadow=True)
```

203. We can also "explode" or offset one of the slices.
```Python
# set slice labels
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'

# set slice sizes 
sizes = [15, 30, 45, 10]

# explode or offset only the 2nd slice (i.e. 'Hogs')
explode = (0, 0.1, 0, 0)

# create figure and axes
fig1, ax1 = plt.subplots()

# create pie chart with percent formatting, start angle, and drop shadow
ax1.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90, shadow=True, explode=explode)

# set equal aspect ratio to ensure pie is a circle
ax1.axis('equal')

# show plot
plt.show()
```
### Additional Resources

204. For more on pie charts:
- [`matplotlib`, Basic pie chart](https://matplotlib.org/gallery/pie_and_polar_charts/pie_features.html)
- [`matplotlib.pyplot.pie`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.pie.html)
- [`matplotlib` Gallery, Pie and polar charts](https://matplotlib.org/gallery/index.html#pie-and-polar-charts)

## Boxplots

205. Used to represent descriptive statistics, a box plot depicts groups of numerical data as quartiles.

206. Box plots are sometimes called box-and-whisker plots because they can include lines extending from the boxes (*whiskers*) to show variability outside upper and lower quartiles.

207. Box plots are a standardized way of displaying summary statistics for a dataset.

208. Statistics represented in a box plot include:
- ***minimum***: lowest data point (excluding outliers); 0th percentile or Q<sub>0</sub>
- ***maximum***: highest data point (excluding outliers); 100th percentile or Q<sub>4</sub>
- ***median***: middle value in the dataset; 50th percentile or Q<sub>2</sub>
- ***first quartile***: also known as the lower quartile; median of the lower half of the dataset; 25th percentile or Q<sub>1</sub>
- ***third quartile***: also known as the umper quartile; median of the upper half of the dataset; 75th percentile or Q<sub>3</sub>

209. In the process of calculating these summary statistics, a sixth value is calculated, the interquartile range.

210. ***Interquartile range*** is the distance between upper and lower quartiles.

211. To draw a basic box plot using `matplotlib`:
```Python
# import statements
from matplotlib.patches import Polygon

# fix random state for reproducibility
np.random.seed(19680801)

# create sample data
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))

# create figure and axes
fig, axs = plt.subplots()

# draw basic boxplot
axs.boxplot(data)
axs.set_title('Basic Plot')

# show plot
plt.show()
```

212. We can modify this example to not show the outlier points and map only the quartile summary statistics:
```Python 
# fix random state for reproducibility
np.random.seed(19680801)

# create sample data
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))

# create figure and axes
fig, axs = plt.subplots()

# draw boxplot that will not show outlier points
axs.boxplot(data, 0, '')
axs.set_title('Box Plot Without Outlier Points')

# show plot
plt.show()
```

213. We can also generate a horizontal box plot.
```Python
# fix random state for reproducibility
np.random.seed(19680801)

# create sample data
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))

# create figure and axes
fig, axs = plt.subplots()

# draw horizontal boxplot
axs.boxplot(data, 0, 'rs', 0)
axs.set_title('Horizontal Box Plot')

# show plot
plt.show()
```

214. We can also change the whisker length for our box plot:
```Python
# fix random state for reproducibility
np.random.seed(19680801)

# create sample data
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))

# create figure and axes
fig, axs = plt.subplots()

# draw boxplot with modified whisker length
axs.boxplot(data, 0, 'rs', 0, 0.75)
axs.set_title('Box Plot With Modified Whisker Length')

# show plot
plt.show()
```

215. We can also set a custom fill color for our boxes:
```Python
# set random state
np.random.seed(19680801)

# load test data
all_data = [np.random.normal(0, std, size=100) for std in range(1, 4)]

# set labels
labels = ['x1', 'x2', 'x3']

# create figure and axes
fig, (ax1, ax2) = plt.subplots(nrows=1, ncols=2, figsize=(9, 4))

# rectangular box plot
bplot1 = ax1.boxplot(all_data,
                     vert=True,  # vertical box alignment
                     patch_artist=True,  # fill with color
                     labels=labels)  # will be used to label x-ticks
ax1.set_title('Rectangular box plot')

# notch shape box plot
bplot2 = ax2.boxplot(all_data,
                     notch=True,  # notch shape
                     vert=True,  # vertical box alignment
                     patch_artist=True,  # fill with color
                     labels=labels)  # will be used to label x-ticks
ax2.set_title('Notched box plot')

# color assignments
colors = ['pink', 'lightblue', 'lightgreen']
for bplot in (bplot1, bplot2):
    for patch, color in zip(bplot['boxes'], colors):
        patch.set_facecolor(color)

# add grid lines
for ax in [ax1, ax2]:
    ax.yaxis.grid(True)
    ax.set_xlabel('Three separate samples')
    ax.set_ylabel('Observed values')

# show plot
plt.show()
```

### Additional Resources

216. For more on box plots:
- [`matplotlib`, Boxplots](https://matplotlib.org/gallery/statistics/boxplot_demo.html#sphx-glr-gallery-statistics-boxplot-demo-py)
- [`matplotlib`, Box plots with custom fill colors](https://matplotlib.org/gallery/statistics/boxplot_color.html#sphx-glr-gallery-statistics-boxplot-color-py)
- [`matplotlib` Gallery, Statistics](https://matplotlib.org/gallery/index.html#statistics)
- [`matplotlib.pyplot.boxplot`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.boxplot.html)

## Tables

217. We can use the `.table()` function to create a stand-alone table or a table that would accompany another type of graphical plot.

218. In `matplotlib`, the `.table()` function generates a table plot.

219. This means the table is displaying as a static 2D visualization, just like other `matplotlib` plots.

220. To create a stacked bar chart and table with disaster data over a 100 year period:
```Python
# set data
data = [[ 66386, 174296,  75131, 577908,  32015],
        [ 58230, 381139,  78045,  99308, 160454],
        [ 89135,  80552, 152558, 497981, 603535],
        [ 78415,  81858, 150656, 193263,  69638],
        [139361, 331509, 343164, 781380,  52269]]

# create figure and axes
fig, axs = plt.subplots()

# set column labels
columns = ('Freeze', 'Wind', 'Flood', 'Quake', 'Hail')

# set row labels
rows = ['%d year' % x for x in (100, 50, 20, 10, 5)]

# set value increments
values = np.arange(0, 2500, 500)
value_increment = 1000

# set color shade
colors = plt.cm.BuPu(np.linspace(0, 0.5, len(rows)))
n_rows = len(data)

# set bar width
index = np.arange(len(columns)) + 0.3
bar_width = 0.4

# initialize the vertical-offset for the stacked bar chart.
y_offset = np.zeros(len(columns))

# plot bars and create text labels for the table
cell_text = []
for row in range(n_rows):
    plt.bar(index, data[row], bar_width, bottom=y_offset, color=colors[row])
    y_offset = y_offset + data[row]
    cell_text.append(['%1.1f' % (x / 1000.0) for x in y_offset])

# reverse colors and text labels to display the last value at the top.
colors = colors[::-1]
cell_text.reverse()

# add table at the bottom of the axes
the_table = plt.table(cellText=cell_text,
                      rowLabels=rows,
                      rowColours=colors,
                      colLabels=columns,
                      loc='bottom')

# adjust plot layout to accomodate table
plt.subplots_adjust(left=0.2, bottom=0.2)

# assign lbels and titles
plt.ylabel("Loss in ${0}'s".format(value_increment))
plt.yticks(values * value_increment, ['%d' % val for val in values])
plt.xticks([])
plt.title('Loss by Disaster')

# show plot
plt.show()
```

220. To show just the table portion from the previous example:
```Python
# set data
data = [[ 66386, 174296,  75131, 577908,  32015],
        [ 58230, 381139,  78045,  99308, 160454],
        [ 89135,  80552, 152558, 497981, 603535],
        [ 78415,  81858, 150656, 193263,  69638],
        [139361, 331509, 343164, 781380,  52269]]

# create figure and axes
fig, axs = plt.subplots()

# set column labels
column_headers = ('Freeze', 'Wind', 'Flood', 'Quake', 'Hail')

# set row labels
row_headers = ['%d year' % x for x in (100, 50, 20, 10, 5)]

# format table data as non-numeric text
cell_text = []
for row in data:
    cell_text.append([f'{x/1000:1.1f}' for x in row])
    
# set colors for row and column labels
rcolors = plt.cm.BuPu(np.full(len(row_headers), 0.1))
ccolors = plt.cm.BuPu(np.full(len(column_headers), 0.1))

# create the figure and axes with customzied visual elements
plt.figure(linewidth=2)

# add table at the bottom of the axes
the_table = plt.table(cellText=cell_text,
                      rowLabels=row_headers,
                      rowColours=rcolors,
                      rowLoc='right',
                      colColours=ccolors,
                      colLabels=column_headers,
                      loc='center')

# adjust table scale
the_table.scale(1, 1.5)

# hide plot axis
ax = plt.gca()
ax.get_xaxis().set_visible(False)
ax.get_yaxis().set_visible(False)

# hide axis border
plt.box(on=None)

# set title
plt.suptitle('Loss by Disaster')

# set footer
plt.figtext(0.95, 0.05, '30 December 2020', horizontalalignment='right', size=6, weight='light')

# center title on figure, not hidden axis
plt.draw()

# show plot
plt.show()
```

### Additional Resources

221. For more on tables in `matplotlib`:
- [`matplotlib`, Table Demo](https://matplotlib.org/gallery/misc/table_demo.html#sphx-glr-gallery-misc-table-demo-py)
- [`matplotlib.pyplot.table`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.table.html)
- Michael Demastrie, ["Simple Little Tables with Matplotlib"](https://towardsdatascience.com/simple-little-tables-with-matplotlib-9780ef5d0bc4) *Towards Data Science* (18 July 2020).

## Other Types of Plots

222. `matplotlib`  supports a wide range of plot types and customizations not covered here.

223. Other types of plots include:
- Filled polygon
- Stackplots and streamgraphs
- Image plots
- Density plots
- Contour plots
- Mesh plots
- Streamplots
- Geographic projections
- Violin plots
- Polar charts
- Custom object plots

224. That's not even getting into 3D plotting in `matplotlib`, or plotting geographic data.

225. A good place to start is the [`matplotlib` Gallery](https://matplotlib.org/gallery/), which includes sample code for different plot types.

226. ["Sample plots in matplotlib"](https://matplotlib.org/tutorials/introductory/sample_plots.html) is another starting place.

###  For 3D Plotting

227. 3D plotting resources:
- [Jake VanderPlas, "Three-Dimensional Plotting in Matplotlib" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.12-three-dimensional-plotting.html)
- [`matplotlib`, 3D surface](https://matplotlib.org/gallery/mplot3d/surface3d.html)
- [`matplotlib`, "The mplot3d Toolkit"](https://matplotlib.org/tutorials/toolkits/mplot3d.html#toolkit-mplot3d-tutorial)
- [`matplotlib` gallery, "3D plotting"](https://matplotlib.org/gallery/index.html#mplot3d-examples-index)

### Geospatial Data

228. Up to this point, we have been working with data plotted on a 2D cartesian coordinate system, with `x` and `y` axes.

229. For our purposes, it's most useful to think of maps in the same way--as data plotted on a coordinate system.

230. For geospatial data, that coordinate system is typically some type of latitude or longitude based projection.

231. The data to be plotted includes explicit location information (rather than a numerical or categorical field that can be mapped to an axis).

232. Upcoming labs will focus on plotting data stored in a Pandas `DataFrame` and building interactive visualizations.

233. We'll go into more detail on mapping in those labs.

234. A few resources we'll return to in those labs:

**Free online geocoding services:**
- [LocalFocus data journalism batch geocoder](https://geocode.localfocus.nl/)
- [Texas A&M Geocoding Services](https://geoservices.tamu.edu/Services/Geocode/)
  * *Requires creating a free account*
  
**Installing and Configuring `geopandas`**:
- Anaconda
  * Tanish Gupta, "[Fastest Way to Intsall Geopandas in Jupyter Notebooks](https://medium.com/analytics-vidhya/fastest-way-to-install-geopandas-in-jupyter-notebook-on-windows-8f734e11fa2b)" *Analytics Vidhya* (6 December 2020)
  * Anaconda, "[conda-forge packages, geopandas](https://anaconda.org/conda-forge/geopandas)" *Anaconda documentation*
  * GeoPandas, "[Installation](https://geopandas.org/getting_started/install.html)" *GeoPandas documentation*
- Google CoLab
  * Abdishakur Hassan, Jupyter notebook on using `geopandas` in Google CoLab, from "[Geographic data science tutorials with Python](https://github.com/shakasom/GDS)" *GitHub repository*
    * [Google CoLab](https://colab.research.google.com/github/shakasom/GDS/blob/master/Part1%20-%20Introduction.ipynb)
    * [GitHub](https://github.com/shakasom/GDS/blob/master/Part1%20-%20Introduction.ipynb)
    
**Getting Started With GeoPandas**:
- Jonathan Soma, "[Mapping with geopandas](https://jonathansoma.com/lede/foundations-2017/classes/geopandas/mapping-with-geopandas/)" from 2017 "[Foundations of Computing](https://jonathansoma.com/lede/foundations-2017/)" course, Columbia Graduate School of Journalism
- CoderzColumn, "[Plotting Static Maps with geopandas](https://coderzcolumn.com/tutorials/data-science/plotting-static-maps-with-geopandas-working-with-geospatial-data)" *CoderzColumn* (11 March 2020)
- GeoPandas, "[Plotting with Geoplot and GeoPandas](https://geopandas.org/gallery/plotting_with_geoplot.html)" *GeoPandas documentation*

### For More on Text and Annotation

235. A few of our examples used `matplotlib`'s annotation functionality.

236. Annotation using `.text()` can highlight specific data points or draw attention to specific elements of a plot.

237. For more on text and annotation:
- [Jake VanderPlas, "Text and Annotation" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.09-text-and-annotation.html)
- [`matplotlib` gallery, "Text, labels and annotations"](https://matplotlib.org/gallery/index.html#text-labels-and-annotations)
- [`matplotlib` Annotations](https://matplotlib.org/3.3.3/tutorials/text/annotations.html)
- [`matplotlib.pyplot.annotate`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.annotate.html)

# Lab Notebook Question 4

Q4: Write code that generates at least 3 of the following plot types.
- Figure with subplots
- Scatterplot
- Histogram
- Bar chart (regular, horizontal, stacked, or grouped)
- Pie chart
- Boxplot
- Table
- Other

Each of the three plots needs to include the following style elements (as appropriate).
- Title
- Axis labels
- Tick marks
- Tick labels
- Line or marker style
- Line or marker color
- Legend

Include code + comments.

# Saving or Exporting Plots

238. Up to this point, all of our examples have ended with the line `plt.show()`.

239. But there are many situations in which you might want or need to save a plot as a static image file.

240. We can do this using `plt.savefig()`.

241. `matplotlib` supports the following image file types:
- `.png`: portable network graphics; raster-graphics file format that supports lossless data compression
- `.pdf`: portable document format; proprietary Adobe file format; fixed-layout flat document
- `.ps`: postscript; page description language developed by Adobe
- `.eps`: encapsulated postscript; postscript document formatted as a graphics file format
- `.svg`: scalable vector graphics; vector based image based on XML

242. The basic syntax for saving a figure as an image file:
```Python
# basic syntax
plt.savefig('file_name.file_type')

# example for a png file
plt.savefig('png_sample.png')

# example for an svg file
plt.savefig('svg_sample.svg')
```

243. We can customize aspects of the saved image using other arguments in combination with `.savefig()`.

244. `dpi` can set the resolution to a numeric value.
```Python
plt.savefig('svg_sample.svg', dpi=300)
```

245. Setting `transparent` to `True` makes the image background transparent for file types that support transparent background.
```Python
plt.savefig('svg_sample.svg', transparent=True)
```

246. `bbox_inches` will alter the size of the bounding box or whitespace around the output image.

247. If no bounding box is needed, `bbox_inches='tight'` is ideal.

## Additional Resources

248. For more on customization options when saving a figure as an image:
- [`matplotlib.pyplot.savefig`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.savefig.html)

## Lab Notebook Question 5

Q5: Add lines of code for each of the plots generated for Q4 to save the plot as an image file.

# Best Practices for Data Visualization

249. By this point, your brain is probably overwhelmed by the nuances of `matplotlib` syntax.

250. Let's take a step back and think through ***why*** we want or need to visualize data, or what we hope to accomplish through visualizing data.

251. Head on over to the [Data Visualization Considerations or Best Practices](https://github.com/kwaldenphd/matplotlib-intro/blob/main/data-viz-intro.md) page to learn more about things like...
  * Choosing a chart type
  * Working with visual cues
  * Essential visualization elements

# `OO` vs. `pyplot`

252. If you start exploring `matplotlib` documentation or other internet resources/tutorials, you will likely run into `matplotlib` syntax that is different than what's presented here.

253. That is because Matplotlib has two interfaces. 

254. The first is an `object-oriented (OO) interface`. 

255. When working in the `OO` interface, we utilize an instance of `axes.Axes` to render visualizations on an instance of `figure.Figure`.

256. The second is based on `MATLAB` and uses a state-based interface. 

257. This second interface is encapsulated in the `pyplot` module. 

258. `pyplot` is a collection of functions that make matplotlib work like `MATLAB`. 

259. At first glance, `pyplot` can seem like a much easier alternative to the object-oriented interface.

260. For example, the following code generates a line plot using `pyplot` syntax:
```Python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4])

plt.ylabel('some numbers')

plt.show()
```

260. No figure, no axis- what magic!

261. Except...`pyplot` doesn't scale with multiple plots or plots  that require significant customization.

262. The `pyplot` interface hs much less flexible than the `OO` interface.

263. Plus, `matplotlib`'s own documentation recommends that you use the `OO` interface.

264. For more on the differences between these two interfaces and how to translate sample code across interfaces:
- [`matplotlib`, "Pyplot tutorial"](https://matplotlib.org/3.3.3/tutorials/introductory/pyplot.html)
- [`matplotlib`, "The Lifecycle of a Plot"](https://matplotlib.org/3.3.3/tutorials/introductory/lifecycle.html)
- Tejas Sanap, ["Pyplot vs Object Oriented Interface"](https://matplotlib.org/matplotblog/posts/pyplot-vs-object-oriented-interface/) *matplotblog* (27 May 2020)

# What's Next

265. In the next lab, we'll cover how to put `matplotlib` in conversation with `pandas` to plot data stored in a `DataFrame`.

266. We'll also look at the `seaborn` library for creating graphics.

267. We will also explore how we can use the `plotly` library for creating interactive data visualizations. 

268. Stay tuned, and fear not--this thorough intro to `matplotlib` will help immensely when adding more complexity or additional possibilities to your data visualization toolkit.

# Lab Notebook Questions

[Link to access lab notebook template (Jupyter Notebook)](https://drive.google.com/file/d/1mKVWgMdmdQ6H7ZF4lpAOVM16tTQRX_gO/view?usp=sharing)

Q1: Describe in your own words the core components of a matplotlib figure. What is the general sequence of steps involved in generating a matplotlib figure?

Q2: Describe the different types of colormaps in your own words. What are the parameters or factors to consider when choosing a colormap?

Q3: Create your own matplotlib figure and include the following style elements. Include code + comments.
- Title
- Axis labels
- Tick marks
- Tick labels
- Line or marker style
- Line or marker color
- Legend

Q4: Write code that generates at least 3 of the following plot types.
- Figure with subplots
- Scatterplot
- Histogram
- Bar chart (regular, horizontal, stacked, or grouped)
- Pie chart
- Boxplot
- Table
- Other

Each of the three plots needs to include the following style elements (as appropriate).
- Title
- Axis labels
- Tick marks
- Tick labels
- Line or marker style
- Line or marker color
- Legend

Include code + comments.

Q5: Add lines of code for each of the plots generated for Q4 to save the plot as an image file.
