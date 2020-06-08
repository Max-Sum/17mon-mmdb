# 17mon MMDB

![Daily Build](https://github.com/Max-Sum/mmdb_china_ip_list/workflows/Daily%20Build/badge.svg)

GeoIP MMDB from 17mon

适合在网络分流工具中使用，对中国IP的匹配分流更为友好，兼容MaxMind DB的客户端！

每周自动拉取新的17mon数据库，并发布一个新的Release版本。


## 固定下载连接

[Country.mmdb](https://raw.githubusercontent.com/Max-Sum/mmdb_china_ip_list/release/Country.mmdb)
[version](https://raw.githubusercontent.com/alecthw/mmdb_china_ip_list/release/version)

## 简介

在网络分流工具(例如Clash)中使用[MaxMind](https://www.maxmind.com/en/home)的`GeoLite2-Country`对中国IP的匹配不是很友好，实际使用中出现不少问题。

此项目，使用17mon提供的[数据库](https://cdn.ipip.net/17mon/country.zip)，结合Maxmind的IPv6库，使得对中国IP匹配得更为友好。

## 使用

从[Release](https://github.com/Max-Sum/mmdb_china_ip_list/releases)下载生成的`Country.mmdb`。

使用方式同MaxMind官方API，可参考[指导文档](http://maxmind.github.io/MaxMind-DB/)。

### OpenClash中使用

替换掉`/etc/openclash/Country.mmdb`，最后重启下clash即可。

## 构建

需要`perl`环境，`MaxMind-DB-Writer-perl`的依赖和使用可以参考[官方文档](https://github.com/maxmind/MaxMind-DB-Writer-perl)。

``` bash
# 下载mmdb writer
git clone https://github.com/maxmind/MaxMind-DB-Writer-perl.git writer
cd writer

# 安装依赖
curl -LO http://xrl.us/cpanm
perl cpanm --installdeps -n .
perl cpanm -n Path::Class

# 构建
./Build manifest
perl Build.PL
./Build install

# 返回上级目录
cd ..

# 下载本项目
git clone https://github.com/Max-Sum/mmdb_china_ip_list.git
cd mmdb_china_ip_list

# 下载GeoLite2-Country-CSV
curl -L -o GeoLite2-Country-CSV.zip "https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-Country-CSV&license_key=JvbzLLx7qBZT&suffix=zip"
unzip GeoLite2-Country-CSV.zip
rm -f GeoLite2-Country-CSV.zip
mv GeoLite2* mindmax

# 下载17mon
curl -L -o 17mon.zip "https://cdn.ipip.net/17mon/country.zip"
unzip 17mon.zip

#构建
perl china_ip_list.pl
```
生成的文件为`Country.mmdb`。

## MaxMind GeoIP 格式

官方对自己的数据库中的内容说明很少，都是自己一点点跟代码找出来的格式，然后据此生成的数据库。

下面列出所有字段示例供参考。

头
``` json
{
    "database_type": "GeoLite2-Country",
    "binary_format_major_version": 2,
    "build_epoch": 1589304057,
    "ip_version": 6,
    "languages": [
        "de",
        "en",
        "es",
        "fr",
        "ja",
        "pt-BR",
        "ru",
        "zh-CN"
    ],
    "description": {
        "en": "GeoLite2 Country database"
    },
    "record_size": 24,
    "node_count": 616946,
    "binary_format_minor_version": 0
}
```

network->字段
``` json
{
    "continent": {
        "code": "AS",
        "names": {
            "de": "Asien",
            "ru": "Азия",
            "pt-BR": "Ásia",
            "ja": "アジア",
            "en": "Asia",
            "fr": "Asie",
            "zh-CN": "亚洲",
            "es": "Asia"
        },
        "geoname_id": 6255147
    },
    "country": {
        "names": {
            "de": "China",
            "ru": "Китай",
            "pt-BR": "China",
            "ja": "中国",
            "en": "China",
            "fr": "Chine",
            "zh-CN": "中国",
            "es": "China"
        },
        "iso_code": "CN",
        "geoname_id": 1814991,
        "is_in_european_union": false,
    },
    "registered_country": {
        "names": {
            "de": "China",
            "ru": "Китай",
            "pt-BR": "China",
            "ja": "中国",
            "en": "China",
            "fr": "Chine",
            "zh-CN": "中国",
            "es": "China"
        },
        "iso_code": "CN",
        "geoname_id": 1814991
    },
    "represented_country": {
        "names": {
            "de": "China",
            "ru": "Китай",
            "pt-BR": "China",
            "ja": "中国",
            "en": "China",
            "fr": "Chine",
            "zh-CN": "中国",
            "es": "China"
        },
        "iso_code": "CN",
        "geoname_id": 1814991
    },
    "traits": {
        "is_anonymous_proxy": true,
        "is_satellite_provider": true
    }
}
```

## 感谢

- [GeoIP MaxMind DB 生成指南](https://blog.csdn.net/openex/article/details/53487465)

- [GeoLite Mirror | Sukka](https://geolite.clash.dev/)

- [使用 GeoLite 实现IP精准定位(Java实现)](https://www.jianshu.com/p/1b1a018ae729)

- [Loyalsoldier提供的GeoLite2-Country-CSV下载链接](https://github.com/Loyalsoldier/v2ray-rules-dat)

## 其他

摸索不易，引用整合或者二次发布还望留个名......
