---
title: "title"
subtittle: "subtitle" 
date: "09 September 2026"
author: author 
bibliography: /Users/moi/zotero/exportdb/MyLibrary.bib 
number-sections: true
toc: true
toc-depth: 3
toc-expand: 3
format:
  html:
    html-math-method: katex
    css: styles.css
    code-fold: true
execute:
    warning: false
---

# Framework 

Analyses and results in a reproducible format (code and output) following
reproducible framework [@powers2019].







``` r
#|
library(readxl)
require(openxlsx)
```

```
## Loading required package: openxlsx
```

``` r
library(here)
```

```
## here() starts at /Users/moi/ifremer/projets/00project
```

``` r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

``` r
library(ggplot2)
library(arrow)
```

```
## Warning: package 'arrow' was built under R version 4.6.1
```

```
## 
## Attaching package: 'arrow'
```

```
## The following object is masked from 'package:utils':
## 
##     timestamp
```

``` r
library(data.table)
```

```
## data.table 1.18.4 using 8 threads (see ?getDTthreads).
```

```
## Latest news: r-datatable.com
```

```
## 
## Attaching package: 'data.table'
```

```
## The following objects are masked from 'package:dplyr':
## 
##     between, first, last
```

```
## The following object is masked from 'package:base':
## 
##     %notin%
```

``` r
library(tictoc)
```

```
## 
## Attaching package: 'tictoc'
```

```
## The following object is masked from 'package:data.table':
## 
##     shift
```

``` r
library(knitr)
library(kableExtra)
```

```
## Warning: package 'kableExtra' was built under R version 4.6.1
```

```
## 
## Attaching package: 'kableExtra'
```

```
## The following object is masked from 'package:dplyr':
## 
##     group_rows
```

``` r
library(DT)
library(sf)
```

```
## Warning: package 'sf' was built under R version 4.6.1
```

```
## Linking to GEOS 3.13.0, GDAL 3.8.5, PROJ 9.5.1; sf_use_s2() is TRUE
```

``` r
here::i_am("project.Rproj")
```

```
## here() starts at /Users/moi/ifremer/projets/00project
```

# Parameters


# stuff

```
# R session information


``` r
sessioninfo::session_info()
```

