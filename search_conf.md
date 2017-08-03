


Splunk Search configuration 
===========================


## Search 의 종류 ##

 - adhoc 
 - scheduled 
 - data model acceleration 
 - report acceleration

----------

동시 수행 검색문의 제어
-------------
limits.conf

    [search]
    base_max_searches = 6
    max_searches_per_cpu = 1



> **max_hist_searches = CPU * max_searches_per_cpu + base_max_searches**



Realtime Search문의 제어
-------------
limits.conf

    [search]
    max_rt_search_multiplier = 1

> **max_rt_searches = max_rt_search_multiplier * max_hist_searches**

Scheduled Search의 제어
-------------
limits.conf

    [scheduler]
    max_searches_perc = 50

> **max_searches = max_searches_perc * max_hist_searches**

Data Model/Report Acceleration의 제어
-------------
limits.conf
    [scheduler]
    auto_summary_perc = 50
    
>**max_auto_summary = auto_summary_perc * max_searches**    
