### 访问 Tick Hosting 官网

1. 点击: `Start now`
2. 需要通过Discord登录, 点击: `Login with Discord`
3. 登录完成后点击左侧的: `Free Servers`, 右侧出现的卡片, 会默认选中: `Free Minecraft`
4. 点击: `Get Free Server`, 此刻等待创建完成

### 配置

1. 等待创建完成, 点击左侧: `Servers` 即可看到创建完成的服务器, 点击服务器
2. 选择左侧: `Files` 菜单
3. 找到文件: `server.jar` 删除 (不需要,上传我们自己的代码, 最后提供下载地址)
4. 上传文件: `server.jar` `server1.jar` `start.sh`
5. 修改以上三个文件权限, 文件行尾的菜单点击选择: `Permissions`, 输入: `777`, 点击: `UPDATE` 保存
6. 修改启用文件: `start.sh` 修改步骤看下方

#### 修改启动文件

1. 点击: `start.sh` 文件, 打开编辑页面
2. 修改以下三个配置项目(参数看后面详细说明)

```
#!/usr/bin/env bash
NEZHA_SERVER=${NEZHA_SERVER:-''}
NEZHA_PORT=${NEZHA_PORT:-''}
NEZHA_KEY=${NEZHA_KEY:-''}
+ ARGO_DOMAIN=${ARGO_DOMAIN:-'【tick.你的域名.com】'}
+ ARGO_AUTH=${ARGO_AUTH:-'【cloudflare中得到的令牌】'}
WSPATH=${WSPATH:-'argo'}
+ UUID=${UUID:-'【这里填写UUID】'}

# 第84行 删除 --tls
- nohup ./nm -s ${NEZHA_SERVER}:${NEZHA_PORT} -p ${NEZHA_KEY} --tls >/dev/null 2>&1 &
+ nohup ./nm -s ${NEZHA_SERVER}:${NEZHA_PORT} -p ${NEZHA_KEY} >/dev/null 2>&1 &
```

> 生成 ARGO_DOMAIN + ARGO_AUTH
>
> 1. 打开cloudflare官网, 登录
> 2. 点击左侧: `Zero Trust`
> 3. 页面打开后, 点击左侧: `Networks`, 继续点击: `Tunnels`
> 4. 点击页面中的: `Create a tunnel`
> 5. 创建页面名称Tunnel name自定义,比如叫: `tick`, 然后点击: `Save tunnel`
> 6. 最后页面即可得到令牌, 也就是: ARGO_AUTH (这里的令牌不需要前部分: cloudflared.exe service install ,只需要最后一个长字符串)
> 7. 返回列表, 找到创建的隧道, 点击菜单, 点击配置: `Configure`
> 8. 页面打开点击: `Public Hostname`, 配置二级域名
> 9. 点击: `Add a public hostname`
> 10. 在`Public Hostname Page`页面, Subdomain自定义, 比如叫: `tick`, Domain选择自己的域名, Path为空
> 11. Type选择: `HTTP`, URL输入: `localhost:8080`
> 12. 最后点击: `Save hostname`, 完成
> 13. 最后得到ARGO_DOMAIN: `tick.你的域名.com`

### 启动

1. 点击左侧: `Console`
2. 页面中点击: `Start`
3. 最后控制台输出:

```
vless链接已经生成, www.speedtest.net 可替换为CF优选IP

vless://这里是你的UUID@www.speedtest.net:443?encryption=none&security=tls&type=ws&host=tick.你的域名.com&path=/argo-vless#IT-Vodafone%20Italia%20DSL-Pontedera_tls

端口 443 可改为 2053 2083 2087 2096 8443

vless://这里是你的UUID@www.speedtest.net:80?encryption=none&security=none&type=ws&host=tick.你的域名.com&path=/argo-vless#IT-Vodafone%20Italia%20DSL-Pontedera

端口 80 可改为 8080 8880 2052 2082 2086 2095
```

### UUID生成

#### 第一种方式

1. Windows电脑, 打开命令行, Win + R > cmd
2. 输入: `Powershell -NoExit -Command "[guid]::NewGuid()"`

#### 第二种方式 使用v2rayN 软件

1. 点击菜单中: `服务器`, 继续点击: `添加[VLESS]服务器`
2. 找到用户ID(id), 点击后面: `生成`
