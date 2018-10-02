# crimedata

The goal of crimedata is to access police-recorded crime data from large US 
cities using the [Open Crime Database](https://osf.io/zyaqn/) (CODE), a service 
that releases these data in a convenient format for analysis. All the data are 
available to use for free as long as you acknowledge the source of the data.

The function `get_crime_data()` returns a [tidy](https://CRAN.R-project.org/package=tidyr) 
data [tibble](https://CRAN.R-project.org/package=tibble)
of crime data with each row representing a single crime. The data provided for
each offense includes the offense type, approximate offense location and 
date/time. More fields are available for some records, depending on what data
have been released by each city. For most cities, data are available from 2010
onwards, with some available back to 2007.

More detail about what data are available, how they were constructed and the
meanings of the different categories can be found on the [CODE project 
website](https://osf.io/zyaqn/). Further detail is available in a [pre-print
data paper](https://doi.org/10.31235/osf.io/9y7qz).


## Installation

You can install crimedata from github with:

``` r
# install.packages("devtools")
devtools::install_github("mpjashby/crimedata")
```

## Examples

Data can be downloaded by year:

``` r
library(crimedata)

crime_data <- get_crime_data(years = 2007:2010)
```

The data are in a tidy format, so can be quickly manipulated using [dplyr](https://CRAN.R-project.org/package=dplyr)
verbs. For example, to analyse only personal robberies in Chicago, you can:

``` r

chicago_robberies <- get_crime_data(years = 2009) %>% 
  filter(city_name == "Chicago", offense_type == "personal robbery")

```
