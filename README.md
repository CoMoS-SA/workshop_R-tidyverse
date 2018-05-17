# Workshop: *R for Data Science in the tidyverse*

This repository contains the material for the PhD Workshop *R for Data Science in the tidyverse* in Sant'Anna School of Advanced Studies (Pisa) on May 16-17-18, 2018.

![Poster](https://images.pexels.com/photos/577585/pexels-photo-577585.jpeg?cs=srgb&dl=coding-computer-data-577585.jpg&fm=jpg)
*Image credit: [Kevin Ku](https://www.pexels.com/@kevin-ku-92347)*

The workshop is intended mainly for first-year PhDs in Economics, but all *CoMoS* modellers are welcome to attend!

The workshop covers topics on data science throughout a typical research project using the [*tidyverse*](https://www.tidyverse.org/). No prior knowledge of *R* is required! Hopefully even those of you familiar with “base R” (but not the tidyverse) will find something new.

The material is based on [*R for Data Science*](http://r4ds.had.co.nz/index.html) by Garrett Grolemund and Hadley Wickham.
See also their book [*R for Data Science: Import, Tidy, Transform, Visualize, and Model Data*](https://www.amazon.it/dp/1491910399) published by O'Reilly Media, 2017.


## Schedule

Date                 | Time        | Room              | Code 
--                   | --          | --                | --   
Wednesday 16/06/2018 | 10:30–12:30 | Aula 3 Toscanelli | [1_data_transformation.md](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/1_data_transformation.md) 
Thursday 17/06/2018  | 10:30–12:30 | Aula 3 Toscanelli |      
Friday 18/06/2018    | 10:30–12:30 | Aula 3 Toscanelli |      


## Important Preparation

* Please bring your __laptop__ and __charger__;
* Install an __up-to-date__ version of [R](https://cran.r-project.org/);
* Install an __up-to-date__ version of [RStudio](https://www.rstudio.com/products/rstudio/download/#download);
* (Windows only) install [Rtools](https://cran.r-project.org/bin/windows/Rtools/);
* Install [git](https://git-scm.com/download/) on your system;
* Get a copy of the material:
    1. Create a new project in RStudio: `File > New Project > Version Control > Git`
    2. The repository URL is [https://github.com/CoMoS-SA/workshop-R-tidyverse.git](https://github.com/CoMoS-SA/workshop-R-tidyverse.git)
    3. Open in new session
* In RStudio, install *tidyverse* and *nycflights13* in *R*:
```R
install.packages("tidyverse")
install.packages("nycflights13")
```


## Tentative outline:

* __Data input in R__: importing data from “messy” files, reading common and exotic formats and directory structures; preserving metadata; web scraping.
* __Data wrangling in R__: “tidying” strategies for fixing common issues with data; text processing with regular expressions; reshaping (wide-long) tabular data; merging and appending data.
* __Visualization__: plot data with *ggplot2*; principles and recipes for visualization.
* __Automation__: using the pipe `%>%`;  automate tasks with functional programming with *purrr*.
* __Statistical modeling__: automated approaches to estimation and model selection.
