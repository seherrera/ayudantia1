Untitled
================

``` r
library(quanteda)
```

    ## Warning: package 'quanteda' was built under R version 4.0.5

    ## Package version: 3.0.0
    ## Unicode version: 10.0
    ## ICU version: 61.1

    ## Parallel computing: 4 of 4 threads used.

    ## See https://quanteda.io for tutorials and examples.

``` r
library(dplyr)
```

    ## Warning: package 'dplyr' was built under R version 4.0.4

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.0.5

    ## -- Attaching packages ---------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.0.3     v stringr 1.4.0
    ## v tidyr   1.1.3     v forcats 0.5.0
    ## v readr   1.3.1

    ## Warning: package 'ggplot2' was built under R version 4.0.4

    ## Warning: package 'tidyr' was built under R version 4.0.4

    ## -- Conflicts ------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(utf8)
library(ggplot2)
setwd("C:/Users/sebah/Desktop/U/mineria de datos/ayudantia 2")
primer_tiempo2020 <- read_csv("Primer_Tiempo2020.csv", col_names = TRUE)
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_double(),
    ##   torneo = col_character(),
    ##   equipo = col_character(),
    ##   id_partido = col_character(),
    ##   partido = col_character(),
    ##   fasepartido = col_character(),
    ##   local = col_logical(),
    ##   tiempo = col_character()
    ## )

    ## See spec(...) for full column specifications.

