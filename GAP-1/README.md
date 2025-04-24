# Prometheus - Exporters, Service Discovery"

```
Были созданы две виртуальные машины под WordPress и Prometheus на базе дистрибутивов Ubuntu 22.04.
WordPress развёрнут по официальной документации Canonical
https://ubuntu.com/tutorials/install-and-configure-wordpres
```
![WordPress](https://raw.githubusercontent.com/Blackwerzen/otus_monitoring/refs/heads/main/GAP-1/pictures/pic02.PNG)


```
Установлены  три экспортера:
* Node exporter
* Mysqld exporter
* Blackbox exporter
Конфигурации системных юнитов для автоматического запуска экспортеров находятся в каталоге configs
```

```
На второй ВМ был развёрнут Prometheus v3.3.0
Конфигурационный файл расположен в каталоге configs
Все экспортеры добавлены как таргеты для наблюдения
```
![WordPress](https://raw.githubusercontent.com/Blackwerzen/otus_monitoring/refs/heads/main/GAP-1/pictures/pic01.PNG)

# Отказоустойчивость Prometheus, хранилища метрик для Prometheus (Thanos, VictoriaMetrics, Mimir)

```
Развёрнута виртуальная машина под VictoriaMetrics на базе дистрибутива Ubuntu 22.04.
Конфигурационный файл VictoriaMetrics расположен в каталоге configs
```
Время хранения выставлено сроком на 14 дней
```
  -retentionPeriod 14d
```
Для лэйбла prod в конфигурацию Prometheus для каждого таргета добавлены:
```
  labels:
    site: prod
```
Для передачи данных в VictoriaMetrics добавлен настройка remote_write:
```
remote_write:
  - url: http://192.168.136.133:8428/api/v1/write
```
