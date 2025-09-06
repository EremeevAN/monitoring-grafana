### Домашнее задание к занятию 14 «Средство визуализации Grafana»
### Задание 1
Используя директорию help внутри этого домашнего задания, запустите связку prometheus-grafana.
Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
Подключите поднятый вами prometheus, как источник данных.
Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.
![image](https://github.com/EremeevAN/monitoring-grafana/blob/main/1.png)
### Задание 2
Изучите самостоятельно ресурсы:

PromQL tutorial for beginners and humans.
Understanding Machine CPU usage.
Introduction to PromQL, the Prometheus query language.
Создайте Dashboard и в ней создайте Panels:

утилизация CPU для nodeexporter (в процентах, 100-idle);
```
-(sum by(instance) (irate(node_cpu_seconds_total{instance="$node",job="$job", mode!="idle"}[$__rate_interval])) / on(instance) group_left sum by (instance)((irate(node_cpu_seconds_total{instance="$node",job="$job"}[$__rate_interval])))) * 100
```
CPULA 1/5/15;
```
-node_load1{job="$job",instance="$node"}
```
```
-node_load5{job="$job",instance="$node"}
```
```
-node_load15{job="$job",instance="$node"}
```

количество свободной оперативной памяти;
```
-100 - ((avg_over_time(node_memory_MemAvailable_bytes{instance="$node",job="$job"}[$__rate_interval]) * 100) / avg_over_time(node_memory_MemTotal_bytes{instance="$node",job="$job"}[$__rate_interval]))
```

количество места на файловой системе.
```
-100 - ((avg_over_time(node_filesystem_avail_bytes{instance="$node",job="$job",mountpoint="/",fstype!="rootfs"}[$__rate_interval]) * 100) / avg_over_time(node_filesystem_size_bytes{instance="$node",job="$job",mountpoint="/",fstype!="rootfs"}[$__rate_interval]))
```

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.
![image](https://github.com/EremeevAN/monitoring-grafana/blob/main/2.png)
### Задание 3
Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
В качестве решения задания приведите скриншот вашей итоговой Dashboard.
![image](https://github.com/EremeevAN/monitoring-grafana/blob/main/3.png)
### Задание 4
Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
В качестве решения задания приведите листинг этого файла.
Файл по ссылке:https://github.com/EremeevAN/monitoring-grafana/blob/main/dashboard.json
