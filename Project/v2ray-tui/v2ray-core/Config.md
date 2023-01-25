--- 
# 服务端配置
你需要一台防火墙外的服务器，来运行服务器端的 V2Ray。配置如下：
```json
{
    "inbounds": [
        {
            "port": 10086, // 服务器监听端口
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": "b831381d-6324-4d53-ad4f-8cda48b30811"
                    }
                ]
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom"
        }
    ]
}
```
服务器的配置中需要确保 id 和端口与客户端一致，就可以正常连接了。

# 客户端配置
在你的 PC（或手机）中，需要用以下配置运行 V2Ray ：
```json
{
    "inbounds": [
        {
            "port": 1080, // SOCKS 代理端口，在浏览器中需配置代理并指向这个端口
            "listen": "127.0.0.1",
            "protocol": "socks",
            "settings": {
                "udp": true
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "server", // 服务器地址，请修改为你自己的服务器 ip 或域名
                        "port": 10086, // 服务器端口
                        "users": [
                            {
                                "id": "b831381d-6324-4d53-ad4f-8cda48b30811"
                            }
                        ]
                    }
                ]
            }
        },
        {
            "protocol": "freedom",
            "tag": "direct"
        }
    ],
    "routing": {
        "domainStrategy": "IPOnDemand",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "direct"
            }
        ]
    }
}
```
上述配置唯一要更改的地方是你的服务器 IP，配置中已注明。上述配置会把除局域网（比如访问路由器）以外的所有流量转发至你的服务器。
在配置当中，有一个 id (在这里的例子是 b831381d-6324-4d53-ad4f-8cda48b30811)，作用类似于 Shadowsocks 的密码 (password), 相对应的 VMess 传入传出的 id 必须相同（如果你不是很明白这句话，那么可以简单理解成服务器与客户端的 id 必须相同）

# 运行

- 在 Windows 和 macOS 中，配置文件通常是 V2Ray 同目录下的 config. json 文件。直接运行 v2ray 或 v2ray. exe 即可。
- 在 Linux 中，配置文件通常位于 /etc/v2ray/ 或 /usr/local/etc/v2ray/ 目录下。运行 v2ray run -c /etc/v2ray/config. json，或使用 systemd 等工具将 V2Ray 作为服务在后台运行。



