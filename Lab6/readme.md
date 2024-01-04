# Лабораторная работа №6

Сысоев Г.А.

## Цель работы

1.  Закрепить навыки исследования данных журнала Windows Active
    Directory

2.  Изучить структуру журнала системы Windows Active Directory

3.  Зекрепить практические навыки использования языка программирования R
    для обработки данных

4.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R

## Ход работы

```{r}
library(dplyr)
library(xml2)
library(rvest)
library(jsonlite)
library(tidyr)
```

## Подготовка данных

## Задание 1

### Импортируйте данные в R

```{r}
json_dataframe <- jsonlite::stream_in(file('./caldera_attack_evals_round1_day1_2019-10-20201108.json'))
library('xml2')
library('rvest')
library('dplyr')
weburl <- "https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor"
webreq <- xml2::read_html(weburl)
events_dataframe <- rvest::html_table(webreq)[[1]]
	
## Задание 2

### Привести датасеты в вид "аккуратных данных", преобразовать типы столбцов в соответствии с типом данных

```{r}
json_dataframe$'@timestamp' <- as.POSIXct(json_dataframe$'@timestamp', format = "%Y-%m-%dT%H:%M:%OSZ", tz = "UTC")
json_dataframe <- json_dataframe %>% rename(timestamp = `@timestamp`, metadata = `@metadata`)
```

## Задание 3

### Просмотрите общую структуру данных с помощью функции glimpse()

```{r}
glimpse(events_dataframe)
glimpse(json_dataframe)
```
Rows: 381
Columns: 4
$ `Current Windows Event ID` <chr> "4618", "4649", "4719", "4765", "4766", "4794", "4897", "4964", "5124", "N/A", "1102", "4621", "4675", "4692", "4693", "47…
$ `Legacy Windows Event ID`  <chr> "N/A", "N/A", "612", "N/A", "N/A", "N/A", "801", "N/A", "N/A", "550", "517", "N/A", "N/A", "N/A", "N/A", "610", "617", "61…
$ `Potential Criticality`    <chr> "High", "High", "High", "High", "High", "High", "High", "High", "High", "Medium to High", "Medium to High", "Medium", "Med…
$ `Event Summary`            <chr> "A monitored security event pattern has occurred.", "A replay attack was detected. May be a harmless false positive due to…
	
## Анализ

## Задание 1

### Раскройте датафрейм избавившись от вложенных датафреймов.

```{r}
json_dataframe <- json_dataframe %>% tidyr::unnest(c(metadata, event, log, winlog, ecs, host, agent), names_sep = ".")
json_dataframe %>% (glimpse)
```

# A tibble: 101,904 × 34
   timestamp           metadata.beat metadata.type metadata.version metadata.topic event.created           event.kind event.code event.action log.level message
   <dttm>              <chr>         <chr>         <chr>            <chr>          <chr>                   <chr>           <int> <chr>        <chr>     <chr>  
 1 2019-10-20 20:11:06 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:09.98… event            4703 Token Right… informat… "A tok…
 2 2019-10-20 20:11:07 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:09.98… event            4673 Sensitive P… informat… "A pri…
 3 2019-10-20 20:11:09 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:11.99… event              10 Process acc… informat… "Proce…
 4 2019-10-20 20:11:10 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:14.01… event              10 Process acc… informat… "Proce…
 5 2019-10-20 20:11:11 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:14.01… event              10 Process acc… informat… "Proce…
 6 2019-10-20 20:11:15 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:18.02… event              10 Process acc… informat… "Proce…
 7 2019-10-20 20:11:15 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:18.02… event              11 File create… informat… "File …
 8 2019-10-20 20:11:15 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:18.02… event              10 Process acc… informat… "Proce…
 9 2019-10-20 20:11:15 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:18.02… event              10 Process acc… informat… "Proce…
10 2019-10-20 20:11:16 winlogbeat    _doc          7.4.0            winlogbeat     2019-10-20T20:11:18.02… event              10 Process acc… informat… "Proce…

	
## Задание 2

### Минимизируйте количество колонок в датафрейме -- уберите колоки с единственным значением параметра.

```{r}
optimiz_dataframe <- subset(json_dataframe, select = - c(metadata.beat, metadata.type,metadata.version,metadata.topic,event.kind,winlog.api,agent.ephemeral_id,agent.hostname,agent.id,agent.version,agent.type))
optimiz_dataframe %>% glimpse()
```
    Rows: 101,904
    Columns: 23
    $ timestamp            <dttm> 2019-10-20 20:11:06, 2019-10-20 20:11:07, 2019-1…
    $ event.created        <chr> "2019-10-20T20:11:09.988Z", "2019-10-20T20:11:09.…
    $ event.code           <int> 4703, 4673, 10, 10, 10, 10, 11, 10, 10, 10, 10, 7…
    $ event.action         <chr> "Token Right Adjusted Events", "Sensitive Privile…
    $ log.level            <chr> "information", "information", "information", "inf…
    $ message              <chr> "A token right was adjusted.\n\nSubject:\n\tSecur…
    $ winlog.event_data    <df[,234]> <data.frame[26 x 234]>
    $ winlog.event_id      <int> 4703, 4673, 10, 10, 10, 10, 11, 10, 10, 10, …
    $ winlog.provider_name <chr> "Microsoft-Windows-Security-Auditing", "Microsoft…
    $ winlog.record_id     <int> 50588, 104875, 226649, 153525, 163488, 153526, 13…
    $ winlog.computer_name <chr> "HR001.shire.com", "HFDC01.shire.com", "IT001.shi…
    $ winlog.process       <df[,2]> <data.frame[26 x 2]>
    $ winlog.keywords      <list> "Audit Success", "Audit Failure", <NULL>, <NULL>,…
    $ winlog.provider_guid <chr> "{54849625-5478-4994-a5ba-3e3b0328c30d}", "{54…
    $ winlog.channel       <chr> "security", "Security", "Microsoft-Windows-Sysmo…
    $ winlog.task          <chr> "Token Right Adjusted Events", "Sensitive Privile…
    $ winlog.opcode        <chr> "Info", "Info", "Info", "Info", "Info", "Info", "…
    $ winlog.version       <int> NA, NA, 3, 3, 3, 3, 2, 3, 3, 3, 3, 3, 3, 3, NA, 3…
    $ winlog.user          <df[,4]> <data.frame[26 x 4]>
    $ winlog.activity_id   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ winlog.user_data     <df[,30]> <data.frame[26 x 30]>
    $ ecs.version          <chr> "1.1.0", "1.1.0", "1.1.0", "1.1.0", "1.1.0", "1.1…
    $ host.name            <chr> "WECServer", "WECServer", "WECServer", "WECSer…
	
## Задание 3

### Какое количество хостов представлено в данном датасете?

```{r}
optimiz_dataframe %>% select(host.name) %>% unique()
```
    # A tibble: 1 × 1
      host.name
      <chr>    
    1 WECServer
	
Ответ: 1 - Windows Event Collector - сборщик логов.

## Задание 4

### Подготовьте датафрейм с расшифровкой Windows Event_ID, приведите типы данных к типу их значений.

```{r}
events_dataframe <- events_dataframe %>% rename(Current_Windows_Event_ID = `Current Windows Event ID`, Legacy_Windows_Event_ID = `Legacy Windows Event ID`, Potential_Criticality = `Potential Criticality`, Event_Summary = `Event Summary`)

