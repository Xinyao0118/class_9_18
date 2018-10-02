*problem 1*
===========

code chunk 1
------------

Generate a data\_frame included:

10 uniform random variables with values b/w 0 and 5

A logical vector indicating whether elements of random\_sample are
greater than 2

A (length-10) character vector

A (length-10) factor vector

    library(tidyverse)

    ## -- Attaching packages ------------------------------------------ tidyverse 1.2.1 --

    ## √ ggplot2 3.0.0     √ purrr   0.2.5
    ## √ tibble  1.4.2     √ dplyr   0.7.6
    ## √ tidyr   0.8.1     √ stringr 1.3.1
    ## √ readr   1.1.1     √ forcats 0.3.0

    ## -- Conflicts --------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    dt_frame = tibble(
      random_sample = runif(10, min = 0, max = 5) ,
      logical_vector = random_sample > 2 ,
      ch_vector = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j") ,
      factor_vector = as.factor(ch_vector) 
    )
    dt_frame = as.data.frame(dt_frame)

    # view top lines of dt_frame
    head(dt_frame)

    ##   random_sample logical_vector ch_vector factor_vector
    ## 1     1.7034971          FALSE         a             a
    ## 2     1.1388743          FALSE         b             b
    ## 3     4.3336312           TRUE         c             c
    ## 4     2.9903991           TRUE         d             d
    ## 5     0.6116763          FALSE         e             e
    ## 6     2.9260278           TRUE         f             f

The mean of each variable in the dataframe
------------------------------------------

The mean of **random sample** is 2.313171

The mean of the **logical vector** is 0.5

The mean of the **character vector** is NA

The mean of the **list of factor vector** is NA

**Explanation:**When applying the function of mean(),the random sample
and logical vector worked while character vector and factor vector
didn\`t work. That is because according to the useage of mean(), the
elements of the vector should be umeric/logical vectors and date,
date-time and time interval objects.

code chunk 2
------------

    #change character to numeric
    chr_to_num = as.numeric(dt_frame$ch_vector) 
    #change character to factor
    chr_to_factor = as.factor(dt_frame$ch_vector) 
    #change factor to character
    factor_to_chr = as.character(dt_frame$factor_vector) 
    #change factor to numeric
    factor_to_num = as.numeric(dt_frame$factor_vector) 
    #change logical to numeric
    logic_to_num = as.numeric(dt_frame$logical_vector) 

**Explanation**The warning (not shown above) means the variables cannot
be converted from character to numberic. Except that, some other kinds
of conversions(exp:factor to numberic to character,logic to numberic,
character to factor ) can be realized successfully.

*problem 2 *
============

code chunk 3
------------

Create a data\_frame included:

Respectivgely generate x,y: a random sample of size 1000 from a standard
Normal distribution.

A logical vector indicating whether the x + y &gt; 0.

A numeric vector created by coercing the above logical vector.

A factor vector created by coercing the above logical vector.

    dt_frame2 = tibble(
      x = rnorm(1000, mean = 0, sd = 1) , 
      y = rnorm(1000, mean = 0, sd = 1) ,
      vc_logic = x + y > 0 ,
      vc_num = as.numeric(vc_logic) ,
      vc_factor = as.factor(vc_logic)
    )
    dt_frame2 = as.data.frame(dt_frame2)

    head(dt_frame2)

    ##             x          y vc_logic vc_num vc_factor
    ## 1 -0.47113244 -1.7191365    FALSE      0     FALSE
    ## 2  0.30755895  0.1725474     TRUE      1      TRUE
    ## 3 -0.89489934  1.2801411     TRUE      1      TRUE
    ## 4 -0.07778677  1.1154900     TRUE      1      TRUE
    ## 5  0.67897180  0.5245112     TRUE      1      TRUE
    ## 6  0.87966561  0.7441072     TRUE      1      TRUE

The size of the dataset is 1000 rows\* 5 columns .

The mean of x is 0.0281674 and the median of x is 0.02294 .

The proportion of cases for which the logical vector is TRUE is 0.502.

scatterplot
-----------

    #Create scarrerplot of y vs x and the point colored by logical variable
    ggplot(dt_frame2, mapping = aes(x, y))+
      geom_point(data = dt_frame2, aes(x, y), 
                 col = ifelse(dt_frame2$vc_logic, "red", "blue"), 
                 size =1 ) +
      labs(title = "scatterplot of y vs x ")

![](calm_down_files/figure-markdown_strict/unnamed-chunk-1-1.png)

    ggsave("scatterplot_of_x_vs_y_colored_logic.pdf")

    ## Saving 7 x 5 in image

    #Create scarrerplot of y vs x and the point colored by numberic variable
    ggplot(dt_frame2, mapping = aes(x, y))+
      geom_point(data = dt_frame2, aes(x, y), 
                 col = ifelse(dt_frame2$vc_num, "blue", "green"), 
                 size =1 ) +
      labs(title = "scatterplot of y vs x ")

![](calm_down_files/figure-markdown_strict/unnamed-chunk-1-2.png)

    #Create scarrerplot of y vs x and the point colored by factor variable
    ggplot(dt_frame2, mapping = aes(x, y))+
      geom_point(data = dt_frame2, aes(x, y),
                 col = ifelse(dt_frame2$vc_factor == "TRUE", "purple", "violet"), 
                 size =1 ) +
      labs(title = "scatterplot of y vs x ")

![](calm_down_files/figure-markdown_strict/unnamed-chunk-1-3.png)
