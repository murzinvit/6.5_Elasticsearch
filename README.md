### 6.5_Elasticsearch </br>
------------------------------------------------ </br>
#### Задача 1:
1) Докерфайл для запуска контейнера с elastic [Dockerfile](https://github.com/murzinvit/6.5_Elasticsearch/blob/b410ec0390e8e348526bbc4508b1f5363346152b/Dockerfile) </br>
2) Команда для запуска: `docker run -d --name elasic -p 9200:9200 -p 9300:9300 murzinvit/elasticsearch:latest` </br>
3) Образ на hub.docker.com [https://hub.docker.com/repository/docker/murzinvit/elasticsearch](https://hub.docker.com/repository/docker/murzinvit/elasticsearch) </br>
4) Недостаток памяти исправил командой(выполнять на хосте) - `echo "vm.max_map_count=262144" >> /etc/sysctl.conf && sysctl -p` </br>

### Ответ на curl localhost:9200 </br>
![screen](https://github.com/murzinvit/screen/blob/7a1e0db8094655db237f06c9a3534b3478571282/Elastic_screen_curl_9200.png)

#### Задача 2: </br>
Документация по запросам к Elasticsearch: [www.elastic.co/guide/en/elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices.html) </br>
Запросы к Elastic можно отправлять через curl в cmd, или по http через браузер </br>
Создать индекс можно запросом: [elastic_put](https://github.com/murzinvit/6.5_Elasticsearch/blob/3f12afa445fb49343759627298eb581b4ff94725/elastic_put) </br>
Получить список индексов и статусов можно запросом: `curl -X GET "localhost:9200/_cat/indices?v"` </br>
Получить состояние кластера: `curl -X GET "localhost:9200/_cluster/health"` </br>
Часть индексов и сам кластер находятся в состоянии yellow т.к single-node и данные не реплицированы </br>
Удаление всех индексов: `curl -X DELETE "localhost:9200/_all"` </br>

#### Задача 3: </br>
1) Папка для snashots: `mkdir -p /etc/elasticsearch/snapshots/netology_backup` </br>
2) Регистрация папки netology_backup: [запрос](https://github.com/murzinvit/6.5_Elasticsearch/blob/87c5e71858c17d87d7343685b15f4833add266bc/elastic_snapshots) </br>
3) Результат выполнения запроса: </br>
![Snap_screen](https://github.com/murzinvit/screen/blob/0d3534ee0afc442367b1ed4f8ff54c2478dcde23/Elastic_snapshots_results.jpg)
4) Создайте индекс test с 0 реплик и 1 шардом и приведите в ответе список индексов: </br>
![screen](https://github.com/murzinvit/screen/blob/5c84630298e02c789366f9772e1fdd4f478119f2/Elastic_put_test.jpg)
5) Создайте snapshot состояния кластера elasticsearch: [запрос](https://github.com/murzinvit/6.5_Elasticsearch/blob/ec207d896d0a625b35da3d0e02c0bc624adcc5e3/make_snapshop)</br>
![screen](https://github.com/murzinvit/screen/blob/161c417274556aa4e180864c5b390745d62cade4/Elastic_ls_forlder_result.jpg)
6) Удалите индекс test и создайте индекс test-2. Приведите в ответе список индексов: </br>
![screen](https://github.com/murzinvit/screen/blob/9b1b28a0c889df53b8cb9a621bcc9b658e3cd6d4/Elastic_test2_result.jpg)
7) Восстановите состояние кластера elasticsearch из snapshot, созданного ранее: </br>
   Запрос для восстановления индекса: [Index_restore](https://github.com/murzinvit/6.5_Elasticsearch/blob/35f05976ea063392f05154a86b2cdd26177c870d/Index_restore) </br>
   ![screen](https://github.com/murzinvit/screen/blob/88784c117128bdbf1e026db48b7dde461a25bb9f/Elastic_restore_result.jpg)




