# Nginx 屏蔽垃圾蜘蛛、攻擊、惡意來源 IP

服務器資源有限，受不了垃圾蜘蛛一天到晚的爬取，爬取也就算了，還拿去當做自己盈利點，果斷屏蔽！

本配置文件適合 nginx，apache 可以自己對照著修改，IP 不斷更新中，大家可以根據自己的需要添加或刪除，由於有些來源 IP 純屬肉雞，因此僅供參考。

本文件較嚴格，基本都是一個網段一起屏蔽，如果你是企業網站、官網之類的大型站點，請斟酌。

用法：

① 下載配置文件，放到適當的位置，比如：

cd /usr/local/nginx/conf/vhost/ && wget https://raw.githubusercontent.com/vircloud/ips/master/deny-ips.conf

② 修改站點配置文件，在適當的位置引入配置，比如：

server

{

......

include deny-ips.conf;

......

}

③ 重啟 nginx 服務：

service nginx reload

