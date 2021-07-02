---
layout: post
title: "Start Docker"
subtitle: 
tags: [docker]
comments: true
published: true
---

### Cloud Computing And Docker
- Use cloud computing e.g. AWS、GCP、Azure
- To deploy, train, scale the machine learning model.

### Why Docker ?
Data Science 常用的 App (application)可以是：
- 一個包含 [TensorFlow](https://www.tensorflow.org/) 庫的 [Jupyter Notebook](https://jupyter.org/) 伺服器
- 一個 ML 產品，如透過已訓練的模型來判斷圖片裡頭有沒有[貓咪的 Flask App](https://github.com/leemengtaiwan/cat-recognition-app)
- 一個 SQL 查詢以及資料視覺化 dashborad 工具，如 [Superset](https://github.com/apache/superset)
- 一個簡單的 Python Script，針對輸入的大量數據做處理

Docker 的容器就是這樣的一個概念，幫你事先將一個 App 所需要的所有環境，包含作業系統都「容納」在一起。

<img src="/assets/images/start_docker/image/0_9xWcmttq6cQfVPWU.png" style="vertical-align:middle;margin:0px 30px" width="80%">


容器裡頭不只包含 App 自己本身的程式碼，也涵蓋了所有能讓這個 App 順利執行的必要環境：

- Python 函式庫，如特定版本的 TensorFlow、Pandas 及 Jupyter Notebook
- MySQL、MongoDB 等 App 會用到的資料庫
- App 會用到的各種 metadata、資料集
- 各種 OS 限定的驅動程式（drivers）、依賴函式庫
- 其他（把所有你想得到的東西填進來）

### What is Docker ?
- Dockerfile: many open source on [Docker Hub](https://hub.docker.com/)
- Docker image: build from Dockerfile
- Docker container: run by Docker image

<img src="/assets/images/start_docker/image/0_LF94f5-yeqCsRXXC.png" style="vertical-align:middle;margin:0px 20px" width="100%">

for example, we can pull a image created by Tensorflow:
```bash
> docker pull tensorflow/tensorflow
> docker images
> docker run -it -p 1234:8888 tensorflow/tensorflow
```

If there is a `Dockerfile` as following:
```docker
FROM ubuntu:16.04

RUN apt-get update -y && apt-get install -y software-properties-common && add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update -y && apt-get install -y \
 python3.6 \
 python3-pip \
 curl \
 git
```

Build it with `docker build -t IMAGE_NAME .`, then we can see
```bash
E:\repository\docker\start_docker>docker images                                                                                                      0.0s 
REPOSITORY              TAG       IMAGE ID       CREATED              SIZE                                                                           0.0s 
test_image_2            latest    ba1bc33f6138   About a minute ago   581MB                                                                          0.0s 
test_image_1            latest    d9b475a5f117   2 weeks ago          135MB                                                                          0.0s 
tensorflow/tensorflow   latest    45872ba1e662   5 months ago         1.57GB          
```

And run it by `docker run -it -p IP:PORT IMAGE_NAME`:
```bash
E:\repository\docker\start_docker>docker run -it -p 1111:3333 test_image_2
root@db3767f997ab:/
```


### Summary
- Docker 是一個能幫我們在各種不同 OS 上建置開發環境的工具
- Docker 三元素包含 Dockerfile、Docker 映像檔（Image）以及 Docker 容器（Container）
- Docker 利用 Dockerfile 預先建置好一個 Docker 映像檔。在使用者想要使用容器的時候，以該映像檔為基礎，運行一個對應的 Docker 容器
- Docker Hub 上有各式各樣可以直接供使用的映像檔
- 你只需要 docker pull 及 docker run 就能開始一個分析專案


### Reference
1. [Docker](https://zh.wikipedia.org/wiki/Docker)
2. [如何將 Docker 應用在資料科學](https://leemeng.tw/3-ways-you-can-leverage-the-power-of-docker-in-data-science-part-1-learn-the-basic.html)
3. [Dockerfile實踐](https://vuepress.mirror.docker-practice.com/appendix/best_practices/)
4. [Docker for beginners](https://docker-curriculum.com/#hello-world)
5. [A great docker_practice repo by Cheng-hao, Lee](https://github.com/harry83017622/docker_practice)