events_dataframe$Current_Windows_Event_ID <- as.integer(events_dataframe$Current_Windows_Event_ID)
events_dataframe$Legacy_Windows_Event_ID <- as.integer(events_dataframe$Legacy_Windows_Event_ID)

events_dataframe %>% glimpse()
```
    Rows: 381
    Columns: 4
    $ Current_Windows_Event_ID <int> 4618, 4649, 4719, 4765, 4766, 4794, 4897, 496…
    $ Legacy_Windows_Event_ID  <int> NA, NA, 612, NA, NA, NA, 801, NA, NA, 550, 51…
    $ Potential_Criticality    <chr> "High", "High", "High", "High", "High", "High…
    $ Event_Summary            <chr> "A monitored security event pattern has occur…
	
## Задание 5

### Есть ли в логе события с высоким и средним уровнем значимости? Сколько их?

```{r}
events_dataframe %>% select(Potential_Criticality) %>% filter(Potential_Criticality == 'High' | Potential_Criticality == 'Medium') %>% group_by(Potential_Criticality) %>% count()
```
    # A tibble: 2 × 2
    # Groups:   Potential_Criticality [2]
      Potential_Criticality     n
      <chr>                 <int>
    1 High                      9
    2 Medium                   79

Ответ: Да, есть, Высокий - 9, Средний - 79.

## Вывод

### Получили знания о методах исследования данных журнала событий Windows Active Directory с помощью языка R