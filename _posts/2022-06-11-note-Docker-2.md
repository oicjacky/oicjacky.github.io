---
layout: post
title: "Docker II"
subtitle: 
tags: [docker]
comments: true
published: true
---

### 情境三：手上有一個影像辨識App(用Flask架構出來)，用container做為測試環境

這裡我們拆解成三個部分，一般來說無絕對先後順序，有可能一開始就用docker開發，
有可能從既有的服務容器化。

1. 開發程式碼檔案
2. 設置好container
3. 啟用app服務並測試

先編寫好我們的`dockerfile`，直接下載[pytorch image](https://hub.docker.com/r/pytorch/pytorch)，並在裡面安裝使用到的工具
git, vim, jupyter和flask：

```dockerfile
FROM pytorch/pytorch

RUN apt-get update && \
    apt-get install -y git vim && \
    python -m pip install jupyter flask
```

接著Build image，
<img src="/assets/images/docker-II/docker-II-01.png" style="vertical-align:middle;margin:0px 0px" width="100%">

根據平常開發程式碼放置地方，有三種選擇：

(i) 在[github](https://github.com/oicjacky/ML-course-of-Lee/tree/main/ImageNetAPP)
```bash
> docker run -it -p 30:30 image_net_app
> git clone https://github.com/oicjacky/ML-course-of-Lee.git
> cd ML-course-of-Lee/ImageNetAPP/
> ls
README.md  app.py  imagenet_class_index.json  inference.py
```

(ii) 在本機端，掛載硬碟方式啟動container
```bash
> docker run -it -p 30:30 -v C:\Users\user\Pyvirtualenv\course_CNN\ImageNetAPP:/mount/ImageNetAPP image_net_app
> cd /mount/ImageNetAPP
> ls
README.md  __pycache__  app.py  dockerfile  imagenet_class_index.json  inference.py
```
<!-- <img src="/assets/images/docker-II/docker-II-04.png" style="vertical-align:middle;margin:0px 0px" width="100%"> -->

(iii) 一樣在本機端，但在Build image時就把它一起打包進去

```dockerfile
# 內容和上面dockerfile一樣
# '.'代表你目前工作目錄底下檔案都會複製進去/mount/ImageNetAPP
# 可以用.dockerignore
COPY . /mount/ImageNetAPP
```
<img src="/assets/images/docker-II/docker-II-05.png" style="vertical-align:middle;margin:0px 0px" width="100%">

這裡我選擇(i)作為操作結果。

進入container後，設定好環境變數後，就可以跑flask服務啟動app.py：
<img src="/assets/images/docker-II/docker-II-02.png" style="vertical-align:middle;margin:0px 0px" width="100%">

最後我們測試從本機送請求給container的app服務：
```python
import requests
resp = requests.post("http://localhost:30/predict",
                     files={"file": open(r'C:\Users\user\Pyvirtualenv\course_CNN\images\kobe.png','rb')})
print(resp.json())
```
這時container裡的terminal：

<img src="/assets/images/docker-II/docker-II-03.png" style="vertical-align:middle;margin:0px 0px" width="100%">

可以看到我們成功收到172.17.0.1(我的本機)的POST request，服務返回模型判斷這張照片是basketball。

<img src="/assets/images/docker-II/Kobe.png" style="vertical-align:middle;margin:0px 90px" width="60%">



### Reference
1. [Docker](https://zh.wikipedia.org/wiki/Docker)
2. [如何將 Docker 應用在資料科學](https://leemeng.tw/3-ways-you-can-leverage-the-power-of-docker-in-data-science-part-1-learn-the-basic.html)
3. [Dockerfile實踐](https://vuepress.mirror.docker-practice.com/appendix/best_practices/)
4. [Docker for beginners](https://docker-curriculum.com/#hello-world)
5. [A great docker_practice repo by Cheng-hao, Lee](https://github.com/harry83017622/docker_practice)