```
## ─ Session info ─────────────────────────────────────────────────────────────────────────────────────────────────
##  setting  value
##  version  R version 4.6.0 (2026-04-24)
##  os       macOS Tahoe 26.6.2
##  system   aarch64, darwin23
##  ui       X11
##  language (EN)
##  collate  en_GB.UTF-8
##  ctype    en_GB.UTF-8
##  tz       Europe/Paris
##  date     2026-09-09
##  pandoc   3.10.1 @ /opt/homebrew/bin/ (via rmarkdown)
##  quarto   1.10.18 @ /usr/local/bin/quarto
## 
## ─ Packages ─────────────────────────────────────────────────────────────────────────────────────────────────────
##  package      * version date (UTC) lib source
##  arrow        * 25.0.0  2026-07-16 [1] CRAN (R 4.6.1)
##  assertthat     0.2.1   2019-03-21 [1] CRAN (R 4.6.0)
##  bit            4.6.0   2025-03-06 [1] CRAN (R 4.6.0)
##  bit64          4.8.2   2026-05-19 [1] CRAN (R 4.6.0)
##  cellranger     1.1.0   2016-07-27 [1] CRAN (R 4.6.0)
##  class          7.3-23  2025-01-01 [1] CRAN (R 4.6.0)
##  classInt       0.4-11  2025-01-08 [1] CRAN (R 4.6.0)
##  cli            3.6.6   2026-04-09 [1] CRAN (R 4.6.0)
##  data.table   * 1.18.4  2026-05-06 [1] CRAN (R 4.6.0)
##  DBI            1.3.0   2026-02-25 [1] CRAN (R 4.6.0)
##  digest         0.6.39  2025-11-19 [1] CRAN (R 4.6.0)
##  dplyr        * 1.2.1   2026-04-03 [1] CRAN (R 4.6.0)
##  DT           * 0.34.0  2025-09-02 [1] CRAN (R 4.6.0)
##  e1071          1.7-17  2025-12-18 [1] CRAN (R 4.6.0)
##  evaluate       1.0.5   2025-08-27 [1] CRAN (R 4.6.0)
##  farver         2.1.2   2024-05-13 [1] CRAN (R 4.6.0)
##  fastmap        1.2.0   2024-05-15 [1] CRAN (R 4.6.0)
##  generics       0.1.4   2025-05-09 [1] CRAN (R 4.6.0)
##  ggplot2      * 4.0.3   2026-04-22 [1] CRAN (R 4.6.0)
##  glue           1.8.1   2026-04-17 [1] CRAN (R 4.6.0)
##  gtable         0.3.6   2024-10-25 [1] CRAN (R 4.6.0)
##  here         * 1.0.2   2025-09-15 [1] CRAN (R 4.6.0)
##  htmltools      0.5.9   2025-12-04 [1] CRAN (R 4.6.0)
##  htmlwidgets    1.6.4   2023-12-06 [1] CRAN (R 4.6.0)
##  jsonlite       2.0.0   2025-03-27 [1] CRAN (R 4.6.0)
##  kableExtra   * 1.4.1   2026-07-08 [1] CRAN (R 4.6.1)
##  KernSmooth     2.23-26 2025-01-01 [1] CRAN (R 4.6.0)
##  knitr        * 1.51    2025-12-20 [1] CRAN (R 4.6.0)
##  later          1.4.8   2026-03-05 [1] CRAN (R 4.6.0)
##  lifecycle      1.0.5   2026-01-08 [1] CRAN (R 4.6.0)
##  magrittr       2.0.5   2026-04-04 [1] CRAN (R 4.6.0)
##  nvimcom      * 0.9.94  2026-04-27 [1] local
##  openxlsx     * 4.2.8.1 2025-10-31 [1] CRAN (R 4.6.0)
##  otel           0.2.0   2025-08-29 [1] CRAN (R 4.6.0)
##  pillar         1.11.1  2025-09-17 [1] CRAN (R 4.6.0)
##  pkgconfig      2.0.3   2019-09-22 [1] CRAN (R 4.6.0)
##  processx       3.9.0   2026-04-22 [1] CRAN (R 4.6.0)
##  proxy          0.4-29  2025-12-29 [1] CRAN (R 4.6.0)
##  purrr          1.2.2   2026-04-10 [1] CRAN (R 4.6.0)
##  quarto       * 1.5.1   2025-09-04 [1] CRAN (R 4.6.0)
##  R6             2.6.1   2025-02-15 [1] CRAN (R 4.6.0)
##  RColorBrewer   1.1-3   2022-04-03 [1] CRAN (R 4.6.0)
##  Rcpp           1.1.2   2026-07-05 [1] CRAN (R 4.6.1)
##  readxl       * 1.5.0   2026-05-16 [1] CRAN (R 4.6.0)
##  rlang          1.3.0   2026-07-05 [1] CRAN (R 4.6.1)
##  rmarkdown    * 2.31    2026-03-26 [1] CRAN (R 4.6.0)
##  rprojroot      2.1.1   2025-08-26 [1] CRAN (R 4.6.0)
##  rstudioapi     0.19.0  2026-06-11 [1] CRAN (R 4.6.0)
##  S7             0.2.2   2026-04-22 [1] CRAN (R 4.6.0)
##  scales         1.4.0   2025-04-24 [1] CRAN (R 4.6.0)
##  sessioninfo    1.2.4   2026-06-04 [1] CRAN (R 4.6.0)
##  sf           * 1.1-2   2026-07-23 [1] CRAN (R 4.6.1)
##  stringi        1.8.7   2025-03-27 [1] CRAN (R 4.6.0)
##  stringr        1.6.0   2025-11-04 [1] CRAN (R 4.6.0)
##  svglite        2.2.2   2025-10-21 [1] CRAN (R 4.6.0)
##  systemfonts    1.3.2   2026-03-05 [1] CRAN (R 4.6.0)
##  textshaping    1.0.5   2026-03-06 [1] CRAN (R 4.6.0)
##  tibble         3.3.1   2026-01-11 [1] CRAN (R 4.6.0)
##  tictoc       * 1.2.1   2024-03-18 [1] CRAN (R 4.6.0)
##  tidyselect     1.2.1   2024-03-11 [1] CRAN (R 4.6.0)
##  units          1.0-1   2026-03-11 [1] CRAN (R 4.6.0)
##  vctrs          0.7.3   2026-04-11 [1] CRAN (R 4.6.0)
##  viridisLite    0.4.3   2026-02-04 [1] CRAN (R 4.6.0)
##  withr          3.0.3   2026-06-19 [1] CRAN (R 4.6.0)
##  xfun           0.60    2026-07-09 [1] CRAN (R 4.6.1)
##  xml2           1.6.0   2026-06-22 [1] CRAN (R 4.6.1)
##  yaml           2.3.12  2025-12-10 [1] CRAN (R 4.6.0)
##  zip            3.0.1   2026-07-13 [1] CRAN (R 4.6.1)
## 
##  [1] /Library/Frameworks/R.framework/Versions/4.6/Resources/library
##  * ── Packages attached to the search path.
## 
## ────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

# Bilbiography
