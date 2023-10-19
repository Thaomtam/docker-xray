## Install docker
```
curl -fsSL https://get.docker.com | sh
```

## Clone the Project Repository:

```
git clone https://github.com/Thaomtam/docker-xray && cd docker-xray
```
## Build docker image
```
docker build -t docker-xray .
```

## Start a container

```
mkdir -p /etc/xray
```

```
/etc/xray/config.json
```
## Xem quy trình Xray đang sử dụng % CPU :
```
docker exec -it docker-xray ps
```
## Status :
```
docker ps -a | grep docker-xray
```
## Start :
```
docker start docker-xray
```
## Stop :
```
docker stop docker-xray
```
## Remove :
```
docker rm -f docker-xray
```

## Mẫu

```
cat << EOF > /etc/xray/config.json
{
  "dns": {
    "servers": [
      "1.1.1.1",
      "1.0.0.1"
    ]
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
  ]
}
EOF
```

## RUN

```
docker run -d -p443:443 -p80:80 -p16557:16557 -p8004:8004 -p8005:8005 --name docker-xray --restart=always -v /etc/xray:/etc/xray docker-xray
```

**Warning**: Hàng không free
