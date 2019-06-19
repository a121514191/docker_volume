# docker_volume (體積)
為了確保相關資料及設定不會隨著 container 消滅而不見，

當你需要指定的資料數量很多或是需要建立很多個相同的container時，

Data Volume Container，其實就是個一般容器，儲存你的資料，

特別的是你可以將許許多多的 volume 指定在 Data Volume Container 上，

再將其他需要共同資料的 container 指向這個 data volume container ，

data volume container 也支援備份及還原的功能。

# 實作流程

### 首先建立一個容器 --name(命名)  busybox為dockerhub上的image

>docker create -v /var/www/html --name dataContainer busybox

>docker create -v /config --name volume_test busybox

![](https://github.com/a121514191/docker_2/blob/master/centos.PNG)

### 查看

>docker ps -a 

![](https://github.com/a121514191/docker_2/blob/master/centos.PNG)

### 將你要的文件cp(複製)到剛剛建立的容器裡面

!這邊卡了很久，原因只出在於範例多了空白

docker cp path/file volume_test:/config/ (O)
>docker cp test.txt volume_test:/config/ 

![](https://github.com/a121514191/docker_2/blob/master/centos.PNG)

docker cp path/file volume_test:/ config / (X)
>docker cp test.txt volume_test:/ config / 

![](https://github.com/a121514191/docker_2/blob/master/centos.PNG)



### 之後將我們要的檔案附加進去容器

可以看到原本放在我們容器的config在這個容器也有了
再往裡面找能找到剛剛所加入的test.txt

>docker run -it --volumes-from volume_test ubuntu 
>ls
>cd config
>ls

![](https://github.com/a121514191/docker_2/blob/master/lowercase.PNG)

### 最後是導入和導出容器數據

>docker export  volume_test> dataContainer.tar

>docker import  volume_test.tar

!!!不知為何導出無數據

### 實做部分


