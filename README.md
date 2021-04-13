# qxx: 我的理解: 
工作原理: 把./nginx/log映射到了nginx里, 同时映射到了filebeat里, 所以filebeat你能监控的日志的文件的变化; 

## 程序的理解
- App: 后端程序, 基于nodejs、express
- Nginx: 转发请求到app
- Elasticsearch: 存储; 
- Filebeat: 收集nginx的日志到logstash
- Logstash: 解析收到的filebeat的日志, 存到es
- Kibana: 管理、可视化es


# Elastic stack (ELK) + Filebeat for Monitoring Nginx on Docker

This is extended version from [ELK on Docker](https://github.com/deviantony/docker-elk) with Filebeat plugin. Filebeat takes in charge of streaming log file from nginx to Logstash then processing it and visualize to Kibana.

## What 's insides 

```
├── app
│   ├── package.json
│   ├── package-lock.json
│   ├── src
│   │   └── index.js
│   └── yarn.lock
├── elasticsearch
│   ├── config
│   │   └── elasticsearch.yml
│   └── Dockerfile
├── filebeat
│   ├── config
│   │   └── filebeat.yml
│   └── Dockerfile
├── kibana
│   ├── config
│   │   └── kibana.yml
│   └── Dockerfile
├── logstash
│   ├── config
│   │   └── logstash.yml
│   ├── Dockerfile
│   └── pipeline
│       └── nginx.conf
├── nginx
│   ├── config
│   │   └── site.conf
│   ├── Dockerfile
│   └── log
│       ├── access.log
│       └── error.log
├── docker-compose.yml
├── LICENSE
└── README.md
```

- App: minimal simple Express app
- Nginx: web server for app.
- Elasticsearch: containing build image and configure for Elasticsearch
- Filebeat: containing build image and configure for Filebeat to streaming log of Nginx to Logstash
- Logstash: containing build image and configure pipeline for Logstash to process sent log file from Filebeat
- Kibana: containing build image and configure for Kibana to visualize data

## Getting Started

To run this stack, run the following command
```bash
docker-compose up
```
Then go to `http://localhost:5601` to see your data in Kibana

Default Kibana user information
- Username: elastic
- Password: changeme
