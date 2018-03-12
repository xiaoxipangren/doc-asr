# Asr-tool docker镜像安装使用指南

## 系统要求

### Docker

推荐安装17.09.0-ce\(community edition\)或更高版本，具体安装步骤请参考[https://docs.docker.com/install/](https://docs.docker.com/install/ "官方文档")

# 安装

只需要将asr-tool的docker镜像pull到本地便完成安装：

```bash
sudo docker pull registry.cn-hangzhou.aliyuncs.com/nationalchip/asr:jieba
```

# 运行容器

```bash
#镜像重tag为 asr:jieba
sudo docker tag registry.cn-hangzhou.aliyuncs.com/nationalchip/asr:jieba asr:jieba 

#删除原有的同名asr容器
sudo docker stop asr
sudo docker rm asr

#以asr为容器名运行该镜像
sudo docker run --name asr -dit asr:jieba
```

# 执行Asr tool

```bash
#拷贝语料到容器内，text为文本格式的按行分割关键词或语句的语料文件
sudo docker cp text asr:/asr/

#直接进入容器内部，调用asr工具
sudo docker exec -it asr bash

#$:开头的命令为容器内命令
$:cd /asr
#查看asr tool帮助文档
$:cat README

#调用asr工具训练语料
#text文上述传入的语料文件，可随意命名
$:./run.sh text

#训练结果保存在/asr/data/search_Graph中，包括words.txt TLG.fst两个文件
#训练时间视机器配置和语料的大小而定
#训练完成后退出容器
$:exit

#拷贝结果到本地
sudo docker cp asr:/asr/data/search_Graph/words.txt ./
sudo docker cp asr:/asr/data/search_Graph/TLG.txt ./
```



