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


#docker安装kibana
docker pull docker.elastic.co/kibana/kibana:7.6.2
docker run --name kibana6.6.0 -e ELASTICSEARCH_URL=http://192.168.172.20:9200 -p 5601:5601 -d eadc7b3d59dd
#进入容器之中
docker exec -it a8bfcdadf624 /bin/bash
#在config文件夹下面修改kibana.yml，将url修改成
elasticsearch.hosts: [ "http://39.98.138.203:9200" ]
#汉化添加这句添加
i18n.locale: "zh-CN"
#重启
docker restart a8bfcdadf624

安装ik分词器
#进入ElasticSearch容器
docker exec -it fa2709031c12 /bin/bash
#进入plugins文件夹
cd plugins
#安装wget
yum wget
#下载安装ik（对应kibana和ElasticSearch版本）
wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.6.2/elasticsearch-analysis-ik-7.6.2.zip
#建立ik文件夹
mkdir ik
#移动到ik下并解压
unzip elasticsearch-analysis-ik-7.6.2.zip -d ik
rm -f elasticsearch-analysis-ik-7.6.2.zip 
#重启ElasticSearch
docker restart  (id)

安装elasticsearch-head
#拉取
docker pull mobz/elasticsearch-head:5
#启动并端口映射
docker run -d -p 9100:9100 docker.io/mobz/elasticsearch-head:5
访问9100端口绑定ElasticSearch就可以了，前提是做了跨域处理。