``` r
#str(primer_tiempo2020)
attach(primer_tiempo2020)
summary(primer_tiempo2020)
```

    ##     torneo             equipo           id_partido          partido         
    ##  Length:130         Length:130         Length:130         Length:130        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  fasepartido          local            tiempo           accuratePass  
    ##  Length:130         Mode :logical   Length:130         Min.   : 62.0  
    ##  Class :character   FALSE:65        Class :character   1st Qu.:115.2  
    ##  Mode  :character   TRUE :65        Mode  :character   Median :143.5  
    ##                                                        Mean   :147.5  
    ##                                                        3rd Qu.:181.2  
    ##                                                        Max.   :269.0  
    ##    wonTackle       lostCorners    goalsConceded        saves    
    ##  Min.   : 0.000   Min.   :0.000   Min.   :0.0000   Min.   :0.0  
    ##  1st Qu.: 3.000   1st Qu.:1.000   1st Qu.:0.0000   1st Qu.:1.0  
    ##  Median : 5.000   Median :2.000   Median :0.0000   Median :1.0  
    ##  Mean   : 5.154   Mean   :2.277   Mean   :0.5923   Mean   :1.5  
    ##  3rd Qu.: 7.000   3rd Qu.:3.000   3rd Qu.:1.0000   3rd Qu.:2.0  
    ##  Max.   :14.000   Max.   :7.000   Max.   :3.0000   Max.   :5.0  
    ##  ontargetScoringAtt totalScoringAtt     subsMade       totalThrows   
    ##  Min.   :0.000      Min.   : 0.000   Min.   :0.0000   Min.   : 3.00  
    ##  1st Qu.:1.000      1st Qu.: 4.000   1st Qu.:0.0000   1st Qu.: 8.00  
    ##  Median :2.000      Median : 6.000   Median :0.0000   Median :11.00  
    ##  Mean   :2.108      Mean   : 5.938   Mean   :0.1077   Mean   :10.98  
    ##  3rd Qu.:3.000      3rd Qu.: 7.750   3rd Qu.:0.0000   3rd Qu.:13.00  
    ##  Max.   :5.000      Max.   :14.000   Max.   :1.0000   Max.   :26.00  
    ##  totalYellowCard    goalKicks        totalPass       fkFoulWon     
    ##  Min.   :0.0000   Min.   : 0.000   Min.   : 93.0   Min.   : 2.000  
    ##  1st Qu.:0.0000   1st Qu.: 2.000   1st Qu.:159.5   1st Qu.: 5.000  
    ##  Median :1.0000   Median : 4.000   Median :189.0   Median : 6.000  
    ##  Mean   :0.9077   Mean   : 3.962   Mean   :190.9   Mean   : 6.338  
    ##  3rd Qu.:1.0000   3rd Qu.: 5.000   3rd Qu.:222.5   3rd Qu.: 8.000  
    ##  Max.   :3.0000   Max.   :11.000   Max.   :304.0   Max.   :12.000  
    ##   totalTackle       fkFoulLost     possessionPercentage totalClearance  
    ##  Min.   : 1.000   Min.   : 2.000   Min.   :23.60        Min.   : 0.000  
    ##  1st Qu.: 5.000   1st Qu.: 6.000   1st Qu.:45.62        1st Qu.: 4.000  
    ##  Median : 7.000   Median : 7.000   Median :50.00        Median : 7.000  
    ##  Mean   : 7.192   Mean   : 7.054   Mean   :50.00        Mean   : 7.385  
    ##  3rd Qu.: 9.000   3rd Qu.: 9.000   3rd Qu.:54.38        3rd Qu.:10.000  
    ##  Max.   :15.000   Max.   :13.000   Max.   :76.40        Max.   :16.000  
    ##  formationUsed blockedScoringAtt   goalAssist         goals       
    ##  Min.   :0     Min.   :0.000     Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0     1st Qu.:0.000     1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0     Median :1.000     Median :0.0000   Median :0.0000  
    ##  Mean   :0     Mean   :1.262     Mean   :0.3769   Mean   :0.5923  
    ##  3rd Qu.:0     3rd Qu.:2.000     3rd Qu.:1.0000   3rd Qu.:1.0000  
    ##  Max.   :0     Max.   :6.000     Max.   :2.0000   Max.   :3.0000  
    ##   totalOffside   shotOffTarget     wonCorners     cornerTaken   
    ##  Min.   :0.000   Min.   :0.000   Min.   :0.000   Min.   :0.000  
    ##  1st Qu.:0.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median :1.000   Median :2.000   Median :2.000   Median :2.000  
    ##  Mean   :1.038   Mean   :2.569   Mean   :2.277   Mean   :2.269  
    ##  3rd Qu.:2.000   3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :5.000   Max.   :7.000   Max.   :7.000   Max.   :7.000  
    ##  penaltyConceded   penaltyFaced    penGoalsConceded   penaltyWon    
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0.0000   Median :0.0000   Median :0.0000   Median :0.0000  
    ##  Mean   :0.1692   Mean   :0.1692   Mean   :0.1308   Mean   :0.1692  
    ##  3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000  
    ##  Max.   :2.0000   Max.   :2.0000   Max.   :1.0000   Max.   :2.0000  
    ##     ownGoals        penaltySave       secondYellow      totalRedCard    
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.00000   Median :0.00000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.02308   Mean   :0.02308   Mean   :0.01538   Mean   :0.04615  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000  
    ##  posesion_Rival  precision_pases precision_tiros  minutos_juego  
    ##  Min.   :23.60   Min.   :50.68   Min.   :  0.00   Min.   :10.62  
    ##  1st Qu.:45.62   1st Qu.:70.71   1st Qu.: 25.00   1st Qu.:20.53  
    ##  Median :50.00   Median :76.40   Median : 40.00   Median :22.50  
    ##  Mean   :50.00   Mean   :75.99   Mean   : 41.20   Mean   :22.50  
    ##  3rd Qu.:54.38   3rd Qu.:82.28   3rd Qu.: 57.14   3rd Qu.:24.47  
    ##  Max.   :76.40   Max.   :89.43   Max.   :100.00   Max.   :34.38  
    ##  minutos_juegorival golesSalvados   foulsInofensivos cortarJuegoContrario
    ##  Min.   :10.62      Min.   :0.000   Min.   : 1.000   Min.   : 4.00       
    ##  1st Qu.:20.53      1st Qu.:1.000   1st Qu.: 5.000   1st Qu.:10.00       
    ##  Median :22.50      Median :1.000   Median : 6.000   Median :12.00       
    ##  Mean   :22.50      Mean   :1.523   Mean   : 6.146   Mean   :12.21       
    ##  3rd Qu.:24.47      3rd Qu.:2.000   3rd Qu.: 8.000   3rd Qu.:15.00       
    ##  Max.   :34.38      Max.   :5.000   Max.   :11.000   Max.   :24.00       
    ##   juegoCortado  
    ##  Min.   : 8.00  
    ##  1st Qu.:17.00  
    ##  Median :20.00  
    ##  Mean   :20.64  
    ##  3rd Qu.:25.00  
    ##  Max.   :40.00

