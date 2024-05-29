---
title: "Objects Launched into Space"
subtitle: "Proposal"
author:
  - name: "Derek Rice"
    affiliations:
      - name: "School of Information, University of Arizona"
description: "INFO526 Term Project"
format:
  html:
    code-tools: true
    code-overflow: wrap
    code-line-numbers: true
    embed-resources: true
editor: visual
code-annotations: hover
execute:
  warning: false
---

::: {.cell}

```{.r .cell-code}
if (!require("pacman"))
    install.packages("pacman")

pacman::p_load(tidyverse, tidytuesdayR, dplyr, janitor, lubridate,ggplot2)
```
:::


## Dataset: Outer Space Objects

-   The data set summarizes the number of objects launced into space from 1957 to 2023 as a function of entity.
-   The source of the dataset is the United Nations Office of Outer Space Affairs. A prior analysis of the dataset is available here: https://ourworldindata.org/grapher/yearly-number-of-objects-launched-into-outer-space
-   Dataset source: https://github.com/rfordatascience/tidytuesday/blob/master/data/2024/2024-04-23/readme.md
-   The data set is comprised of 4 columns and 1175 rows - see "head" and "glimpse" summarized herein.
-   I choose the data set because I was thinking it would be interesting to identify the countries launching gadgets into space and the magnitude of the difference between the United States and other countries.
-   A graphical plot summary of the data is provided below - the plot presents an overview of the dataset and visually displays the number of launches per entity between 1957 and 2023.


::: {.cell}

```{.r .cell-code}
# cite: https://github.com/rfordatascience/tidytuesday/blob/master/data/2024/2024-04-23/readme.md

outer_space_objects <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2024/2024-04-23/outer_space_objects.csv')
```
:::

::: {.cell}

```{.r .cell-code}
dim(outer_space_objects)
```

::: {.cell-output .cell-output-stdout}

```
[1] 1175    4
```


:::
:::

::: {.cell}

```{.r .cell-code}
head(outer_space_objects)
```

::: {.cell-output .cell-output-stdout}

```
# A tibble: 6 × 4
  Entity  Code   Year num_objects
  <chr>   <chr> <dbl>       <dbl>
1 APSCO   <NA>   2023           1
2 Algeria DZA    2002           1
3 Algeria DZA    2010           1
4 Algeria DZA    2016           3
5 Algeria DZA    2017           1
6 Angola  AGO    2017           1
```


:::
:::

::: {.cell}

```{.r .cell-code}
glimpse(outer_space_objects)
```

::: {.cell-output .cell-output-stdout}

```
Rows: 1,175
Columns: 4
$ Entity      <chr> "APSCO", "Algeria", "Algeria", "Algeria", "Algeria", "Ango…
$ Code        <chr> NA, "DZA", "DZA", "DZA", "DZA", "AGO", "AGO", NA, NA, NA, …
$ Year        <dbl> 2023, 2002, 2010, 2016, 2017, 2017, 2022, 1985, 1992, 1996…
$ num_objects <dbl> 1, 1, 1, 3, 1, 1, 1, 2, 1, 2, 1, 2, 1, 2, 1, 1, 1, 1, 1, 3…
```


:::
:::

::: {.cell}

```{.r .cell-code}
filtered_outer_space_objects = outer_space_objects %>%
  filter (Entity %in% c("United States","China","Russia","Japan","France","India","European Space Agency", "Germany"))
```
:::


## Graphical Summary of the Dataset


::: {.cell}

```{.r .cell-code}
ggplot(data = filtered_outer_space_objects, aes(x=Year, y=num_objects, color = Entity)) +
  geom_smooth(se = FALSE, method = loess) +
  labs(
    x = "year of launch",
    y = "number of objects launched",
    title = "Number of objects launched into space by year",
    subtitle = "data collected from United Nations Office of Outer Space Affairs",
    caption = "objects are defined as satelllites, probes, landers, crewed spacecrafts, and space station flights"
  ) +
  theme(
    axis.text.x = element_text(size = 8, face = "bold"),
    axis.text.y = element_text(size = 8, face = "bold"),
    plot.title = element_text (size = 10, face = "bold", hjust = 0.5),
    plot.subtitle = element_text(size = 8, face = "plain", hjust = 0.5),
    plot.caption = element_text(size = 6, face = "plain", hjust = 1),
    panel.background = element_rect(fill = "white"),
    plot.background = element_rect(fill = "white"),
    panel.grid.major = element_line(color = "gray90"),
    panel.grid.minor = element_line(color = "gray95")
  ) 
```

::: {.cell-output-display}
![](proposal_files/figure-html/unnamed-chunk-7-1.png){width=672}
:::
:::


## Description

-   The dataset comprises 4 columns and 1175 rows. The dataset summarizes space launch events between 1957 and 2023 as a function of the entity or country responsible for the launch.

-   **Entity**: <character> the country launching the space object

-   **Code**: <character> the type of gadget launched into Earth orbit or beyond (satellites, probes, landers, crewed spacecrafts, and space station components)

-   **Year**: <double-precision floating-point number> the year of the lauch

-   **num_objects**: <double-precision floating-point number> the number of objects lauched by "Entity" during a year.

## Questions

-   Question 1 - what country is most likely to become the first "space faring nation" and is there a close second?

-   Question 2 - are any of the countries in the developing world engaged in space launch events?

## Analysis plan

-   The analysis plan is to plot the data on a map and display the launches by country over time. Currently, I have no idea how to do this, create a map, and plot an event from the data set onto the map?

-   I am thinking I will need to get a map of the world with the countries displayed. Another data set with the longitude and latitude for each country may be needed.

-   The launch event data set includes country and number of launches per year, to this I am thinking I will need to add columns defining the longitude and latitude of each launch event.

-   With longitude and latitude defined for each row/event I would then plot the launches on a map.

-   Perhaps the map can be set up to display the launches year to year? I have no talent for programming so this idea of a map displaying launches by year is going to be a bit of a trick.

