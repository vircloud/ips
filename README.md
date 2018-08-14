# Nginx 屏蔽垃圾蜘蛛、攻擊、惡意來源 IP 精準版

服務器資源有限，受不了垃圾蜘蛛一天到晚的爬取，爬取也就算了，還拿去當做自己盈利點，果斷屏蔽！

本配置文件適合 nginx，apache 可以自己對照著修改，IP 不斷更新中，大家可以根據自己的需要添加或刪除，由於有些來源 IP 純屬肉雞，因此僅供參考。

本文件區別於嚴格版，**精準至具體 IP **。

用法：

① 下載配置文件，放到適當的位置，比如：

cd /usr/local/nginx/conf/vhost/ && wget https://raw.githubusercontent.com/vircloud/ips/accurate/deny-ips.conf

② 修改站點配置文件，在適當的位置引入配置，比如：

server

{

......

include deny-ips.conf;

......

}

③ 重啟 nginx 服務：

service nginx reload


問：IP 是如何確定的？

答：查詢 Nginx 訪問日誌，發現有異常訪問，如下：

```
13.56.229.65 - - [26/Jan/2018:22:32:42 +0800] "GET / HTTP/1.1" 200 2563 "/upload/_dispatch.php" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36"
```

顯然這是一個嘗試破解網站的流量，再到 https://www.ipip.net/ip.html 查詢：

```
AS16509	13.56.0.0/16	AMAZON-02 - Amazon.com, Inc., US
美国加利福尼亚州旧金山 amazon.com
威胁情报：机器人, 撞库, 僵尸网络, 网络攻击 。
```

由此，將 13.56.0.0/16 IP 段納入屏蔽範圍。
