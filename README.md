<!-- README.md is generated from README.Rmd. Please edit that file -->
Pollen - tools for working with aerobiological data
===================================================

[![Build Status](https://travis-ci.org/Nowosad/pollen.png?branch=master)](https://travis-ci.org/Nowosad/pollen) [![CRAN version](http://www.r-pkg.org/badges/version/pollen)](http://cran.r-project.org/package=pollen)

Installation
------------

``` r
devtools::install_github("nowosad/pollen")
```

Examples
--------

``` r
library('pollen')
```

``` r
data('pollen_count')
head(pollen_count)
#>   site       date alder birch hazel
#> 1   Oz 2007-01-01     0     0     0
#> 2   Oz 2007-01-02     0     0     0
#> 3   Oz 2007-01-03     0     0     0
#> 4   Oz 2007-01-04     0     0     0
#> 5   Oz 2007-01-05     0     0     0
#> 6   Oz 2007-01-06     0     0     0
```

``` r
df <- subset(pollen_count, site=='Oz')
pollen_season(df, value="birch", date="date", method="95")
#>    year      start        end
#> 1  2007 2007-03-31 2007-05-03
#> 2  2008 2008-04-19 2008-05-07
#> 3  2009 2009-04-09 2009-05-09
#> 4  2010 2010-04-14 2010-05-07
#> 5  2011 2011-04-20 2011-05-17
#> 6  2012 2012-04-09 2012-05-14
#> 7  2013 2013-04-09 2013-05-09
#> 8  2014 2014-04-08 2014-05-10
#> 9  2015 2015-04-08 2015-04-30
#> 10 2016 2016-04-06 2016-05-09
```

``` r
df2 <- subset(pollen_count, site=='Atlantis')
pollen_season(df2, value="alder", date="date", method="95")
#>    year      start        end
#> 1  2007       <NA>       <NA>
#> 2  2008 2008-03-23 2008-04-14
#> 3  2009 2009-03-16 2009-04-03
#> 4  2010 2010-03-26 2010-04-07
#> 5  2011 2011-03-28 2011-04-14
#> 6  2012 2012-02-13 2012-04-05
#> 7  2013 2013-02-05 2013-03-16
#> 8  2014 2014-02-11 2014-04-29
#> 9  2015 2015-03-19 2015-04-04
#> 10 2016 2016-03-14 2016-04-23
```

``` r
library('purrr')
pollen_count %>% split(., .$site) %>% 
                map_df(~pollen_season(., value="hazel", date="date", method="95"), .id="site")
#>                 site year      start        end
#> 1           Atlantis 2007 2007-01-29 2007-03-19
#> 2           Atlantis 2008 2008-03-23 2008-04-14
#> 3           Atlantis 2009 2009-03-15 2009-04-11
#> 4           Atlantis 2010 2010-03-24 2010-04-14
#> 5           Atlantis 2011 2011-03-26 2011-04-12
#> 6           Atlantis 2012 2012-01-21 2012-03-26
#> 7           Atlantis 2013 2013-02-02 2013-03-29
#> 8           Atlantis 2014 2014-02-07 2014-04-09
#> 9           Atlantis 2015 2015-03-01 2015-03-30
#> 10          Atlantis 2016 2016-03-11 2016-04-06
#> 11 Hundred Acre Wood 2007 2007-01-29 2007-03-31
#> 12 Hundred Acre Wood 2008 2008-03-10 2008-05-10
#> 13 Hundred Acre Wood 2009 2009-02-08 2009-03-31
#> 14 Hundred Acre Wood 2010 2010-01-24 2010-04-16
#> 15 Hundred Acre Wood 2011 2011-03-25 2011-04-16
#> 16 Hundred Acre Wood 2012 2012-01-10 2012-03-29
#> 17 Hundred Acre Wood 2013 2013-01-24 2013-03-12
#> 18 Hundred Acre Wood 2014 2014-03-04 2014-03-31
#> 19 Hundred Acre Wood 2015 2015-02-26 2015-03-31
#> 20 Hundred Acre Wood 2016 2016-02-06 2016-03-31
#> 21                Oz 2007 2007-02-03 2007-03-18
#> 22                Oz 2008 2008-03-10 2008-04-03
#> 23                Oz 2009 2009-02-17 2009-03-26
#> 24                Oz 2010 2010-03-18 2010-04-10
#> 25                Oz 2011 2011-03-27 2011-04-13
#> 26                Oz 2012 2012-01-12 2012-03-14
#> 27                Oz 2013 2013-01-22 2013-03-25
#> 28                Oz 2014 2014-03-05 2014-04-05
#> 29                Oz 2015 2015-03-19 2015-04-02
#> 30                Oz 2016 2016-03-10 2016-03-30
#> 31             Shire 2007 2007-01-28 2007-03-24
#> 32             Shire 2008 2008-02-22 2008-04-01
#> 33             Shire 2009 2009-02-03 2009-03-27
#> 34             Shire 2010 2010-02-07 2010-04-07
#> 35             Shire 2011 2011-02-20 2011-04-12
#> 36             Shire 2012 2012-01-10 2012-03-18
#> 37             Shire 2013 2013-01-21 2013-03-02
#> 38             Shire 2014 2014-03-01 2014-03-27
#> 39             Shire 2015 2015-02-19 2015-03-30
#> 40             Shire 2016 2016-01-17 2016-03-28
```
