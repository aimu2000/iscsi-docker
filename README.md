https://www.msn.cn/zh-cn/news/other/iscsi-or-smb-%E4%B8%80%E8%B5%B7%E9%83%A8%E7%BD%B2%E4%B8%80%E4%B8%AAiscsi%E6%9C%8D%E5%8A%A1%E7%AB%AF-%E5%B0%86nas%E7%A9%BA%E9%97%B4%E6%8C%82%E8%BD%BD%E6%88%90%E7%9C%9F%E6%AD%A3%E7%9A%84%E7%94%B5%E8%84%91%E7%A1%AC%E7%9B%98/ar-AA1p1bqN?ocid=BingHp01&cvid=83686bd1d63447cda341d474f4fbb1a5&ei=133

# iscsi-docker
tgt in docker，基于[fujita/tgt](https://github.com/wtnb75/docker-stgt)和[wtnb75/docker-stgt](https://github.com/fujita/tgt)将配置融入到启动脚本，直接通过环境变量即可进行target配置，无需执行脚本
```
services:
    iscsi-docker:
        container_name: iscsi-docker
        restart: unless-stopped
        network_mode: host
        privileged: true
        volumes:
            - /run/lvm:/run/lvm
            - /lib/modules:/lib/modules
            - /sys/kernel/config:/sys/kernel/config
            - /dev:/dev
        environment:
            - targetname=koryking  ##弄一个自己可以识别的target name
            - lundev1=/dev/sda3
         ## - lundev2=/dev/sda4 ##还想加挂载盘就继续增加lundev后的数字，如lundev3,lundev4
            - ip_address=192.168.66.0/24 ## 修改成自己的ip网段
        image: koryking/iscsi-docker
```
