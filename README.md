
<!-- README.md is generated from README.Rmd. Please edit that file -->

# forgot <img src="man/figures/logo.png" align="right" height="139" />

<!-- badges: start -->
<!-- badges: end -->

The goal of forgot is to help you search for that one function you need
in that one package. This package is based on functions from
[Rd2roxygen](https://github.com/yihui/Rd2roxygen). The `forgot()`
function returns a tibble of section content in R documentation files
from a specified package (that’s already installed). You can search on
this tibble and return an interactive HTML table if needed. There’s also
a RStudio Addin included that you can use to search package
documentation in a small Shiny app. `forgot2()` is for more casual use
and will return a simple version of the forgot tibble with just the
first two columns by default.

This package provides an alternative to function search without using
the help system (`?help()`) in the RStudio IDE. You should still use
that though for learning purposes.

## Installation

You can install the development version of forgot like so:

``` r
# install.packages("devtools")
devtools::install_github("parmsam/forgot")
```

## Examples

This are examples which show you how to solve common problems:

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
#>   function_name title     usage desc  value author examples name  aliases params
#>   <chr>         <chr>     <chr> <chr> <chr> <chr>  <chr>    <chr> <chr>   <chr> 
#> 1 modifiers     Control … "\nf… "\nM… "\nA… "char… "\npatt… modi… "c(\"m… "c(\"…
#> 2 str_count     Count nu… "\ns… "\nC… "\nA… "char… "\nfrui… str_… "NULL"  "c(\"…
#> 3 str_interp    String i… "\ns… "\n\… "\nA… "\nSt… "\n\n# … str_… "NULL"  "c(\"…
#> 4 str_split     Split up… "\ns… "\nT… "\n\… "char… "\nfrui… str_… "c(\"s… "c(\"…
#> 5 word          Extract … "\nw… "\nE… "\nA… "char… "\nsent… word  "NULL"  "c(\"…
#> # ℹ 3 more variables: keywords <chr>, seealso <chr>, format <chr>
```

Or search for a keyword of interest only on specific fields

``` r
forgot("stringr", keyword = "count", selected = c("title", "desc"))
#> # A tibble: 1 × 3
#>   function_name title                   desc                                    
#>   <chr>         <chr>                   <chr>                                   
#> 1 str_count     Count number of matches "\nCounts the number of times \\code{pa…
```

If you want to search across multiple packages, here’s an example of how
you can use purrr to help with that

``` r
library(purrr)
c("stringr", "dplyr") %>%
  purrr::set_names() %>%
  map(forgot, keyword = "count") %>%
  list_rbind(names_to = "Package")
```

Lastly, here’s how you can get a reactable HTML table that you can
search on

``` r
forgot("stringr", keyword = "count", selected = c("title", "desc"),
               interactive = T)
```

### Cat a roxygen2 field of interest into your R console

Here’s how you can cat (?`cat()` for more info) the parameter field,
usage field, or example field. Try it out to see how it looks.

``` r
forgot_params("dplyr", "count")
forgot_usg("dplyr", "count")
forgot_exmpls("dplyr", "count")
```

The write logical (see `forgot_exmpls()` documentation for example)
argument will create a new RStudio document with the roxygen2 field
content of interest that was cat.

### Shortcuts

You can also use some shortcut operators to get the same results as
above.

``` r
# shortcut for forgot2
"dplyr" %f2% "count"
## OR
dplyr %f2% "count"
# shortcut for forgot_usg
"dplyr" %fu% "count"
## OR
dplyr %fu% count
# shortcut for forgot_exmpls
"dplyr" %fe% "count"
## OR
dplyr %fe% count

# shortcut for forgot_params
"dplyr" %fp% "count"
## OR
dplyr %fp% count
```

## Credits

- Hex icon created using the [hexmake
  app](https://connect.thinkr.fr/hexmake/) from
  [ColinFay](https://github.com/ColinFay/hexmake).
- <a href="https://www.flaticon.com/free-icons/confusion" title="confusion icons">Confusion
  icons created by Freepik - Flaticon</a>
