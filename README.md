 <h1 align="center">
  diy机器人
  <br>
  Author: chiupam
</h1>

1、新增查id全局插件，用法：选中一个消息回复id \
2、新增删除del全局插件，用法：任意地方删除自身消息发送d n,n为次数，必填\
3、新增复读re全局插件，用法:选中一个消息回复re n,n为次数，非必填\
4、新增查天气weather全局插件，用法：发送某地天气\
5、新增京粉转链全局插件,用法：选中一个商品断链发送jf，延时稍微有点大\
6、新增ccwav四大查询资产全局插件,用法：cb n,bc n,bb n,bd n，js依赖脚本到 https://github.com/ccwav/QL_DIYBOT/tree/main/Script 拉库\
7、新增WALL_E全局京东口令解析插件，用法:选中一个京东口令消息回复jx

## 目录
- [目录](#目录)
- [仓库目录说明](#仓库目录说明)
- [简介](#简介)
- [已有功能](#已有功能)
  - [基础功能](#基础功能)
  - [可拓展功能](#可拓展功能)
  - [user.py功能](#userpy功能)
- [使用方式](#使用方式)
  - [部署自定义机器人](#部署自定义机器人)
  - [部署user.py监控机器人](#部署userpy监控机器人)
- [前瞻计划](#前瞻计划)
  - [用户要求](#用户要求)
  - [部署方法](#部署方法)
- [常用命令](#常用命令)
# 仓库目录说明
```text
JD_Diy/                     # JD_Diy 仓库
  |-- backup                    # 移除的旧文件
  |-- beta                      # 测试版机器人
  |-- config                    # 配置目录
  |-- jbot                      # 正式版机器人
  |-- module                    # 实例模块
  |-- other                     # 不便于分类脚本
  |-- pys                       # python脚本
  |-- shell                     # shell脚本
  |-- scripts                   # 插件依赖脚本
  |-- requirements.txt          # 依赖文件
  `-- README.md                 # 仓库说明
```
## 简介
随着 v4-bot 启动而启动的自定义机器人，其中大部分功能亦支持青龙用户。
## 已有功能
### 基础功能
- [x] 发送 `/start` 指令可开启自定义机器人
- [x] 发送 `/restart` 指令可重启机器人
- [x] 发送 `/help` 指令可获取快捷命令
- [x] 发送 `/install` 指令可拓展功能
- [x] 发送 `/uninstall` 指令可卸载功能
- [x] 发送 `/list` 指令列出已有功能
### 可拓展功能
- [x] 发送 `/upbot` 升级自定义机器人
- [x] 发送 `/checkcookie` 检测过期情况
- [x] 发送 `/export` 修改环境变量
- [x] 发送 `/blockcookie` 进行屏蔽操作
- [x] 发送 `pin=xxx;wskey=xxx;` 快速添加 `wskey`
- [x] 下载 `.js` `.sh` 的 `raw` 文件
- [x] 添加以 `.git` 结尾的仓库链接可添加仓库
- [x] 发送 `变量名="变量值"` 的格式消息可快捷添加环境变量
### user.py功能
- [x] 监控龙王庙频道，监控并定时执行红包雨
- [x] 关注店铺有礼自动执行（需自行配置频道ID）
- [x] 自动替换某些环境变量（需自行配置频道ID）
- [x] ~~监控动物园频道，自动下载开卡脚本并选择执行~~\
  user.py提供模板，实际请自行更改
# 使用方法
## 部署自定义机器人
进入容器中执行以下命令即可，此命令也可以在机器人中使用（即使用 /cmd 指令）
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/diybot.sh ]; then rm -f $root/diybot.sh; fi; cd $root; wget https://raw.githubusercontent.com/msechen/JD_Diy/main/shell/diybot.sh; bash diybot.sh
```
## 部署[user.py]监控机器人
首先进入容器中执行以下命令，然后按提示操作即可（此命令禁止在机器人中使用）
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/user.sh ]; then rm -f $root/user.sh; fi; cd $root; wget https://raw.githubusercontent.com/msechen/JD_Diy/main/shell/user.sh; bash user.sh
```
重要提醒：user.py监控机器人登录比较困难，如果一次不能登录，请使用命令pip3 install telethon --upgrade先升级最新客户端，然后命令sh user.sh选择2卸载后再重新安装，登录手机号码格式008613XXXXXXX。


# 常用命令
1. 升级原机器人程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/bot.sh ]; then rm -f $root/bot.sh; fi; cd $root; wget https://raw.githubusercontent.com/SuMaiKaDe/bot/main/config/bot.sh; bash bot.sh
```
2. 重启程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 restart jbot; else ps -ef | grep 'python3 -m jbot' | grep -v grep | awk '{print $1}' | xargs kill -9 2>/dev/null; nohup python3 -m jbot >/ql/log/bot/bot.log 2>&1 & fi 
```
3. 启动程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 start jbot; else nohup python3 -m jbot >/ql/log/bot/bot.log 2>&1 & fi 
```
4. 停止程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 stop jbot; else ps -ef | grep 'python3 -m jbot' | grep -v grep | awk '{print $1}' | xargs kill -9 2>/dev/null; fi 
```
5. 卸载diy程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; rm -f $root/jbot/diy/*.py
```
6. 卸载user监控程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; cd $root; rm -f user.session; rm -f user.session-journal; rm -f $root/jbot/diy/user.py
```
7. 重启user监控程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; cd $root; bash user.sh
```
8. 一键
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/bot.sh ]; then rm -f $root/bot.sh; fi; cd $root; wget https://cdn.jsdelivr.net/gh/SuMaiKaDe/bot@main//config/bot.sh; bash bot.sh; if [ -f $root/diybot.sh ]; then rm -f $root/diybot.sh; fi; cd $root; wget https://raw.githubusercontent.com/msechen/JD_Diy/main/shell/diybot.sh; bash diybot.sh; if [ -f $root/user.sh ]; then rm -f $root/user.sh; fi; cd $root; wget https://raw.githubusercontent.com/msechen/JD_Diy/main/shell/user.sh; bash user.sh
```
  
