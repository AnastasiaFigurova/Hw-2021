Визуализация персонажей Звездных войн
================
Mine Çetinkaya-Rundel translated by Basil Yakimov

### Взглянем на фрейм starwars.

``` r
glimpse(starwars)
```

    ## Rows: 87
    ## Columns: 14
    ## $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or~
    ## $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2~
    ## $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.~
    ## $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N~
    ## $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "~
    ## $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",~
    ## $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, ~
    ## $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",~
    ## $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini~
    ## $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T~
    ## $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma~
    ## $ films      <list> <"The Empire Strikes Back", "Revenge of the Sith", "Return~
    ## $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp~
    ## $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",~

### Модифицируйте следующий график для замены цвета всех точек на розовый (`"pink"`).

``` r
ggplot(starwars, 
       aes(x = height, y = mass, color = gender, size = birth_year)) +
  geom_point(color = "pink")
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](starwars_files/figure-gfm/scatterplot-1.png)<!-- -->

### Добавьте заголовок и подписи к осям и легенде. Раскомментируйте строчки, чтобы увидеть результат.

``` r
ggplot(starwars, 
       aes(x = height, y = mass, color = gender, size = birth_year)) +
  geom_point(color = "#30509C") +
  labs(
    title = "График зависимости веса от высоты персонажей",
    x = "Высота (см)", 
    y = "Вес (кг)",
    )
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](starwars_files/figure-gfm/scatterplot-labels-1.png)<!-- -->

### Выберите одну категориальную переменную из набора данных и постройте столбчатый график ее распределения.

(Небольшой фрагмент стартового кода представлен ниже и этот фрагмент
кода не будет исполняться (настройка `eval = FALSE`), поскольку
имеющийся код синтаксически некорректен и не может быть исполнен,
что заблокирует весь документ. Когда вы дополните этот код, замените
настройку фрагмента на `eval = TRUE` либо вообще удалите опцию
`eval`).

``` r
ggplot(starwars, aes(y = skin_color)) +
  geom_bar()
``

### Выберите одну числовую переменную из набора данных и постройте гистограмму ее распределения.

(На сей раз стартового фрагмента кода нет, работайте самостоятельно!)
```

``` r
ggplot(starwars, aes(x = mass)) + 
  geom_histogram() +
  labs(
    x = "Вес, кг",
    y = "Частота",
    title = "Гистограмма веса персонажей Starwars"
  )
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 28 rows containing non-finite values (stat_bin).

![](starwars_files/figure-gfm/histogram-1.png)<!-- -->

### Выберите числовую и категориальную переменные и создайте визуализацию (вы сами выбираете тип\!) отношения между этими переменными. Помимо вашего кода и результата, изложите интерпретацию вашей визуализации.

``` r
#ggplot(starwars, aes(x = height, fill = sex)) +
  #geom_histogram()
ggplot(starwars, aes(x = height, fill = sex)) +
  geom_density(adjust = 2, 
               alpha = 0.5) +
  labs(
    x = "Height, сm",
    y = "Count",
  )
```

    ## Warning: Removed 6 rows containing non-finite values (stat_density).

    ## Warning: Groups with fewer than two data points have been dropped.

    ## Warning in max(ids, na.rm = TRUE): у 'max' нет не пропущенных аргументов;
    ## возвращаю -Inf

![](starwars_files/figure-gfm/num-cat-1.png)<!-- --> Наибольшее
количество женщин обладает ростом приблизительно 160-170 см,
наибольшее количество мужчин обладает ростом приблизительно 180-190
см, однако переменная рост у мужчин принимает большее количество
разнообразных значений, о чем говорят хвосты графика.

### Выберите две категориальные переменные и создайте визуализацию отношения между этими переменными. Помимо вашего кода и результата, изложите интерпретацию вашей визуализации.

``` r
ggplot(starwars, aes(x = gender, 
                  fill = sex)) +
  geom_bar()
```

![](starwars_files/figure-gfm/cat-cat-1.png)<!-- --> На графике можно
заметить, что все мужчины относят себя к маскулинному гендеру, все
гермафродиты относят себя также к маскулинному гендеру, все женщины
относят себя к феминному гендеру.

### Выберите две числовые и две категориальные переменные и создайте визуализацию, которая включает все эти переменные. Изложите интерпретацию вашей визуализации.

``` r
ggplot(data = starwars, 
       mapping = aes(x = height, y = mass,
                     colour = sex,
                     shape = gender)) +
  geom_point() +
  labs(x = "Height, сm", y = "Mass, kg")
```

    ## Warning: Removed 29 rows containing missing values (geom_point).

![](starwars_files/figure-gfm/multi-1.png)<!-- --> На графике можно
заметить, что большинство мужчин весят примерно до 200 кг, имеют
рост от 160 до 200 см (однако есть значения меньше 10 кг и больше 200
кг), все мужчины относят себя к мускулинному гендеру. Рост женщин лежит
в промежутке от 150 до приблизительно 180 см, вес приблизательно до 100
кг, уклоняющихся наблюдений среди группы женщин не наблюдается, все
женщины причисляют себя к феминному гендеру. На графике встречается
одно уклоняющееся наблюдение по переменной mass - данное наблюдение
гемафродит, весом приблизительно 1600-1700 кг, рост примерно 175
см, относит себя к мускулинному гендеру.
