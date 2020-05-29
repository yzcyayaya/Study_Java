#拉取ES镜像
docker pull  daocloud.io/library/elasticsearch:7.6.2
#运行ES
docker run -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -d -p 9200:9200 -p 9300:9300 --name ES03 41072cdeebc5
#配置ElasticSearch
docker exec -it fa2709031c12(容器id) /bin/bash
cd config
vim elasticsearch.yml
#添加以下（跨域跨端口）
http.cors.enabled: true
http.cors.allow-origin: "*"