``` r
## Borrar Datos Char

primer_tiempo2020
```

    ## # A tibble: 130 x 49
    ##    torneo equipo id_partido partido fasepartido local tiempo accuratePass
    ##    <chr>  <chr>  <chr>      <chr>   <chr>       <lgl> <chr>         <dbl>
    ##  1 Prime~ Uni<f~ 6xszsf73j~ Univer~ Regular Se~ FALSE fh              235
    ##  2 Prime~ Unive~ 6xszsf73j~ Univer~ Regular Se~ TRUE  fh              199
    ##  3 Prime~ Evert~ e88gat05j~ Univer~ Regular Se~ FALSE fh              157
    ##  4 Prime~ Unive~ e88gat05j~ Univer~ Regular Se~ TRUE  fh              192
    ##  5 Prime~ Curic~ 35ijq76er~ Univer~ Regular Se~ FALSE fh              142
    ##  6 Prime~ Unive~ 35ijq76er~ Univer~ Regular Se~ TRUE  fh              168
    ##  7 Prime~ Coqui~ 9o9ji2f68~ Univer~ Regular Se~ FALSE fh              190
    ##  8 Prime~ Unive~ 9o9ji2f68~ Univer~ Regular Se~ TRUE  fh              200
    ##  9 Prime~ Santi~ 357wqv370~ Univer~ Regular Se~ FALSE fh              156
    ## 10 Prime~ Unive~ 357wqv370~ Univer~ Regular Se~ TRUE  fh               92
    ## # ... with 120 more rows, and 41 more variables: wonTackle <dbl>,
    ## #   lostCorners <dbl>, goalsConceded <dbl>, saves <dbl>,
    ## #   ontargetScoringAtt <dbl>, totalScoringAtt <dbl>, subsMade <dbl>,
    ## #   totalThrows <dbl>, totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>,
    ## #   fkFoulWon <dbl>, totalTackle <dbl>, fkFoulLost <dbl>,
    ## #   possessionPercentage <dbl>, totalClearance <dbl>, formationUsed <dbl>,
    ## #   blockedScoringAtt <dbl>, goalAssist <dbl>, goals <dbl>, totalOffside <dbl>,
    ## #   shotOffTarget <dbl>, wonCorners <dbl>, cornerTaken <dbl>,
    ## #   penaltyConceded <dbl>, penaltyFaced <dbl>, penGoalsConceded <dbl>,
    ## #   penaltyWon <dbl>, ownGoals <dbl>, penaltySave <dbl>, secondYellow <dbl>,
    ## #   totalRedCard <dbl>, posesion_Rival <dbl>, precision_pases <dbl>,
    ## #   precision_tiros <dbl>, minutos_juego <dbl>, minutos_juegorival <dbl>,
    ## #   golesSalvados <dbl>, foulsInofensivos <dbl>, cortarJuegoContrario <dbl>,
    ## #   juegoCortado <dbl>

