# Перевод документации по dplyr

Данный репозиторий содержит переводы всех виньеток по пакету 
[dplyr](https://cran.r-project.org/web/packages/dplyr/):

[Data frames](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/data_frames.Rmd) 

[Databases](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/databases.Rmd)

[Hybrid evaluation](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/hybrid_evaluation.Rmd)

[Introduction to dplyr](http://rpubs.com/aa989190f363e46d/dplyr_intro) (перевод выполнен [aa989190f363e46d](http://rpubs.com/aa989190f363e46d/dplyr_intro), здесь сохранена [копия](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/dplyr_introduction.rmd))

[Adding a new SQL backend](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/SQL_backend.Rmd)

[Non-standard evaluation](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/nse.Rmd)

[Two-table verbs](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/2table_verbs.Rmd) (также был найден [перевод старой версии](http://rpubs.com/aa989190f363e46d/dplyr-two-table))

[Window functions and grouped mutate/filter](https://github.com/statist-bhfz/dplyr_doc_ru/blob/master/2table_verbs.Rmd)

Ниже представлены фрагменты кода из readme, иллюстрирующие использование полезной функции `do` (в виньетках эта тема не рассматривается):

```
by_year <- lahman_df() %>% 
  tbl("Batting") %>%
  group_by(yearID)
by_year %>% 
  do(mod = lm(R ~ AB, data = .))
#> Source: local data frame [143 x 2]
#> Groups: <by row>
#> 
#>    yearID     mod
#>     (int)   (chr)
#> 1    1871 <S3:lm>
#> 2    1872 <S3:lm>
#> 3    1873 <S3:lm>
#> 4    1874 <S3:lm>
#> 5    1875 <S3:lm>
#> 6    1876 <S3:lm>
#> 7    1877 <S3:lm>
#> 8    1878 <S3:lm>
#> 9    1879 <S3:lm>
#> 10   1880 <S3:lm>
#> ..    ...     ...
```

```
by_year %>% 
  do(mod = lm(R ~ AB, data = .)) %>%
  object.size() %>%
  print(unit = "MB")
#> 22.2 Mb

by_year %>% 
  do(mod = biglm::biglm(R ~ AB, data = .)) %>%
  object.size() %>%
  print(unit = "MB")
#> 0.8 Mb
```
