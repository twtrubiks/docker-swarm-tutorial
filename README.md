# docker-swarm-tutorial

Docker Swarm 基本教學 - 從無到有 Docker-Swarm-Beginners-Guide📝

* [Youtube Tutorial PART 1 - Docker Machine 介紹](https://youtu.be/RSXlK0U-2Bo)
* [Youtube Tutorial PART 2 - Docker Swarm 簡介](https://youtu.be/ir0ApK1rfA4)
* [Youtube Tutorial PART 3 - Docker Swarm 建立 - 基礎篇](https://youtu.be/q2V3ZT5NdNo)

## 簡介

因為 Docker Swarm 很多指令其實都和 Docker 類似，所以建議大家對 Docker 先有

一定的了解，這樣才不會對很多指令都很陌生，可以參考我之前的文章。

* [Docker 基本教學 - 從無到有 Docker-Beginners-Guide](https://github.com/twtrubiks/docker-tutorial)

* [Docker + Django + Nginx + uWSGI + Postgres Tutorial](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial)

* [實戰 Docker + Django + Nginx + uWSGI + Postgres - Load Balance](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-load-balance-tutorial)

* [實戰 Docker + Jenkins + Django + Postgres](https://github.com/twtrubiks/docker-jenkins-django-tutorial)

分散式系統通常都是非常複雜的 :scream:，Docker Swarm 的學習曲線比較低，建議

先對他有些認識，如果你目前猶豫 [Kubernetes](https://kubernetes.io/) ( k8s ) 和 Docker Swarm 要先學哪一個 :confused:

而且你也沒有任何相關分散式系統的經驗，這樣不用思考了，先學 Docker Swarm 就對了:smile:

透過這篇文章，你將會學會

* 認識 Docker Machine

* 認識 Docker Swarm

* 實戰 Docker Swarm + Django ( 等待新增 )

## docker-machine 教學

* [Youtube Tutorial PART 1 - Docker Machine 介紹](https://youtu.be/RSXlK0U-2Bo)

![](https://i.imgur.com/n1QaEcm.png)

可以在本地端練習控制多個虛擬機，等熟悉後，要控制雲端的機器也是一樣的。

### docker-machine 安裝教學

詳細安裝教學可參考  [https://docs.docker.com/machine/install-machine/](https://docs.docker.com/machine/install-machine/)

建議直接裝 [Docker Toolbox](https://docs.docker.com/toolbox/overview/) 會比較快 :smile:

安裝過程基本上很簡單

![](https://i.imgur.com/FH3vuV8.png)

![](https://i.imgur.com/CvRmdYm.png)

灰色的基本上就是一定要安裝的，其他的就看你需不需要安裝。

![](https://i.imgur.com/xahEJt9.png)

最後在輸入下列指令確認是否安裝成功

```cmd
 docker-machine version
```

![](https://i.imgur.com/MxHFzCy.png)

### docker-machine 指令介紹

這邊先簡單介紹一下他的指令，

建立一台 machine，這邊我分 Windows ( 比較麻煩 :triumph: ) 和 Mac，

***Windows*** ( 因為 Hyper-V and VirtualBox 互相會衝突 )

```cmd
docker-machine create --driver hyperv vm1
```

`--driver, -d`， 選擇 Driver to create machine

![](https://i.imgur.com/6GkusmS.png)

windows 用戶還需要額外做設定 :weary: 請參考 [docker-machine - windows 額外設定](https://github.com/twtrubiks/docker-swarm-tutorial#docker-machine---windows-%E9%A1%8D%E5%A4%96%E8%A8%AD%E5%AE%9A)

詳細可參考 [https://docs.docker.com/machine/drivers/hyper-v/](https://docs.docker.com/machine/drivers/hyper-v/)

***Mac***

```cmd
docker-machine create --driver virtualbox vm1
```

詳細可參考 [https://docs.docker.com/machine/drivers/virtualbox/](https://docs.docker.com/machine/drivers/virtualbox/)

`docker-machine create` 更多可參考 [https://docs.docker.com/machine/reference/create/](https://docs.docker.com/machine/reference/create/)

查看目前 machine

```cmd
docker-machine ls
```

可參考 [https://docs.docker.com/machine/reference/ls/](https://docs.docker.com/machine/reference/ls/)

環境變數設定

```cmd
docker-machine env machinename
```

可參考 [https://docs.docker.com/machine/reference/env/](https://docs.docker.com/machine/reference/env/)

連線到指定的 Docker Machine

```cmd
docker-machine ssh machinename
```

範例為 ssh 進去 vm1

![](https://i.imgur.com/8BQq8aR.png)

可參考 [https://docs.docker.com/machine/reference/ssh/](https://docs.docker.com/machine/reference/ssh/)

啟動 machine

```cmd
docker-machine start machinename
```

停止 machine

```cmd
docker-machine stop machinename
```

移除 machine

```cmd
docker-machine rm machinename
```

可參考 [https://docs.docker.com/machine/reference/rm/](https://docs.docker.com/machine/reference/rm/)

查看目前 machine 狀態

```cmd
docker-machine status machinename
```

### docker-machine - windows 額外設定

當使用 `docker-machine env vm1` 查看時，你會發現我們沒有 ipv4

![](https://i.imgur.com/Slr2vpc.png)

這時候就需要做一些額外設定了 :cold_sweat:

我參考這邊圖解給大家看 [https://docs.docker.com/machine/drivers/hyper-v/#example](https://docs.docker.com/machine/drivers/hyper-v/#example)

先找到 Hyper-V 管理員

![](https://i.imgur.com/8OwR0ax.png)

接著選擇虛擬交換器管理員

![](https://i.imgur.com/EPHduBV.png)

建立一個外部的虛擬交換器

![](https://i.imgur.com/rRHmeWG.png)

名稱可以自己訂，這邊就用官方範例的名稱 Primary Virtual Switch

![](https://i.imgur.com/9I0JScb.png)

接著 **重開機** ，避免遇到很怪的問題。

建立 machine 的指令變成下列這樣

```cmd
docker-machine create -d hyperv --hyperv-virtual-switch "<NameOfVirtualSwitch>" <nameOfNode>
```

`NameOfVirtualSwitch` 這是我們剛剛設定的名稱。

試著建立一台 machine

```cmd
docker-machine create -d hyperv --hyperv-virtual-switch "Primary Virtual Switch" vm2
```

![](https://i.imgur.com/7BktDYg.png)

接下來可以再用 `docker-machine env vm2` 查看

![](https://i.imgur.com/bSFO07X.png)

我們得到 ipv4 了:flushed:

## docker swarm 教學

![](https://i.imgur.com/bHwJXgO.png)

### docker swarm 簡介

* [Youtube Tutorial PART 2 - Docker Swarm 簡介](https://youtu.be/ir0ApK1rfA4)

參考 [https://docs.docker.com/engine/swarm/](https://docs.docker.com/engine/swarm/)，我簡單整理 Feature highlights 給大家 :relaxed:

* Cluster management integrated with Docker Engine

    只需要使用 Docker Engine CLI 就可以建立 swarm，不需要再安裝其他的軟體，而且很多指令都和 docker 類似。

* Decentralized design

    可以從單一個 image 直接建立整個 swarm。

* Declarative service model

    docker 使用 declarative 的方式讓你定義各個 service 的狀態。（ 建議 google 一下 Declarative service :smirk: ）

* Scaling

    對於每一個 service，你可以宣告要執行多少數量的任務，當你 scale up or down 的時候，swarm manager 會自動增減來保持所需的狀態。

* Desired state reconciliation

    swarm manager node 會一直監控 cluster 狀態，保持你所需的狀態。舉個例子，假設你設定一個服務有十個 replicas，其中有一台 worker machine 死了兩個 replicas，swarm manager node 會再指派給可運作的 worker 兩個 replicas。

* Multi-host networking

    你可以為你的服務指定 overlay network。在 overlay network 中，當初始化或更新時，swarm manager 會自動指派網路給容器。（ 建議 google 一下 overlay network :smirk: ）

* Load balancing

    你可以將服務的 ports 暴露給外部 Load balancer。在內部，swarm 讓你可以在節點之間指定如何分配服務。

* Secure by default

    在 swarm 中，每一個節點強制使用 TLS 互相認證和加密，用來保護自己以及和其他節點的溝通。你也可以選擇使用自己定義的 certificates。

* Rolling updates

    swarm manager 讓你控制服務佈署到不同的節點之間的延遲，如果出現任何問題，可以 roll-back（ 回滾 ）任務到之前的服務。

### docker swarm 概念

請參考 [https://docs.docker.com/engine/swarm/key-concepts/](https://docs.docker.com/engine/swarm/key-concepts/)

#### Swarm

swarm 是由多個 docker hosts 主機組成，這些 docker hosts 以 swarm mode 運行，角色主要有 manager

（ 管理成員以及指派任務 ）和 work（ 執行 swarm service ）。docker hosts 可以是  managers 或 works，

docker 的工作原理是維持所需的狀態，舉個例子，
假如一個 worker node 崩潰了，docker 會在其他可運

作的 worker 中調用 tasks，tasks 是在 swarm 服務中正在執行的一個容器，
他是由 swarm manager 管理，

而不是一個獨立的容器。

swarm service 相對於獨立的 container 的優勢是可以在不需要手動重新啟動服務的狀態下，修改服務的設

定 ( 包含網路和volumes )。

當 docker 執行在 swarm mode 時，你仍然可以在 docker hosts 上面獨立執行 containers，
獨立的容器和

swarm services 主要的的區別是，swarm services 只有 swarm managers 可以管理群集，而獨立的容器可以

在任何的 daemon
上執行。

#### Nodes

節點是 docker engine 中的一個 instance，你也可以將他視為 docker 的節點。你可以在機器中運行一或多個

節點，通常產品
swarm 佈署會分佈多個 physical computer  和雲端機器的 docker 節點。

當 deploy 一個應用程式到 swarm 時，我們需要定義一個 manager node，這個 manager node 將分配 tasks

給其他的 workers，manager nodes 會選出一個 leader 來編排任務。

 worker 節點收到來自 manager nodes 分派的任務，預設的  manager nodes 也會執行服務（ 如同 wokers ），

 當然，你也可以設定
 manager nodes 只做管理的工作，並成為唯一的管理者，work node 通知 manager node

 目前自己負責的 tasks 的狀態，
 讓 manager 可以維持每個 worker 該負責的任務 （以達到期望的狀態 ）。

#### Services and tasks

服務是在 manager nodes 或 worker nodes 中執行任務的定義。
當你建立一個服務時，你可以指定哪個容器需要

用那個 image 以及需要哪些指令。

在 replicated services 中，swarm manager 會根據節點之間的比例分配特定數量的 replica tasks。

在 global services 中，swarm 在每一個可用的節點中執行一項服務任務。

task 攜帶一個 docker 容器和在容器中執行的命令，當 task 被指派給一個 node 時，他就不能移動到其他的節點。

他只可以執行（ or 失敗 ）在被分派的節點上

#### Load balancing

swarm manager 使用 ingress load balancing 來 expose 你想要在群集外的服務。
swarm manager 可以自動指定服

務一個 PublishedPort 或者你可以設定他，
如果你沒有指定 port，swarm manager 將分配一個 30000-32767 之間的

port 給他。

swarm 模式有一個內部的 DNS 元件，可以自動為群集中每一個服務分配一個  DNS entry，
swarm manager 使用內部

的 load balancing 去分配服務之間的請求。

#### How nodes work

docker swarm 中，主要的就是 **managers** and **workers**

![](https://i.imgur.com/pF1zdad.png)

請可參考 [https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)

#### How services work

請參考 [https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/](https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/)

### docker swarm 基礎篇

* [Youtube Tutorial PART 3 - Docker Swarm 建立 - 基礎篇](https://youtu.be/q2V3ZT5NdNo)

先建立三台 machine ( vm1 , vm2 , vm3 )

![](https://i.imgur.com/tko77BZ.png)

這邊拿 vm1 當作 manager ( ip 為 `192.168.1.107` )

先 ssh 進去 vm1

```cmd
docker-machine ssh vm1
```

接著初始化 docker swarm

```cmd
docker swarm init --advertise-addr 192.168.1.107
```

![](https://i.imgur.com/wH5H51l.png)

A 的部分告訴你 vm1 是 manager，

B 的部分則是增加一個 worker 到 swarm 中的指令。

```cmd
docker swarm join --token SWMTKN-1-5ixph5gyd5gj51jg1749d4c6mms31kdnzcpji5c2yz4ke95rdw-2o9ias3hkslk29ph08wa3seon 192.168.1.107:2377
```

到 machine vm2 執行

![](https://i.imgur.com/Kf8a59i.png)

到 machine vm3 執行

![](https://i.imgur.com/sajS4pN.png)

更多 docker swarm init 可參考 [https://docs.docker.com/engine/reference/commandline/swarm_init/](https://docs.docker.com/engine/reference/commandline/swarm_init/)

接下來回到 vm1 ( manager ) ，使用以下指令查看 swarm 中的 node

```cmd
docker node ls
```

![](https://i.imgur.com/QQFduc7.png)

從上圖中可以發現 vm1 是 Leader

可參考 [https://docs.docker.com/engine/reference/commandline/node_ls/](https://docs.docker.com/engine/reference/commandline/node_ls/)

到這邊基本上就完成了，我們可以開始建立服務。

## docker service

* [Youtube Tutorial PART 3 - Deploy Services to a Swarm 教學](xxxxx)

接下來我們先用 `docker service` 來玩玩 `docker swarm`

詳細可參考 [https://docs.docker.com/engine/swarm/services/](https://docs.docker.com/engine/swarm/services/)

先 ssh 到 vm1 ( manager )

建立 service

```cmd
docker service create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

範例

```cmd
docker service create --name=my_nginx nginx
```

`--name`，service 的名稱

![](https://i.imgur.com/AplY3vq.png)

`--detach` 如果設定為 false ，則會在 foreground ( 前景 ) 執行，

沒特別指定，就是在背景執行，如下方

```cmd
docker service create --detach=false nginx
```

![](https://i.imgur.com/eThAZPt.png)

可參考 [https://docs.docker.com/engine/reference/commandline/service_create/](https://docs.docker.com/engine/reference/commandline/service_create/)

接著查看 service

```cmd
docker service ls [OPTIONS]
```

![](https://i.imgur.com/Cfe56ZI.png)

可參考 [https://docs.docker.com/engine/reference/commandline/service_ls/](https://docs.docker.com/engine/reference/commandline/service_ls/)

更新 service

```cmd
docker service update [OPTIONS] SERVICE
```

範例 ( 將剛剛的範例增加 published port )

```cmd
docker service update --publish-add 80 my_nginx
```

![](https://i.imgur.com/GL7FNuo.png)

可以使用 `docker service ls`查看

![](https://i.imgur.com/tOSYgN2.png)

這時候可以試著瀏覽 [http://192.168.1.107:30000/](http://192.168.1.107:30000/)，應該能成功看到畫面:kissing_smiling_eyes:

![](https://i.imgur.com/ds9fmas.png)

可參考 [https://docs.docker.com/engine/reference/commandline/service_update/](https://docs.docker.com/engine/reference/commandline/service_update/)

docker service scale

```cmd
docker service scale SERVICE=REPLICAS [SERVICE=REPLICAS...]
```

範例 ( 將 my_nginx scale=5 )

```cmd
docker service scale my_nginx=5
```

![](https://i.imgur.com/g0YG7RZ.png)

有注意到 REPLICAS 的地方嗎 ? 為什麼會從 2/5 -> 5/5，因為他是在背景執行。

如果我們想停止 service，也可以將 scale 設定為 0

```cmd
docker service scale my_nginx=0
```

可參考 [https://docs.docker.com/engine/reference/commandline/service_scale/](https://docs.docker.com/engine/reference/commandline/service_scale/)

查看 service 的任務狀態 ( List the tasks of one or more services )

```cmd
docker service ps [OPTIONS] SERVICE [SERVICE...]
```

範例

```cmd
docker service ps my_nginx
```

![](https://i.imgur.com/3LtLVZR.png)

注意那個 NODE，指的是這些 service 分別分散部署到不同的 node ( machine )

可參考 [https://docs.docker.com/engine/reference/commandline/service_ps/](https://docs.docker.com/engine/reference/commandline/service_ps/)

查看 service 的詳細資料

```cmd
docker service inspect [OPTIONS] SERVICE [SERVICE...]
```

範例

```cmd
docker service inspect --pretty my_nginx
```

`--pretty`，更適合閱讀

![](https://i.imgur.com/HNlP4Fd.png)

可參考 [https://docs.docker.com/engine/reference/commandline/service_inspect/](https://docs.docker.com/engine/reference/commandline/service_inspect/)

刪除 service

```cmd
docker service rm SERVICE [SERVICE...]
```

查看 service 的 log

```cmd
docker service logs [OPTIONS] SERVICE|TASK
```

```cmd
docker service logs -f my_nginx
```

![](https://i.imgur.com/7JWrASF.png)

他會自己做 Loan Balance，這邊都是分到 vm3 上 :wink:

可參考 [https://docs.docker.com/engine/reference/commandline/service_logs/](https://docs.docker.com/engine/reference/commandline/service_logs/)

## Docker Swarm Visualizer

* [Youtube Tutorial PART 4 - Docker Swarm Visualizer 教學](xxxxx)

接下來推薦大家一個套件 [Docker Swarm Visualizer](https://github.com/ManoMarks/docker-swarm-visualizer)，

顧名思義，他就是可以將 Docker Swarm 視覺化。

run in a docker swarm

```cmd
docker service create --name=viz --publish=8080:8080/tcp --constraint=node.role==manager --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer
```

這時候可以試著瀏覽 [http://192.168.1.107:8080/](http://192.168.1.107:8080/)，應該會看到類似的圖

![](https://i.imgur.com/2wJdVjS.png)

可以發現 6 個 service 服務平均分散到每個 machine 裡面。

## 執行環境

* Mac
* Python 3.6.2
* windows 10

## Reference

* [https://docs.docker.com/](https://docs.docker.com/)
* [docker-swarm-visualizer](https://github.com/ManoMarks/docker-swarm-visualizer)

## License

MIT license