``` r
primer_tiempo2020 <- primer_tiempo2020[,!(colnames(primer_tiempo2020) %in% c("id_partido", "fasepartido", "local", "tiempo","formationUsed", "torneo"))]
primer_tiempo2020
```

    ## # A tibble: 130 x 43
    ##    equipo partido accuratePass wonTackle lostCorners goalsConceded saves
    ##    <chr>  <chr>          <dbl>     <dbl>       <dbl>         <dbl> <dbl>
    ##  1 Uni<f~ Univer~          235         2           3             1     4
    ##  2 Unive~ Univer~          199         2           0             0     1
    ##  3 Evert~ Univer~          157         7           6             0     3
    ##  4 Unive~ Univer~          192         4           1             0     2
    ##  5 Curic~ Univer~          142         6           3             2     2
    ##  6 Unive~ Univer~          168         8           1             1     2
    ##  7 Coqui~ Univer~          190         3           0             0     2
    ##  8 Unive~ Univer~          200         5           0             0     0
    ##  9 Santi~ Univer~          156         4           3             0     0
    ## 10 Unive~ Univer~           92         4           1             1     1
    ## # ... with 120 more rows, and 36 more variables: ontargetScoringAtt <dbl>,
    ## #   totalScoringAtt <dbl>, subsMade <dbl>, totalThrows <dbl>,
    ## #   totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>, fkFoulWon <dbl>,
    ## #   totalTackle <dbl>, fkFoulLost <dbl>, possessionPercentage <dbl>,
    ## #   totalClearance <dbl>, blockedScoringAtt <dbl>, goalAssist <dbl>,
    ## #   goals <dbl>, totalOffside <dbl>, shotOffTarget <dbl>, wonCorners <dbl>,
    ## #   cornerTaken <dbl>, penaltyConceded <dbl>, penaltyFaced <dbl>,
    ## #   penGoalsConceded <dbl>, penaltyWon <dbl>, ownGoals <dbl>,
    ## #   penaltySave <dbl>, secondYellow <dbl>, totalRedCard <dbl>,
    ## #   posesion_Rival <dbl>, precision_pases <dbl>, precision_tiros <dbl>,
    ## #   minutos_juego <dbl>, minutos_juegorival <dbl>, golesSalvados <dbl>,
    ## #   foulsInofensivos <dbl>, cortarJuegoContrario <dbl>, juegoCortado <dbl>

``` r
## Analisis descriptivo


fh2020 <- primer_tiempo2020[order(primer_tiempo2020$saves, decreasing = TRUE),]
fh2020
```

    ## # A tibble: 130 x 43
    ##    equipo partido accuratePass wonTackle lostCorners goalsConceded saves
    ##    <chr>  <chr>          <dbl>     <dbl>       <dbl>         <dbl> <dbl>
    ##  1 Unive~ Uni<f3~          182         5           1             1     5
    ##  2 Depor~ Uni<f3~           74         3           2             0     5
    ##  3 Depor~ Deport~          154         4           2             0     5
    ##  4 Uni<f~ Univer~          235         2           3             1     4
    ##  5 Coqui~ Uni<f3~           82         7           6             1     4
    ##  6 Santi~ O'Higg~          123         5           1             1     4
    ##  7 Evert~ Univer~          157         7           6             0     3
    ##  8 Uni<f~ Uni<f3~          252         6           3             1     3
    ##  9 Unive~ Santia~           95         5           1             0     3
    ## 10 Santi~ Santia~           84         8           2             0     3
    ## # ... with 120 more rows, and 36 more variables: ontargetScoringAtt <dbl>,
    ## #   totalScoringAtt <dbl>, subsMade <dbl>, totalThrows <dbl>,
    ## #   totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>, fkFoulWon <dbl>,
    ## #   totalTackle <dbl>, fkFoulLost <dbl>, possessionPercentage <dbl>,
    ## #   totalClearance <dbl>, blockedScoringAtt <dbl>, goalAssist <dbl>,
    ## #   goals <dbl>, totalOffside <dbl>, shotOffTarget <dbl>, wonCorners <dbl>,
    ## #   cornerTaken <dbl>, penaltyConceded <dbl>, penaltyFaced <dbl>,
    ## #   penGoalsConceded <dbl>, penaltyWon <dbl>, ownGoals <dbl>,
    ## #   penaltySave <dbl>, secondYellow <dbl>, totalRedCard <dbl>,
    ## #   posesion_Rival <dbl>, precision_pases <dbl>, precision_tiros <dbl>,
    ## #   minutos_juego <dbl>, minutos_juegorival <dbl>, golesSalvados <dbl>,
    ## #   foulsInofensivos <dbl>, cortarJuegoContrario <dbl>, juegoCortado <dbl>

