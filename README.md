# Postgresql > csv files > filebeat > logstash
Setup your Postgresql to write csv files
`log_destination = 'csvlog'`

Download [filebeat](https://www.elastic.co/downloads/beats/filebeat) (download, unzip)

Run filebeat with config from project folder
filebeat/filebeat -e -c filebeat.yml


# Logstash > Elastic > Kibana > User
Start apps
`docker-compose up`

Check elastic cluster health
`curl http://elastic:changeme@127.0.0.1:9200/_cat/health`

Access [kibana](http://localhost:5601) web interface(wait up to 1min for first run)
credentials: elastic:changeme

How to stop containers?
`docker-compose down`

# PS
Index is: logstash-*

调试

/usr/share/logstash/bin/logstash -f conf.d/postgresql.conf  --verbose --debug

遇到的问题

multiline.pattern 配置 。
默认的module 模版在测试的时候发现有些case不支持

logstash 的filter
add_field => {"duration" => "%{[message][0]}"}

需要中括号把 message 也阔起来 新版本新语法
