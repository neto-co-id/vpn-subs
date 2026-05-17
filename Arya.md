{
  "log": {},
  "inbounds": [
      {
        "port": 10808,
        "protocol": "socks",
        "listen": "127.0.0.1",
        "settings": {
          "userLevel": 8,
          "auth": "noauth",
          "udp": true
        },
        "tag": "socks"
      },
      {
        "port": 1087,
        "protocol": "socks",
        "listen": "127.0.0.1",
        "settings": {
          "userLevel": 8,
          "auth": "noauth",
          "udp": true
        },
        "tag": "directSocks"
      },
      {
        "port": 62789,
        "protocol": "dokodemo-door",
        "listen": "[::1]",
        "settings": {
          "address": "[::1]"
        },
        "tag": "api"
      }
    ],
  "outbounds": [
      {
        "protocol": "trojan",
        "streamSettings": {
          "security": "tls",
          "network": "ws",
          "tlsSettings": {
            "serverName": "id-uninet3.wc-webkuy.web.id",
            "allowInsecure": false,
            "fingerprint": "chrome",
            "alpn": []
          },
          "wsSettings": {
            "path": "/trojan",
            "headers": {
              "Host": "id-uninet3.wc-webkuy.web.id"
            }
          }
        },
        "mux": {
          "xudpConcurrency": 128,
          "enabled": false,
          "concurrency": 50,
          "xudpProxyUDP443": "allow"
        },
        "settings": {
          "servers": [
            {
              "password": "99989f42-b0cb-4ce1-9e78-87db4068c79f",
              "port": 443,
              "address": "104.17.2.81",
              "email": "",
              "flow": "",
              "level": 8
            }
          ]
        },
        "tag": "proxy"
      },
      {
        "protocol": "freedom",
        "streamSettings": {
          "sockopt": {
            "tcpNoDelay": true
          }
        },
        "settings": {
          "userLevel": 8,
          "fragment": {
            "length": "80-250",
            "interval": "10-100",
            "packets": "tlshello"
          }
        },
        "tag": "fragment"
      }
    ],
  "api": {
      "services": [
        "StatsService"
      ],
      "tag": "api"
    },
  "dns": {
      "disableCache": true,
      "queryStrategy": "UseIP",
      "disableFallbackIfMatch": true,
      "tag": "dnsQuery",
      "disableFallback": true,
      "hosts": {
        "common.dot.dns.yandex.net": [
          "77.88.8.8",
          "77.88.8.1",
          "2a02:6b8::feed:0ff",
          "2a02:6b8:0:1::feed:0ff"
        ],
        "dns.google": [
          "8.8.8.8",
          "8.8.4.4",
          "2001:4860:4860::8888",
          "2001:4860:4860::8844"
        ],
        "dot.pub": [
          "1.12.12.12",
          "120.53.53.53"
        ],
        "dns.alidns.com": [
          "223.5.5.5",
          "223.6.6.6",
          "2400:3200::1",
          "2400:3200:baba::1"
        ],
        "dns.quad9.net": [
          "9.9.9.9",
          "149.112.112.112",
          "2620:fe::fe",
          "2620:fe::9"
        ],
        "dns.cloudflare.com": [
          "104.16.132.229",
          "104.16.133.229",
          "2606:4700::6810:84e5",
          "2606:4700::6810:85e5"
        ],
        "cloudflare-dns.com": [
          "104.16.248.249",
          "104.16.249.249",
          "2606:4700::6810:f8f9",
          "2606:4700::6810:f9f9"
        ],
        "one.one.one.one": [
          "1.1.1.1",
          "1.0.0.1",
          "2606:4700:4700::1111",
          "2606:4700:4700::1001"
        ]
      },
      "servers": [
        {
          "address": "8.8.8.8",
          "skipFallback": false
        }
      ]
    },
  "stats": {},
  "routing": {
        "balancers": [],
        "rules": [
            {
              "ruleTag": "rule-0",
              "type": "field",
              "inboundTag": [
                "api"
              ],
              "outboundTag": "api"
            },
            {
              "ruleTag": "rule-1",
              "type": "field",
              "inboundTag": [
                "dnsQuery"
              ],
              "outboundTag": "proxy"
            },
            {
              "ruleTag": "rule-2",
              "type": "field",
              "inboundTag": [
                "directSocks"
              ],
              "outboundTag": "direct"
            },
            {
              "ruleTag": "rule-3",
              "type": "field",
              "inboundTag": [
                "api"
              ],
              "outboundTag": "api"
            },
            {
              "ruleTag": "rule-4",
              "type": "field",
              "inboundTag": [
                "dnsQuery"
              ],
              "outboundTag": "proxy"
            },
            {
              "ruleTag": "rule-5",
              "type": "field",
              "inboundTag": [
                "directSocks"
              ],
              "outboundTag": "direct"
            }
          ],
        "domainStrategy": "AsIs"
      },
  "policy": {
        "system": {
          "statsOutboundDownlink": true,
          "statsInboundDownlink": true,
          "statsOutboundUplink": true,
          "statsInboundUplink": true
        },
        "levels": {
          "8": {
            "uplinkOnly": 1,
            "statsUserDownlink": false,
            "downlinkOnly": 1,
            "handshake": 4,
            "connIdle": 30,
            "statsUserUplink": false,
            "bufferSize": 0
          }
        }
      },
  "transport": {}
}
