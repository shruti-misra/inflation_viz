# Design Decisions and Development Process

## Design Decisions

The goal of our visualization was to create a dashboard showing how basic aspects of life are impacted by inflation. 

### Data Rationale

We first started by choosing our data of interest. Inflation rate was an obvious choice given that it was central to the visualization. We then asked the question, what are some basic economic elements of people's lives. Four categories emerged from our discussions: unemployment (people care about having a job), wages (people care about how much they earn), mortgage (people care about buying a house) and gas prices (people care about cost of transportation). Each of the four team members then researched each category to make sure they were relevant to inflation. We then gathered temporal data for each of the categories and inflation rate. 

We also considered the gas price data to encode with the inflation at the first, because it is one of the most common goods that people see daily and consume daily. But since it has already been in the CPI implicitly and its growth is just a manifestation of the inflation which is not the cause of inflation, we finally chose WTI Crude oil to encode with.

### Encoding Rationale

The data for each category was a percentage value and thus was quantitative. We had a choice between scatterplots or line charts. We ended up selecting line charts because we were interested in showing the viewer trends over time and decided that line charts do that more effectively. Furthermore, each category of data was encoded in a different color to differentiate between them. 

### Layout and Interaction Rationale

The biggest question guiding our layout and interaction choices was "what do we want out user to get out of the dashboard?" Do we want the user to just be able to compare different categories independently with inflation? or do we want the user to be able to compare categories with inflation and with each other? This was mainly a scoping issue. Eventually, we decided that we wanted to stick to having the user visualize the relationship between each category and inflation independently and not build visualization for cross-category comparisons (i.e wages vs. unemployment etc) as that would make everything too complex.

- Given our above decision we decided to choose a single graph panel with the ability to have a dropdown menu where users could choose their cateogry of interest and compare it with inflation. 

- In the graph panel, we created grey bars to mark periods of recession as defined by the Federal Reserve, as recessions are such extreme and influential period in the business cycle. The idea for the grey bar came from the visualization on the website of our data source (https://fred.stlouisfed.org/series/FPCPITOTLZGUSA). 

- While it was nice to have trendlines, we also wanted to provided the user with some details on demand such as explicit values of the data for each year. So, we incorporated the interaction technique from the "stock prices" example in the Colab notebook from the interactions lecture from class. In addition to using the sliding ruler to show percentages, we also used it to annotate the recession periods indicated by the grey bars for additional clarity. 

- Our goal with the dashboard was to provide the user with a historical overview of economic trends, but also provide the ability for the user to analyze smaller periods of time (for example trends in the 1980s, 1990s etc). This is because economic policies and circumstances vary widely through time. Our economy today is vastly different from what it was in the 1980s (for example, most of the technology sector that exists today barely existed back then). So, we added a zooming along the x-axis functionality for the user to be able to zoom into time periods they might be interested in. 

- A minor design decision was what should be the initial state of the chart. For the longest time, we had it so that initially all 5 trendlines will be displayed on the graph until the user picked an option from the dropdown. Later, we decided against it and initialized the chart to display wages vs. inflation. This was because of two reasons (1) having all the charts on one graph was overwhelming and look cluttered, especially with the oil price changes looming over everything else and (2) there was a small bug. Since the dropdown menu was also initialized to start at "unemployment", clicking "unemployment" again didn't do anything (didn't bring up the right graph). The user would first have to select a different option and then "unemployment" for the interactive filtering to work.  

- Because each category and inflation has such a complex relationship, we realized that the user would need some context to understand what's going on. So, we used the gitlab pages website to design information tabs that provided brief insight into the relationship each category had with inflation and point out some salient trends in the visualization. This information is by no means comprehensive, but hopefully is just enough for someone who doesn't know anything about inflation to get started. 

## Development Process

We initially started with discussing what variables to compare with inflation for our visualization. Four variables/categories emerged: unemployment, wages, mortgage and oil prices. Each of us then picked one category to explore its relationship with inflation further. The exploration phase roughly took an average of 2 hours per person

- Neha looked at inflation and mortgage
- Shruti looked at inflation and unemployment
- Mai looked at inflation and oil prices
- Boyuan looked at inflation and wage change

Once the data was decided the work was split into data wrangling (Mai), application design (Neha, Boyuan, Shruti (supporting)) and writeup + webpage design (Shruti, Mai)


1. Mai first put together the data in the correct format 

2. To gauge how long the application design will take Shruti created an initial prototype of the application with the graph panel with the grey bars, sliding ruler showing values per  year for all four data categories and inflation (~3 hours). 

3. Boyuan and Neha then iterated upon the prototype developed in 2 to add the dropdown filter. However, they ran into a challenge where they could not figure out double selections for the same visualization. So, instead of a sliding ruler, this next prototype had tooltips and zoom (only along the y axis) enabled. Furthermore, the tooltip was only showing up during recession years (grey bars) and the WTI Crude Oil trend line was not showing up. Also, Boyuan and Neha tried to add the interval selection feature. However, brushing is actually flatten the line curve when zooming in too much, creating some issues of overplotting, so this feature was ignored. (~7 hours).

4. Shruti was able to fix the WTI Crude Oil not showing up. It was a small textual error in the data file, so that column was not loading correctly (~ 10 minutes)

5. Boyuan was then able to get the sliding ruler pointwise selection and the dropdown menu selection to work. However, the black circle dot for the inflation chart was not showing up on the sliding ruler (~ 1 hour). We also decided to zoom along the x-axis for the temporal analysis.

6. Neha worked on figuring out how to zoom only along the x-axis (~ 2 hours)

7. Shruti fixed the black dot for inflation on the sliding ruler and zooming along the x-axis. Turns out interactive() does not work with nominal data, so the 'Year' column had to be transformed into datetime for the zoom to work. (~ 1.5 hours)

8. Shruti worked on creating the gitlab page and populating it with textual data and the visualization. Neha, Boyuan and Mai provided textual explanations for each of their categories. (~ 4 hours)

9. Mai and Shruti drafted the writeup (~ 1.5 hours)

### Challenges 

1. Double selection: it took three people to figure out how the dropdown menu interaction can be integrated with the sliding ruler. Now, we all have a better understanding of altair

2. Data Wrangling: The very first step of data wrangling took time. It also changes during the design process. Different visualiation design might require different format of datasets.

3. Zooming: figuring out how to zoom along the x-axis was challenging and took up some time because we were not familiar with altair's limitations. Turns out you can zoom with nominal and ordinal variables in altair. So, the years had to be transformed to temporal type variable. 

### Design Limitations

1. We could not figure out a way to restrict the zoom feature so that it does not zoom out or zoom out too much. Currently, you could zoom in or zoom out to the point where the visualization is unclear. 

2. Minor detail: we could not figure out how to have the "COVID-19 pandemic" annotation for the grey bar to be on two lines, so currently that annotation gets cut off a little in the native graph and needs to be zoomed out/ moved a little for the full annotation to show up.
 

## Deployment Link

This repo is deployed at: http://cse512-22sp.pages.cs.washington.edu/Poor-Grads
