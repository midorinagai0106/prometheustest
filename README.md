# prometheustest

## 概要
- prometheus / grafana / nodeexporter/ alertmanagerのセットアップ
- ※alertmanagerの発火方法は以下を参照
http://localhost:9093/#/alerts

### 起動コマンド
docker-compose -f docker-compose.yml up

### 詰まったところメモ
- prometheus.ymlの書き方
 - 以下の書き方だと、prometheus→node-exporterの参照ができない。
```
   - job_name: 'prometheus'
     static_configs:
       - targets:
         - localhost:9090
   - job_name: 'node'
     static_configs:
       - targets:
         - localhost:9100
```

- 参考 https://qiita.com/samskeyti/items/fbe8b78e47a5e4d6842a
- こんな感じでサービス名:ポート名として指定する
```
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets:
        -  prometheus:9090
        -  node-exporter:9100
```

### 参考文献
- compose周りとか
https://qiita.com/ryojsb/items/419b45ceac014e91a64b
- 詰まったところとか、alertmanager周りとか
https://qiita.com/samskeyti/items/fbe8b78e47a5e4d6842a
- slack api
https://qiita.com/rubytomato@github/items/6558bfdb37d982891c09

### 備忘
- volumeの読み方
/Users/nagaimidori/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
ホストの絶対パス：dockerのマウント先:roをつけるとreadonlyになる
- grafana
http://localhost:3000/?orgId=1
- alertmanager
http://localhost:9093/#/alerts