``` r
## Sub DataFrames


fh2020_rendimiento = fh2020[,colnames(primer_tiempo2020) %in% c("equipo", "partido", "saves", "possessionPercentage", "precision_rendimiento")]
fh2020_rendimiento = fh2020_rendimiento[order(fh2020_rendimiento$possessionPercentage, decreasing = TRUE),]
fh2020_rendimiento
```

    ## # A tibble: 130 x 4
    ##    equipo            partido                            saves possessionPercent~
    ##    <chr>             <chr>                              <dbl>              <dbl>
    ##  1 Universidad Cat<~ Universidad Cat<f3>lica vs Deport~     2               76.4
    ##  2 Deportivo Antofa~ Deportivo Antofagasta vs Universi~     1               69.4
    ##  3 Uni<f3>n La Cale~ Uni<f3>n La Calera vs Coquimbo Un~     0               68.8
    ##  4 Colo Colo         Colo Colo vs Universidad Concepci~     0               68.2
    ##  5 Uni<f3>n Espa<f1~ Uni<f3>n Espa<f1>ola vs Huachipato     0               67.8
    ##  6 Curic<f3> Unido   Universidad Concepci<f3>n vs Curi~     2               67.7
    ##  7 Palestino         Palestino vs Deportivo Antofagasta     1               65.7
    ##  8 Audax Italiano    Audax Italiano vs Colo Colo            0               65.5
    ##  9 Uni<f3>n Espa<f1~ Uni<f3>n Espa<f1>ola vs Palestino      0               65  
    ## 10 Uni<f3>n La Cale~ Uni<f3>n La Calera vs La Serena        3               64.8
    ## # ... with 120 more rows

``` r
fh2020_fauls <- NULL
fh2020_fauls = fh2020[,colnames(primer_tiempo2020) %in% c("equipo", "partido", "totalTackle", "totalYellowCard", "fkFoulWon", "fkFoulLost", "totalOffside", "totalRedCard")]
fh2020_fauls = fh2020_fauls[order(fh2020_fauls$totalYellowCard, decreasing = TRUE),]
fh2020_fauls
```

    ## # A tibble: 130 x 8
    ##    equipo partido totalYellowCard fkFoulWon totalTackle fkFoulLost totalOffside
    ##    <chr>  <chr>             <dbl>     <dbl>       <dbl>      <dbl>        <dbl>
    ##  1 Audax~ Santia~               3         9           3          6            0
    ##  2 Unive~ Uni<f3~               2        10           7         11            0
    ##  3 Depor~ Uni<f3~               2         5           6         12            1
    ##  4 Evert~ Univer~               2         6          12          9            3
    ##  5 Unive~ Santia~               2         6           9          6            2
    ##  6 Cobre~ La Ser~               2         6           8         10            1
    ##  7 Depor~ Deport~               2         7           4          4            1
    ##  8 Cobre~ Cobres~               2         7           8         10            0
    ##  9 Uni<f~ Uni<f3~               2         5           5          6            2
    ## 10 Huach~ Uni<f3~               2         5           6         10            1
    ## # ... with 120 more rows, and 1 more variable: totalRedCard <dbl>

``` r
## Filtrar Datos

everton <- filter(primer_tiempo2020, equipo == "Everton")
everton_rendimiento <- filter(fh2020_rendimiento, equipo == "Everton")
everton_fauls <- filter(fh2020_fauls, equipo == "Everton")


## Agregar Promedio/Suma Total/Min/...

everton_rendimiento <- everton_rendimiento[,!(colnames(everton_rendimiento) %in% c("equipo"))] 
Promedios_rend <- c("Promedio rendimiento",mean(everton_rendimiento$saves),mean(everton_rendimiento$possessionPercentage),mean(everton_rendimiento$precision_pases))
```

    ## Warning: Unknown or uninitialised column: `precision_pases`.

    ## Warning in mean.default(everton_rendimiento$precision_pases): argument is not
    ## numeric or logical: returning NA

