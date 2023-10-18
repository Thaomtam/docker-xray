
## Clone the Project Repository:

```
git clone https://github.com/Thaomtam/docker-xray
```


## Start a container

```
mkdir -p /etc/xray
```

```
/etc/xray/config.json
```

## Mẫu

```
cat << EOF > /etc/xray/config.json
{
  "log": {
    "loglevel": "warning"
  },
  "inbounds": [
    {
      "listen": "0.0.0.0",
      "port": 443,
      "protocol": "vless",
      "settings": {
        "clients": [
          {
            "id": "thoi-tiet-openwrt",
            "flow": "xtls-rprx-vision"
          }
        ],
        "decryption": "none",
        "fallbacks": [
          {
            "dest": "8004",
            "xver": 1
          },
          {
            "dest": "8005",
            "xver": 1
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "security": "reality",
        "realitySettings": {
          "dest": "1.1.1.1:443",
          "serverNames": [
            "lienquan.garena.vn",
            "m.tiktok.com"
          ],
          "privateKey": "sELUHVtMZVXnBVNLOJYOR9NdpZbR7QVjS5b9X0F6iGU",
          "shortIds": [
            "e9455277471d0a78"
          ]
        }
      }
    },
    {
      "listen": "127.0.0.1",
      "port": 8004,
      "protocol": "vless",
      "settings": {
        "clients": [
          {
            "id": "thoi-tiet-openwrt"
          }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "h2",
        "sockopt": {
          "acceptProxyProtocol": true
        }
      }
    },
    {
      "listen": "127.0.0.1",
      "port": 8005,
      "protocol": "trojan",
      "settings": {
        "clients": [
          {
            "password": "thoi-tiet-openwrt"
          }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "sockopt": {
          "acceptProxyProtocol": true
        }
      }
    },
	   {
      "listen": "0.0.0.0",
      "port": 80,
      "protocol": "vless",
      "settings": {
        "clients": [
          {
            "id": "thoi-tiet-openwrt",
            "flow": "xtls-rprx-vision"
          }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "security": "reality",
        "realitySettings": {
          "dest": "1.1.1.1:443",
          "serverNames": [
            "lienquan.garena.vn",
            "m.tiktok.com"
          ],
          "privateKey": "sELUHVtMZVXnBVNLOJYOR9NdpZbR7QVjS5b9X0F6iGU",
          "shortIds": [
            "e9455277471d0a78"
          ]
        }
      }
    },
    {
      "listen": "0.0.0.0",
      "port": 16557,
      "protocol": "socks",
      "settings": {
        "auth": "password",
        "accounts": [
          {
            "user": "admin",
            "pass": "admin123"
          }
        ],
        "udp": true,
        "ip": "127.0.0.1"
      },
      "streamSettings": {
        "network": "tcp",
        "security": "none"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "tag": "block"
    }
  ],
  "policy": {
    "levels": {
      "0": {
        "handshake": 2,
        "connIdle": 120
      }
    }
  }
}
EOF
```

## RUN

```
😂😂😂😂
```

**Warning**: Hàng không free