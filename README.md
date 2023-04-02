
<!-- README.md is generated from README.Rmd. Please edit that file -->

# forgot <img src="man/figures/logo.png" align="right" height="139" />

<!-- badges: start -->
<!-- badges: end -->

The goal of forgot is to help you search for that one function you need
in that one package. This package is based on functions from
[Rd2roxygen](https://github.com/yihui/Rd2roxygen). The `forgot()`
function returns a tibble of section content in R documentation files
from a specified package (that’s already installed). You can search on
this tibble and return an interactive HTML table if needed.

## Installation

You can install the development version of forgot like so:

``` r
# install.packages("devtools")
devtools::install_github("parmsam/forgot")
```

## Example

This is a basic example which shows you how to solve a common problem:

Create a forgot tibble that has columns for doc sections in package
functions

``` r
library(forgot)
library(dplyr)
## basic example code
functions_in_pkg <- forgot("stringr")
functions_in_pkg %>% 
  select(function_name, title, desc) %>%
  head()
#> # A tibble: 6 × 3
#>   function_name title                                                      desc 
#>   <chr>         <chr>                                                      <chr>
#> 1 case          Convert string to upper case, lower case, title case, or … "\n\…
#> 2 invert_match  Switch location of matches to location of non-matches      "\nI…
#> 3 modifiers     Control matching behaviour with modifier functions         "\nM…
#> 4 %>%           Pipe operator                                              "\nP…
#> 5 str_c         Join multiple strings into one string                      "\n\…
#> 6 str_conv      Specify the encoding of a string                           "\nT…
```

Search for a keyword of interest in the forgot tibble

``` r
forgot("stringr", keyword = "count")
#> # A tibble: 5 × 13
#>   function…¹ title usage desc  value author examp…² name  aliases params keywo…³
#>   <chr>      <chr> <chr> <chr> <chr> <chr>  <chr>   <chr> <chr>   <chr>  <chr>  
#> 1 modifiers  Cont… "\nf… "\nM… "\nA… "char… "\npat… modi… "c(\"m… "c(\"… NULL   
#> 2 str_count  Coun… "\ns… "\nC… "\nA… "char… "\nfru… str_… "NULL"  "c(\"… NULL   
#> 3 str_interp Stri… "\ns… "\n\… "\nA… "\nSt… "\n\n#… str_… "NULL"  "c(\"… intern…
#> 4 str_split  Spli… "\ns… "\nT… "\n\… "char… "\nfru… str_… "c(\"s… "c(\"… NULL   
#> 5 word       Extr… "\nw… "\nE… "\nA… "char… "\nsen… word  "NULL"  "c(\"… NULL   
#> # … with 2 more variables: seealso <chr>, format <chr>, and abbreviated
#> #   variable names ¹​function_name, ²​examples, ³​keywords
```

Or search for a keyword of interest only on specific fields

``` r
forgot("stringr", keyword = "count", selected = c("title", "desc"))
#> # A tibble: 1 × 3
#>   function_name title                   desc                                    
#>   <chr>         <chr>                   <chr>                                   
#> 1 str_count     Count number of matches "\nCounts the number of times \\code{pa…
```

Or if you want to search across multiple packages

``` r
library(purrr)
c("stringr", "dplyr") %>%
  purrr::set_names() %>%
  map(forgot, keyword = "count")
```

Alternatively, here’s how you can get a reactable HTML table that you
can search on

``` r
forgot("stringr", keyword = "count", selected = c("title", "desc"),
               interactive = T)
```

## Credits

- Hex icon created using the [hexmake
  app](https://connect.thinkr.fr/hexmake/) from
  [ColinFay](https://github.com/ColinFay/hexmake).
- <a href="https://www.flaticon.com/free-icons/confusion" title="confusion icons">Confusion
  icons created by Freepik - Flaticon</a>