``` r
everton_rendimiento <- rbind(everton_rendimiento, Promedios_rend)
Max_rend <- c("Max rendimiento",max(everton_rendimiento$saves),max(everton_rendimiento$possessionPercentage),max(everton_rendimiento$precision_pases))
```

    ## Warning: Unknown or uninitialised column: `precision_pases`.

    ## Warning in max(everton_rendimiento$precision_pases): ningun argumento finito
    ## para max; retornando -Inf

``` r
everton_rendimiento <- rbind(everton_rendimiento, Max_rend)
Min_rend <- c("Min rendimiento",min(everton_rendimiento$saves),min(everton_rendimiento$possessionPercentage),min(everton_rendimiento$precision_pases))
```

    ## Warning: Unknown or uninitialised column: `precision_pases`.

    ## Warning in min(everton_rendimiento$precision_pases): ningún argumento finito
    ## para min; retornando Inf

``` r
everton_rendimiento <- rbind(everton_rendimiento, Min_rend)
everton_rendimiento
```

    ## # A tibble: 11 x 3
    ##    partido                              saves possessionPercentage
    ##    <chr>                                <chr> <chr>               
    ##  1 Everton vs Universidad Concepci<f3>n 0     58.2                
    ##  2 Everton vs La Serena                 0     52.4                
    ##  3 Everton vs Coquimbo Unido            1     51.4                
    ##  4 Cobresal vs Everton                  1     49.8                
    ##  5 Deportes Iquique vs Everton          0     46.9                
    ##  6 Universidad de Chile vs Everton      3     45.7                
    ##  7 Everton vs Uni<f3>n La Calera        1     38.9                
    ##  8 Uni<f3>n Espa<f1>ola vs Everton      2     36.7                
    ##  9 Promedio rendimiento                 1     47.5                
    ## 10 Max rendimiento                      3     58.2                
    ## 11 Min rendimiento                      0     36.7

``` r
## Graficos

rendimiento_everton <- everton$saves
everton2 <- everton[order(everton$saves, decreasing = FALSE),]
dotchart(everton$goals, labels = everton$partido, cex=0.5, xlab = "goles", ylab = "Partido")
```

![](actividad1_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
dotchart(everton$totalPass, labels = utf8_encode(everton$partido), cex=0.5, xlab = "pases", ylab = "Partido")
```

![](actividad1_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->

``` r
dotchart(everton$accuratePass, labels = utf8_encode(everton$partido), cex=0.5, xlab = "rendimiento", ylab = "Partido")
```

![](actividad1_files/figure-gfm/unnamed-chunk-1-3.png)<!-- -->

``` r
dotchart(everton2$totalPass, labels = utf8_encode(everton$partido), cex=0.5, xlab = "rendimiento", ylab = "Partido")
```

![](actividad1_files/figure-gfm/unnamed-chunk-1-4.png)<!-- -->

``` r
dotchart(everton2$totalPass, labels = utf8_encode(everton$partido), main="rendimiento Acertados everton", pch = 16, col=c("darkblue","dodgerblue"),lcolor="gray90", cex=0.8, xlab = "rendimiento", ylab = "Partido", cex.main=2,cex.lab=1.5)
```

![](actividad1_files/figure-gfm/unnamed-chunk-1-5.png)<!-- -->

``` r
## Analisis de Texto

texto <- primer_tiempo2020$partido
texto <- char_tolower(texto)
texto <- iconv(texto, to = "ASCII//TRANSLIT")
a <- dfm(texto, remove = c(stopwords("es"), "vs", "Universidad"))
```

    ## Warning: 'dfm.character()' is deprecated. Use 'tokens()' first.

    ## Warning: 'remove' is deprecated; use dfm_remove() instead

``` r
dim(a)
```

    ## [1] 130  31
