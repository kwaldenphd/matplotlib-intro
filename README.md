# Lab #11: Introduction to matplotlib

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab  Goals

## Acknowledgements

# Table of Contents

Wes McKinneyh Chapter 9 "Plotting and Visualization"

matplotlib, ["Usage Guide"](https://matplotlib.org/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py)

matplotlib, ["Tutorials"](https://matplotlib.org/tutorials/index.html)

Eric Matthes, Python Crash Course, Chapter 15 "Generating Data"

`pandas` documentation, ["Getting Started: Plotting"](https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html)

Ventsislav Yordanov, ["Data Science with Python: Intro to Data Visualization with Matplotlib"](https://towardsdatascience.com/data-science-with-python-intro-to-data-visualization-and-matplotlib-5f799b7c6d82) *Towards Data Science* (21 July 2018)


# Getting started with `matplotlib`

For our purposes, a plot is defined as "a graphic representation (such as a chart)" (Merriam Webster).

These graphic representations of data are often called charts, graphs, figures, etc. 

In the context of programming, computer science, and data science, we refer to these as plots.

We can generate plots for data stored in `pandas` using the `matplotlib` package.

`matplotlib` was developed in 2002 as a MATLAB-like plotting interface for Python.

"Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python...Matplotlib produces publication-quality figures in a variety of hardcopy formats and interactive environments across platforms. Matplotlib can be used in Python scripts, the Python and IPython shell, web application servers, and various graphical user interface toolkits" ([Matplotlib documentation, Github](https://github.com/matplotlib/matplotlib))

As described [by the original developer John Hunter](https://matplotlib.org/users/history.html), "Matplotlib is a library for making 2D plots of arrays in Python. Although it has its origins in emulating the MATLAB graphics commands, it is independent of MATLAB, and can be used in a Pythonic, object oriented way. Although Matplotlib is written primarily in pure Python, it makes heavy use of NumPy and other extension code to provide good performance even for large arrays. Matplotlib is designed with the philosophy that you should be able to create simple plots with just a few commands, or just one! If you want to see a histogram of your data, you shouldn't need to instantiate objects, call methods, set properties, and so on; it should just work."

For more on `matplotlib`'s development and history: John Hunter, ["History"](https://matplotlib.org/users/history.html) *Matplotlib* (2008)

To be able to call the `matplotlib` API (application programming interface) within Python, we need to make sure the package is installed and loaded.
- To install at the command line: `pip install matplotlib`
- To load in a `.py` script: `import matplotlib.pyplot as plot`
- To work with `matplotlib` from a Jupyter notebook: `%matplotlib notebook`

The default `matplotlib` plot is a line plot.

```Python
# import matplotlib
import matplotlib.pyplot as plot

# import numpy
import numpy as np

# create dataset of numbers 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
data = np.arrange(10)

# create line plot of data 
plt.plot(data)
```

We pass our data to `plt.plot()` and a line plot is generated.

Plots in `matplotlib` reside within a `Figure` object.

These figures contain one or more `Axes`, which are the area where points can be added or specified usign x-y coordinates for 2-D plots.

Once the `Figure` object has been created, we can add start adding elements to the plot.

The easiest way to create a figure is using `pyplot.subplots()`.

NOTE: Because we have loaded the package using `import matplotlib.pyplot as plot`, we can use `plt` as shorthand for `pyplot`.

We can then use `axes.plot()` to create axes and add data.

Another line plot using a list of number values:
```Python
# import package
import matplotlib.pyplot as plot

# create figure with axes
fig, ax = plt.subplots()

# plot data on axes
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])
```

We can see the first list of `1, 2, 3, 4` is shown on the `X` axis.

The second list `1, 4, 2, 3` is shown on the `Y` axis.

NOTE: The `Y` axis values are plotted in the original order--for this type of plot (a line plot), `matplotlib` keeps the list data in its original order.

Let's generate a line plot using a square number sequence

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

# show plot
plt.show()
```

In this example, we import `matplotlib` and create two lists, `squares` and `input_values` that hold the data that will be plotted.

NOTE: We need to specify `input_values`, because the default in `matplotlib` will start the axis at `0`.

We then create a new variable `fig` that represents the entire figure or collection of plots.

The variable `ax` represents a single plot in the `fig` figure.

We then pass `squares` to the `plot()` method to create the plot.

And `plt.show()` opens the `matplotlib` viewer to show us the newly-generated plot.

From within the `matplotlib` viewer, we can zoom in and navigate the plot, as well as save images of the plot.

# Anatomy of a `matplotlib` figure

Before we start customizing plots or generating more complex plots, it's useful to know the components of a `matplotlib` figure.

FIGURE 1 https://matplotlib.org/_images/anatomy.png

## `Figure`

`Figure`: A figure object that can include multiple `Axes` or plots; a `Figure` contains at least one `Axes`

```Python
# create an empty figure with no axes
fig = plt.figure()

# create a figure with a single axes
fig, ax = plt.subplots()

# create a figure with a 2x2 grid of axes
fig, axs = plt.subplots(2, 2)
```

Having multiple `Axes` in the same `Figure` is useful when creating side-by-side visualizations or a dashboard-style collection of visualizations.

## `Axes`

In `matplotlib` syntax, `Axes` are what we would think of as a single plot, where data is plotted.

A `Figure` can contain many `Axes`, but a given `Axes` object can only be in one `Figure`.

For 2D visualizations, an `Axes` contains two `Axis` objects.

## `Axis`

`matplotlib` works in a Cartesian coordinate system, with an `X` (horizontal) and `Y` (vertical) axis.

In a `matplotlib` plot, the `Axis` objects set graph limits and generate tick marks and labels.

The location of ticks is determined by a `Locator` object.

Tick labels are strings formatted using `Formatter`.

## Everything Else

The other components of the `Figure` include things like axis labels, marker or line style, tick labels, figure title, etc.

Knowing how to configure or customize these plot components is not just about aesthetics--in many cases, customizing a plot is necessary for readability.

# Customizing in `matplotlib`

## Title and Axis Labels

We can start by adding a plot title, and axis labels to our square root line plot.
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

# show plot
plt.show()
```

We now see a title and axis labels.

This basic title and axis label syntax applies across different types of `matplotlib` plots.

More on that later.

## Font Size and Line Thickness

We can also customize the font size for title and labels, as well as the line thickness.

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
ax.plot(input_values, squares, linewidth-3)

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

The updated plot includes these size and thickness modifications.

## Ticks and Ticklabels

By default, `matplotlib` will use the tick locations as labels.

We can use `.set_xticks()` and `.set_xticklabels()` to set tick values and labels for the `X` axis.

`.set_yticks()` and `.set_yticklabels()` do the same for the `Y` axis.

Tick values work within the data range for each axis.

Let's say we wanted number words as tick labels for our square root plot.
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

We could also adjust the font size and rotation for those tick labels by modifying the `.set_ticklabels()` lines.
```Python
# set x axis  tick labels
ax.set_xticklabels(['zero', 'one', 'two', 'three', 'four', 'five'], rotation=30, fontsize='small')

# set y axis tick labels
ax.set_yticklabels(['zero', 'five', 'ten', 'fifteen', 'twenty', 'twenty five', 'thirty'], fontsize='small')
```

These modifications set the ticklabel font size as `small` and for the `X` axis tick labels rotate the text by 30 degrees.

We could also adjust the tick label style without adjusting the actual tick labels using `.tick_params()`.

For example, to change the font size for major tick marks on both axis:
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

In this example, the default tick values and labels will be used. 

`.tick_params()` modifies the label size for major tick marks on both the `X` and `Y` axis.

## Colors, Markers, and Line Styles

The `.plot()` function can take additional arguments that specify line style and color.

For plots that have points or markers, these same characters are used to specify point type and color.

# Line Style

Character | String Representation | Description
--- | --- | ---
`-` | `solid` | Dash; solid line style
`--` | `dashed` | Double dash; dashed line style
`-.` | `dashdot` | Dash dot; dash-dot line style
`:` | `dotted` | Colon; dotted line style

For more on customizing line styles:
- [Linestyles](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/linestyles.html)

# Marker Style

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

# Colors

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

You can also specify colors using full color names (`green`), hex strings (`#008000`), or RGB combinations (`0, 128, 0`).

`matplot` lib supports the following named color pallets:
- Base colors (character keyword arguments)
- Tableau (named color from default Tableau 10 pallette; uses `tab:blue` syntax)
- CSS (named colors from CSS; uses `black`, `dimgray`, `antiquewhite` syntax)

For more on colors in `matplotlib`:
- [List of named colors](https://matplotlib.org/3.1.1/gallery/color/named_colors.html)
- [Specifying Colors](https://matplotlib.org/3.1.1/tutorials/colors/colors.html#sphx-glr-tutorials-colors-colors-py)
- [`matplotlib.colors`](https://matplotlib.org/3.1.1/api/colors_api.html#module-matplotlib.colors)
- [Color Demo](https://matplotlib.org/3.1.1/gallery/color/color_demo.html)

## Making Style Choices

When building a plot that will have multiple lines or types of markers, line/marker style (along with color) can help distinguish each component.

In a situation where the plot will be presented or printed in black-and-white only, or viewed by an audience that may include individuals with visual impairments, intentional use of line/marker style is essential for accessibility.

When building a plot that will have multiple lines or types of markers, color (along with line/marker style) can help distinguish each component.

But relying only on color to convey meaning in a plot runs the risks of making the visual inaccessible or not meaningful to those with visual impairments.

Axis Maps's [Colorbrewer2.0](https://colorbrewer2.org/) is a useful tool for finding accessible color palletes.

### Colormaps

As described by Kenneth Moreland, "One of the most fundamental features of scientific visualiation is the process of mapping scalar values to colors" (Moreland, "Diverging Color Maps for Scientific Visualization," in *Proceedings of the 5th International Symposium on Visual Computing*, December 2009. http://dx.doi.org/10.1007/978-3-642-10520-3_9)

The color scheme or pallette for a plot is most often referred to as a colormap.

Colormaps generally fall into a few categories.

`matplotlib` includes [a wide range of built-in colormaps](https://matplotlib.org/tutorials/colors/colormaps.html), some of which are shown in the images below.

#### Sequential

FIGURE 3 https://matplotlib.org/3.1.0/_images/sphx_glr_colormaps_002.png

Sequential colormaps show change in lightness or color saturation incrementally. 

They are generally comprised of a single hue.

#### Diverging

FIGURE 4 https://matplotlib.org/3.1.0/_images/sphx_glr_colormaps_004.png

Diverging colormaps show change in lightness and possibly saturation for two different colors that meet in the middle at an unsaturated color. 

This type of colormap is most effective when data being plotted has a critical middle value, or deviates around zero.

#### Cyclic

FIGURE 5 https://matplotlib.org/3.1.1/_images/sphx_glr_colormaps_019.png

Cyclic colormaps show change in lightness for two different colors that meet in the middle and begin or end at an unsaturated color.

This type of colormap is most effective for data values that wrap around at the endpoints (i.e. phase angle, wind direction, time of day).

### Qualitative

FIGURE 6 https://matplotlib.org/3.1.1/_images/sphx_glr_colormaps_020.png

Qualitative colormaps are miscellaneous colors.

This type of colormap is most effective for information that does not have ordering or relationships.

For more on colormaps in `matplotlib`:
- [Colormaps](https://matplotlib.org/3.1.1/tutorials/colors/colormaps.html)
- [Choosing Colormaps in Matplotlib](https://matplotlib.org/tutorials/colors/colormaps.html#sphx-glr-tutorials-colors-colormaps-py)
- [Creating Colormaps in Matplotlib](https://matplotlib.org/3.1.1/tutorials/colors/colormap-manipulation.html)


## Putting it all together

So how would we use these arguments when generating a plot?

Line or marker styles and colors can be combined in a single string format.

Combining these characters opens up a wide range of customization options.

A few examples:
- `bo`: blue circle marker
- `k--`: black dashed line
- `rp`: red pentagon marker
- `cD`: cyan diamond marker

You can also specify line style using named stings.

These arguments are invoked as part of the `.plot()` function (or the equivalent function when generating other kinds of plots).

A few examples for customizing line color and style:
```Python
# set line color using named color
ax.plot(x, y, color='blue')

# set line color using color character
ax.plot(x, y, color='b')

# set line color using hex
ax.plot(x, y, color="#0000FF"

# set line color using RGB
ax.plot(x, y, color=(0, 0, 255))

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

### Style Sheets

The prospect of having to make choices about font, style, color, and formatting for every component of your plot can be daunting.

`matplotlib` includes a wide range of predefined styles.

FIGURE 2 https://matplotlib.org/3.2.1/gallery/style_sheets/style_sheets_reference.html

https://matplotlib.org/3.2.1/_images/sphx_glr_style_sheets_reference_001.png (sequential up through 027)

Similar to how `CSS` (cascading style sheets) interact with `HTML` (hyper-text markup language), these style sheets cover style and formatting elements like background colors, gridlines, line widths, fonts, font sizes, and more.

To use one of these styles, we can add a single line of code before starting to generate the plot.
```Python
# import matplotlib
import matplotlib.pyplot as plot

# create dataset for y axis
squares = [1, 4, 9, 16, 25]

# create dataset for x axis
input_values = [1, 2, 3, 4, 5]

# set plot style
plt.style.use('ggplot')

# create figure for new plot
fig, ax = plt.subplots()

# generate plot
ax.plot(input_values, squares, linewidth-3)

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

Consult the `matplotlib` ["Style sheets reference" page](https://matplotlib.org/3.2.1/gallery/style_sheets/style_sheets_reference.html) to learn more.

For those interested in data journalism, most large publications have an internal style guide. And since 2017, the AP Stylebook has included a chapter on data journalism.
- Daniel Funke, ["The updated 'Bloomberg Way' s tyle guide focuses on best practices for data and multiplatform journalism"](https://www.poynter.org/reporting-editing/2017/the-updated-bloomberg-way-style-guide-focuses-on-best-practices-for-data-and-multiplatform-journalism/) *Poynter* (18 July 2017)
- Lauren Easton, ["Digging into data journalism"](https://blog.ap.org/industry-insights/digging-into-data-journalism) *Associated Press* (26 July 2017)

## Legends

When building more complex plots with multiple lines, comparisons, etc. plot legends are essential.

Some key terms for working with `.legend()`:
- ***legend entry***: exactly one key and one label
- ***legend key***: colored/patterned marker to the left of each legend label
- ***legend label***: text which describes the handle represented by the key
- ***legend handle***: original object used to generate an appropriate entry in the legend

We can create a legend in `matplotlib` using `.legend()`.

The basic options for creating a legend:
```Python
# calling legend with automatic detection
legend()

# calling legend from existing plot element labels
legend(labels)

# calling legend by defining legend elements
legend(handles, labels)
```

For some types of visualizations, the default legend in `matplotlib` will be sufficient.

One way to build a legend is to use the `label` argument for each piece of the plot.

Using `.legend()` means the elements to be added to the legend are determined automatically.

No additional arguments are passed to the function.

Labels are set using the `.set_label()` method when creating the original handle.

Elements with an empty string as the label or a label that starts with the undescore character `_` will not be included in the legend.

```Python
# create handle for first line
line_1, = ax.plot([LINE DATA], 'b--')

# set label for line_1
line_1.set_label('Line One')

# create handle for second line
line_2, = ax.plot([LINE DATA], color='green', linestyle='-.`)

# set label for line_2
line_2.set_label('Line Two')

# create handle for third line that will NOT be included in the legend
line_3, = ax.plot([LINE DATA], color=(255, 0, 0), linestyle=':')

# alternate option to give line_3 a label but still not have it included in the legend
line_3, = ax.plot([LINE DATA], color='#000000', linestyle='-')
line_3.set_label('_Line Three')
```

In this example, `ax.legend()` will use the `label` attributes for each line to add it to the legend.

Line three will not be added because its label begins with the underscore character `_`.

We can also pass the list of handles directly to `.legend()`:
```Python
# create handle for first line
line_1, = ax.plot([LINE DATA], 'b--')

# set label for line_1
line_1.set_label('Line One')

# create handle for second line
line_2, = ax.plot([LINE DATA], color='green', linestyle='-.`)

# set label for line_2
line_2.set_label('Line Two')

# create legend
ax.legend(handles=[line_1, line_2])
```

In a situation where our handles do not have labels, we can pass both the handles and labels to `.legend()`.
```Python
ax.legend([line_1, line_2], ['Line One', 'Line Two'])
```

In some situations, we might want to create a legend with handles that don't exist in our Figure or Axes.

For example, in a situation where color has meaning, we want a legend that takes color values as handles, rather than values for data associated with a specific color.

We can create a handle just for the legend.

That is, there is no requirement for handles included in the legend to exist in the Figure or Axes.

An example where the color red is a handle for our legend.
```Python
red_patch = mpatches.Patch(color='red', label='The red data')
ax.legend(handles=[red_patch])
plt.show()
```

The same is true for line styles or marker symbols.

An example where blue lines with stars are a handle for our legend.
```Python
blue_line = mlines.Line2D([], [], color='blue', marker='*', markersize=15, label='Blue stars')
ax.legend(handles=[blue_line])
plt.show()
```

We can also customize where a legend is located for a plot using the `loc` keyword argument.

String arguments for `loc`:

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

To invoke these keyword arguments when calling the `.legend()` function:
```Python
ax.legend(loc='best')

ax.legend(handles=[line_1, line_2], loc='upper right')

ax.legend([line_1, line_2], ['Line One', 'Line Two'], loc=2)

ax.legend(handles=[red_patch], loc=7)

ax.legend(handles=[blue_line], loc='upper center')
```

In situations where we want to customize where the legend is located, we can use `bbox_to_anchor` in conjunction with `loc`.

This argument allows arbitrary placement of the legend.

`bbox` coordinates are interpreted in a coordinate system, which uses the default `Axes` or `Figure` coordinates.

A few examples:

```Python
# example that puts the legend's upper-right hand corner in the center of the axes
loc='upper right', bbox_to_anchor=(0.5, 0.5)

# example that puts the legend in the best location in the bottom right quadrant of the axes
loc='best', bbox_to_anchor=(0.5, 0., 0.5, 0.5)

# example that places legend above plot and expands legend to full given bounding box
loc='lower left', bbox_to_anchor=(0., 1.02, 1., .102), ncol=2, mode='expand', borderaxespad=0.)

# example that places a legend to the right of a plot
loc='upper left', bbox_to_anchor=(1.05, 1), borderaxespad=0.)
```

You'll notice the last two examples include additional parameters.

For more on these parameters and other `.legend()` customization options:
- [`matplotlib.pyplot.legend`](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)
- [`matplotlib` "Legend guide"](https://matplotlib.org/3.3.3/tutorials/intermediate/legend_guide.html)

# Other types of plots

## Subplots

## Scatter plots

## Histograms

## Bar charts

## Pie charts

## Tables

# Saving or exporting plots





# `OO` vs. `pyplot`



# Using `matplotlib` with `pandas`


# Practice Problems

# Lab Notebook Questions
