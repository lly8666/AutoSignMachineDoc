# AutoSignMachineDoc

## 目前可使用的脚本

|    脚本名     |   说明   | 状态 |
| :-----------: | :------: | ---- |
|     iqiyi     |          |      |
|   bilibili    |          |      |
|    52pojie    |          |      |
|   hecaiyun    |  和彩云  |      |
|    unicom     |          |      |
|    youthkd    | 中青看点 |      |
| jiandantianqi | 简单天气 |      |
|     shuqi     |   书旗   |      |
|  cashtoutiao  |  惠头条  |      |
|   jingdong    |   京东   |      |
|   yuedongzu   |  悦动族  |      |

## 配置格式参考

详细查看`example/config`目录下内容

```json
{
  "accountSn": "1",
  "session-1": "xxxxxxxxxxxxxx",
  "user-1": "xxxxxxxxxxxxxx",
  "name-1": "xxxxxxxxxxxxxx"
}
```

## 计划任务使用案例

详细查看`example/cron.txt`内容

```text
*/30 7-22 * * * node /workspace/AutoSignMachine/index.js jingdong --config /root/.AutoSignMachine/config/jingdong.json
*/30 7-22 * * * node /workspace/AutoSignMachine/index.js iqiyi --config /root/.AutoSignMachine/config/iqiyi.json
```

## Docker 使用参考

```sh
# 构建
docker build -t lunnlew/auto-sign-machine:latest  -f docker/Dockerfile .
# 运行
docker run \
  --name auto-sign-machine \
  -d \
  -p 3003:3003 \
  -v /root/.AutoSignMachine:/root/.AutoSignMachine \
  -e enable_jingdong=true \
  -e enable_webui=true \
  lunnlew/auto-sign-machine:latest
# 停止
docker stop auto-sign-machine
# 删除
docker rm auto-sign-machine
# 强制删除
docker rm -f auto-sign-machine
# 日志
docker logs -f auto-sign-machine
```

其中暴露出的 3003 端口可用于访问 webUI

默认数据目录为`/root/.AutoSignMachine`,可以使用环境变量`-e SAVE_DATA_DIR=/root/.AutoSignMachine`来重新指定

默认配置文件名称结构为`[command].json`,例如`jingdong.json` ,可以使用环境变量`-e config_[command]=jingdong.json`来重新指定

## 任务环境变量文件.env

文件.env 可创建并放在代码根目录，与 src、example 等同级

可使用的环境变量可查看`.env.default`内容

```text
  notify_pushplus_token=xxxxxxxxxxxxxx
  notify_sckey=xxxxxxxxxxxxxx
  notify_wechat_corpid=xxxxxxxxxxxxxx
  notify_wechat_corpsecret=xxxxxxxxxxxxxx
  notify_wechat_agentld=xxxxxxxxxxxxxx
  notify_tele_bottoken=xxxxxxxxxxxxxx
  notify_tele_chatid=xxxxxxxxxxxxxx
  notify_tele_url=xxxxxxxxxxxxxx
  ban_jingdong_tasks=xxxxxx,xxxxxx,xxxxxx
```
