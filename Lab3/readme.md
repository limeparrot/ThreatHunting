====================
Сысоев Г.А.

Лабораторная работа №3


## Цель

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Исходные данные

1.  ОС Windows 10
2.  RStudio Desktop
3.  Интерпретатор языка R 4.3.2
4.  dplyr
5.  nycflights13

## План

1.  Установить пакет ‘dplyr’
2.  Установить пакет ‘nycflights13’
3.  Выполнить задания

## Шаги

### Установка dplyr

Пакет dplyr можно установить в RStudio Desktop с помощью команды
install.packages(“dplyr”). Далее подключим пакет к текущему проекте с
помощью library(dplyr)

``` {r}
library(dplyr)
```
Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union


### Установка nycflights13

Пакет dplyr можно установить в RStudio Desktop с помощью команды
install.packages(“nycflights13”). Далее подключим пакет к текущему
проекте с помощью library(nycflights13)

``` {r}
library(nycflights13)
```

### Выполнение заданий

### 1. Сколько встроенных в пакет nycflights13 датафреймов?

В пакет nycflights13 встроено 5 датафреймов: 
airlines, airports, flights, planes, weather

### 2. Сколько строк в каждом датафрейме?

``` {r}
airlines %>% nrow()
```
[1] 16


``` {r}
airports %>% nrow()
```
[1] 1458


``` {r}
flights %>% nrow()
```
[1] 336776


``` {r}
planes %>% nrow()
```
[1] 3322


``` {r}
weather %>% nrow()
```
[1] 26115

### 3. Сколько столбцов в каждом датафрейме?

``` {r}
airlines %>% ncol()
```
[1] 2


``` {r}
airports %>% ncol()
```
[1] 8


``` {r}
flights %>% ncol()
```
[1] 19


``` {r}
planes %>% ncol()
```
[1] 9


``` {r}
weather %>% ncol()
```
[1] 15


### 4. Как посмотреть примерный вид датафрейма?

``` {r}
planes %>% glimpse()
```
Rows: 3,322
Columns: 9
$ tailnum      <chr> "N10156", "N102UW", "N103US", "N104UW", "N10575", "N105UW", "N107US", "N108UW", "N109UW", "N110UW", "N11106", "N11107", "N11109", "N1111…
$ year         <int> 2004, 1998, 1999, 1999, 2002, 1999, 1999, 1999, 1999, 1999, 2002, 2002, 2002, 2002, 2002, 2003, 2003, 2003, 2003, 2003, 2004, 2004, 2004…
$ type         <chr> "Fixed wing multi engine", "Fixed wing multi engine", "Fixed wing multi engine", "Fixed wing multi engine", "Fixed wing multi engine", "…
$ manufacturer <chr> "EMBRAER", "AIRBUS INDUSTRIE", "AIRBUS INDUSTRIE", "AIRBUS INDUSTRIE", "EMBRAER", "AIRBUS INDUSTRIE", "AIRBUS INDUSTRIE", "AIRBUS INDUST…
$ model        <chr> "EMB-145XR", "A320-214", "A320-214", "A320-214", "EMB-145LR", "A320-214", "A320-214", "A320-214", "A320-214", "A320-214", "EMB-145XR", "…
$ engines      <int> 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
$ seats        <int> 55, 182, 182, 182, 55, 182, 182, 182, 182, 182, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, 55, …
$ speed        <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
$ engine       <chr> "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo…


### 5. Сколько компаний-перевозчиков(carrier) представлено в этих наборах данных?

``` {r}
unique(airlines) %>% nrow()
```
[1] 16


### 6. Сколько рейсов принял аэропорт John F Kennedy intl в мае?

``` {r}
flights %>% filter(dest == "JFK" & month == 5) %>% nrow()
```

[1] 0


### 7. Какой самый северный аэропорт?

``` {r}
airports %>% filter(lat == max(lat))
```

# A tibble: 1 × 8
      faa   name                      lat   lon   alt    tz dst   tzone
      <chr> <chr>                   <dbl> <dbl> <dbl> <dbl> <chr> <chr>
    1 EEN   Dillant Hopkins Airport  72.3  42.9   149    -5 A     <NA> 


### 8. Какой аэропорт самый высокогорный(находится выше всех над уровнем моря)?

``` {r}
airports %>% filter(alt == max(alt))
```

# A tibble: 1 × 8
      faa   name        lat   lon   alt    tz dst   tzone         
      <chr> <chr>     <dbl> <dbl> <dbl> <dbl> <chr> <chr>         
    1 TEX   Telluride  38.0 -108.  9078    -7 A     America/Denver


### 9. Какие бортовые номера у самых старых самолетов?

``` {r}
planes %>% arrange(year) %>% select(tailnum) %>% head(5)
```

# A tibble: 5 × 1
       tailnum
       <chr>  
     1 N381AA 
     2 N201AA 
     3 N567AA 
     4 N378AA 
     5 N575AA 


### 10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy intl(в грудусах Цельсия)?

``` {r}
tmpWet <- weather %>% filter(origin == "JFK" & month == 9) %>% summarise(tmpWet = mean(temp))
(tmpWet - 32) * 5 / 9
```

tmpWet
1 19.38764


### 11. Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` {r}
flights %>% filter(month == 6) %>% group_by(carrier) %>% summarize(amount = n()) %>% arrange(desc(amount)) %>% head(1)
```

# A tibble: 1 × 2
  carrier amount
  <chr>    <int>
1 UA        4975


### 12. Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` {r}
flights %>% filter(arr_delay > 0 & year == 2013) %>% group_by(carrier) %>% summarise(delays = n()) %>% arrange(desc(delays)) %>% head(1)
```

# A tibble: 1 × 2
  carrier delays
  <chr>    <int>
1 EV       24484


## Оценка результата

С помощью функций пакета dplyr проанализировали данные датафрейма nycflights13

## Вывод

Повысили свои навыки работы с функциями пакета dplyr на датафреймах пакета nycflights13
