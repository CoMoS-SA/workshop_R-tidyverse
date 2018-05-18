# Workshop: *Data Science with R in the tidyverse*

This repository contains the material for the PhD Workshop *R for Data Science in the tidyverse* by [Matteo Sostero](https://matteosostero.com) at [Sant'Anna School of Advanced Studies](https://www.santannapisa.it/it/istituto/economia/complexity-modellers-society-comos) (Pisa) in May 2018.
The workshop is intended mainly for first-year PhDs in Economics, but all members of the [*Computational Modellers Society*](https://www.santannapisa.it/it/istituto/economia/complexity-modellers-society-comos) are welcome to attend!

![Poster](https://images.pexels.com/photos/577585/pexels-photo-577585.jpeg?cs=srgb&dl=coding-computer-data-577585.jpg&fm=jpg)
*Image credit: [Kevin Ku](https://www.pexels.com/@kevin-ku-92347)*

The workshop covers topics on data science throughout a typical research project using the [*tidyverse*](https://www.tidyverse.org/). No prior knowledge of *R* is required! Hopefully even those of you familiar with “base R” (but not the tidyverse) will find something new.

The material is based on [*R for Data Science*](http://r4ds.had.co.nz/index.html) by Garrett Grolemund and Hadley Wickham.
See also their book [*R for Data Science: Import, Tidy, Transform, Visualize, and Model Data*](https://www.amazon.it/dp/1491910399) published by O'Reilly Media, 2017.


## Important Preparation :warning:

Please bring your **laptop** :computer: and **charger** :electric_plug:!

Preparation (10 minutes :hourglass:):

1. Install an **up-to-date** version of [R](https://cran.r-project.org/);
2. Install an **up-to-date** version of [RStudio](https://www.rstudio.com/products/rstudio/download/#download);
3. (Windows only) install [Rtools](https://cran.r-project.org/bin/windows/Rtools/);
4. Install [git](https://git-scm.com/download/) on your system;
5. Get a copy of the material by creating a new project in **RStudio**: 
    1. `File > New Project > Version Control > Git`
    2. The repository URL is [https://github.com/CoMoS-SA/workshop-R-tidyverse.git](https://github.com/CoMoS-SA/workshop-R-tidyverse.git)
    3. Create project as a subdirectory of your choice;
    4. :ballot_box_with_check: “Open in new session”
6. In RStudio, install `tidyverse` and `nycflights13`:
```R
install.packages("tidyverse")
install.packages("nycflights13")
```


## Schedule

Date                 | Time        | Room              
--                   | --          | --                
Wednesday 16/05/2018 | 10:30–12:30 | Aula 3 Toscanelli 
Thursday 17/05/2018  | 10:30–12:30 | Aula 3 Toscanelli 
Friday 18/05/2018    | 10:30–12:30 | Aula 3 Toscanelli 

By popular demand, more sessions will be scheduled in the next few weeks.


## Outline
(In no particular order):

* :page_with_curl: **Data input**: importing data from “messy” files, reading common and exotic formats and directory structures; preserving metadata; web scraping.
* :triangular_ruler: **Data transformation**: “tidying” strategies for fixing common issues with data; text processing with regular expressions; reshaping (wide-long) tabular data; merging and appending data.
* :recycle: **Automation**: using the pipe `%>%`; automate tasks with functional programming with *purrr*.
* :sparkles: **Tidy statistical modeling**: automated approaches to estimation and diagnostics.
* :bar_chart: **Visualization**: plot data with *ggplot2*; principles and recipes for visualization.


## Material
Course [slides](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/Slides%20Data%20Science%20R.pdf).

Session notebooks:
* [1-Data_transformation.md](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/notebooks/1-Data_transformation.md)
* [2-Data_types_lists_map.md](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/notebooks/2-Data_types_lists_map.md)
* [3-Data_input_output.md](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/notebooks/3-Data_input_output.md)
* [4-Tidy_modelling.md](https://github.com/CoMoS-SA/workshop-R-tidyverse/blob/master/notebooks/4-Tidy_modelling.md)

