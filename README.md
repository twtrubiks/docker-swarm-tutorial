# docker-swarm-tutorial

Docker Swarm 基本教學 - 從無到有 Docker-Swarm-Beginners-Guide📝

* [Youtube Tutorial PART 1 - Docker Machine 介紹](https://youtu.be/RSXlK0U-2Bo)
* [Youtube Tutorial PART 2 - Docker Swarm 簡介](https://youtu.be/ir0ApK1rfA4)
* [Youtube Tutorial PART 3 - Docker Swarm 建立 - 基礎篇](https://youtu.be/q2V3ZT5NdNo)
* [Youtube Tutorial PART 4 - Deploy Services to a Swarm - 基礎篇](https://youtu.be/zW8dcez4EPM)
* [Youtube Tutorial PART 5 - Docker Swarm + Django - 實戰篇](https://youtu.be/AeabcmHvSts)
* [Youtube Tutorial PART 6 - Docker Swarm + HAProxy - 實戰篇](https://youtu.be/GaeLgRtiJEc)
* [Youtube Tutorial PART 7 - Docker Swarm Manage sensitive data with Docker secrets - 實戰篇](https://youtu.be/T8mkecPQce4)

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

* [認識 Docker Machine](https://github.com/twtrubiks/docker-swarm-tutorial#docker-machine-%E6%95%99%E5%AD%B8)

* [認識 Docker Swarm](https://github.com/twtrubiks/docker-swarm-tutorial#docker-swarm-%E6%95%99%E5%AD%B8)

* [Deploy Services to a Swarm](https://github.com/twtrubiks/docker-swarm-tutorial#docker-service)

* [認識 Docker Swarm Visualizer](https://github.com/twtrubiks/docker-swarm-tutorial#docker-swarm-visualizer)

* [實戰 Docker Swarm + Django](https://github.com/twtrubiks/docker-swarm-tutorial#docker-swarm--django)

* [Docker Swarm + HAProxy](https://github.com/twtrubiks/docker-swarm-tutorial#docker-swarm--haproxy)

* [Docker Swarm - Manage sensitive data with Docker secrets](https://github.com/twtrubiks/docker-swarm-tutorial#docker-swarm---manage-sensitive-data-with-docker-secrets)

## docker-machine 教學

* [Youtube Tutorial PART 1 - Docker Machine 介紹](https://youtu.be/RSXlK0U-2Bo)

![](https://i.imgur.com/n1QaEcm.png)

可以在本地端練習控制多個虛擬機，等熟悉後，要控制雲端的機器也是一樣的。

### docker-machine 安裝教學

## Docker Toolbox

使用 [Docker Toolbox](https://docs.docker.com/toolbox/overview/) 安裝

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

## 使用指令安裝

詳細安裝教學可參考  [https://docs.docker.com/machine/install-machine/](https://docs.docker.com/machine/install-machine/)

***Windows***

使用 [Git BASH](http://gitforwindows.org/) 執行下列指令 ( 如果你有安裝 git ，通常電腦上都會有 )

```cmd
 if [[ ! -d "$HOME/bin" ]]; then mkdir -p "$HOME/bin"; fi && \
curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" && \
chmod +x "$HOME/bin/docker-machine.exe"
```

***Mac***

```cmd
 curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine && \
  chmod +x /usr/local/bin/docker-machine
```

以上兩種方法我都有使用過，都沒什麼問題:smile:

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

這邊補充一下，

如果你使用 `docker-machine ls` 然後看到類似下面的錯誤訊息

```cmd
Unable to query docker version: Get https://192.168.99.102:2376/v1.15/version: x509: certificate is valid for 192.168.99.105, not 192.168.99.102
```

這時候可以用這個指令修復

```cmd
 docker-machine regenerate-certs [OPTIONS] [arg...]
```

可參考 [https://docs.docker.com/machine/reference/regenerate-certs/](https://docs.docker.com/machine/reference/regenerate-certs/)

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

    swarm manager node 會一直監控 cluster 狀態，保持你所需的狀態。舉個例子，假設你設定一個服務有十個 replicas，其中有一台 worker machine 死了兩個 replicas，swarm manager node 會再指派給可運作的 worker 兩個 replicas，保持服務有十個 replicas（ 保持你所需的狀態 ）。

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
 manager nodes 只做管理的工作，並成為唯一的管理者。

 work node 通知 manager node 目前自己負責的 tasks 的狀態，
 讓 manager 可以維持每個 worker 該負責的任

 務（以達到期望的狀態 ）。

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

#### Raft consensus in swarm mode

當 Docker Engine 執行在 Swarm mode 時，manager nodes 實現 [Raft Consensus Algorithm](http://thesecretlivesofdata.com/raft/)（ 建議觀看 ）來管理

全部的 cluster 的狀態。

假如現在有 A、B、C 三個 manager nodes，並且 A 是 Leader，今天 A 節點因為某種原因失效了，這時候 B、C 兩個

節點會互相選舉，選出一個 Leader 以維持整個系統。

Raft 容忍 `(N-1)/2` 失效，假設 5 個 Manager nodes 中，有 3 個 nodes 失效，雖然正在執行的 tasks 會保持執行，

但整個系統的 scheduler 將失效，也就是無法 balance tasks。

更多請參考 [https://docs.docker.com/engine/swarm/raft/](https://docs.docker.com/engine/swarm/raft/)

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

這邊要再提醒大家一下，注意那個 **To add a worker to this swarm**，

那我如果想要加入其他的 manager 呢:question:

這時候我們可以使用下面的指令

```cmd
docker swarm join-token [OPTIONS] (worker|manager)
```

會顯示 **To add a manager to this swarm**

```cmd
docker swarm join-token manager
```

會顯示 **To add a worker to this swarm**

```cmd
docker swarm join-token worker
```

這邊大家可以自己玩玩看，可以有多個 manager ，但只能有一個 **Leader** !!

更多可參考 [https://docs.docker.com/engine/reference/commandline/swarm_join-token/](https://docs.docker.com/engine/reference/commandline/swarm_join-token/)

到 machine vm2 執行

![](https://i.imgur.com/Kf8a59i.png)

到 machine vm3 執行

![](https://i.imgur.com/sajS4pN.png)

更多 docker swarm init 可參考 [https://docs.docker.com/engine/reference/commandline/swarm_init/](https://docs.docker.com/engine/reference/commandline/swarm_init/)

如果要離開 swarm，可使用

```cmd
docker swarm leave [OPTIONS]
```

可參考 [https://docs.docker.com/engine/reference/commandline/swarm_leave/](https://docs.docker.com/engine/reference/commandline/swarm_leave/)

接下來回到 vm1 ( manager ) ，使用以下指令查看 swarm 中的 node

```cmd
docker node ls
```

![](https://i.imgur.com/QQFduc7.png)

從上圖中可以發現 vm1 是 Leader

可參考 [https://docs.docker.com/engine/reference/commandline/node_ls/](https://docs.docker.com/engine/reference/commandline/node_ls/)

查看 node 詳細資料

```cmd
docker node inspect [OPTIONS] self|NODE [NODE...]
```

可參考 [https://docs.docker.com/engine/reference/commandline/node_inspect/](https://docs.docker.com/engine/reference/commandline/node_inspect/)

移除 node 節點

```cmd
docker node rm [OPTIONS] NODE [NODE...]
```

可參考 [https://docs.docker.com/engine/reference/commandline/node_rm/](https://docs.docker.com/engine/reference/commandline/node_rm/)

這邊要注意的是，當我們移除的 node 是 **manager** 時，你會發現無法移除，

這時候，就必須先 demote 節點，然後才可以刪除

demote 節點

```cmd
docker node demote NODE [NODE...]
```

範例 ( 假設 vm2 是 manager 節點 )，先將 vm2 demote 為 worker，再將他刪除

```cmd
docker node demote vm2
docker node rm -f vm2
```

可參考 [https://docs.docker.com/engine/reference/commandline/node_demote/](https://docs.docker.com/engine/reference/commandline/node_demote/)

既然有 demote ，那一定有 promote

promote 節點

```cmd
docker node promote NODE [NODE...]
```

範例 ( 假設 vm3 是 worker 節點 )，將 vm3 promote 為 manager

```cmd
docker node promote vm3
```

可參考 [https://docs.docker.com/engine/reference/commandline/node_promote/](https://docs.docker.com/engine/reference/commandline/node_promote/)

Update a node

```cmd
docker node update [OPTIONS] NODE
```

詳細參數可參考 [https://docs.docker.com/engine/reference/commandline/node_update/](https://docs.docker.com/engine/reference/commandline/node_update/)

有時候可能某些節點需要進行維護的工作，所以必須先離線，這時候可以透過

`--availability` 這個參數來完成，指令如下

```cmd
docker node update [OPTIONS] NODE
```

舉個例子，vm3 這個節點需要進行維護，將 vm3 drain

```cmd
docker node update --availability drain vm3
```

這時候可以用 `docker node ls` 觀察，會發現他的 AVAILABILITY 變成 Drain 了

![](https://i.imgur.com/J6z9FaF.png)

可以再用 `docker stack ps [OPTIONS] STACK` 去觀察，其他的 node 會去幫被 Drain 的節點做 cover 的動作。

如果 vm3 這個節點維護好了，只需要執行以下指令即可回復

```cmd
docker node update --availability active vm3
```

到這邊基本上就完成了，我們可以開始建立服務 :smile:

## docker service

* [Youtube Tutorial PART 4 - Deploy Services to a Swarm - 基礎篇](https://youtu.be/zW8dcez4EPM)

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

( 這邊特別補充一下，未來的 docker 版本，沒指定都會默認 `--detach=false` )

```cmd
docker service create --detach=false --name my_nginx nginx
```

![](https://i.imgur.com/eThAZPt.png)

也可以寫成

```cmd
docker service create --detach=false --name my_nginx --mode replicated nginx
```

這邊指定了 mode 為 replicated，假如你沒指定，預設為 replicated mode。

可以加上 `-p , --publish`，publish port 給 swarm 之外的 client 端使用。

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

可參考 [https://docs.docker.com/engine/reference/commandline/service_update/](https://docs.docker.com/engine/reference/commandline/service_update/)

如果要更新已經存在的 service，需使用 `--publish-add`，

也可以透過 `--publish-rm` 移除之前 published 的 port。

![](https://i.imgur.com/GL7FNuo.png)

可以使用 `docker service ls`查看

![](https://i.imgur.com/tOSYgN2.png)

這時候可以試著瀏覽 vm2 ( [http://192.168.1.106:30000/](http://192.168.1.106:30000/) ) or vm1 ( [http://192.168.1.107:30000/](http://192.168.1.107:30000/) )

or vm3 ( [http://192.168.1.108:30000/](http://192.168.1.108:30000/) )

( ip 請使用你自己的，你的 ip 應該會和我的不一樣 :expressionless: )

都能成功看到畫面:kissing_smiling_eyes:

![](https://i.imgur.com/ds9fmas.png)

這時候你可能會問，vm2 ( [http://192.168.1.106](http://192.168.1.106) ) 和 vm3 ( [http://192.168.1.108](http://192.168.1.108) ) 裡面沒有任何 container 在執行，

目前只有 vm1 ( [http://192.168.1.107:30000/](http://192.168.1.107:30000/) ) 中有一個 container 在執行，

那為什麼 vm2 和 vm3 也能正常工作 :question:

原因是因為 docker swarm 內建的 Loan Balance +  **Routing Mesh** 幫我們完成了 :open_mouth:

**Routing Mesh** 會將你的 request route 到正在運行的 container 上，可參考下方這張圖

![](https://i.imgur.com/ZwaTYJO.png)

更多的 **Routing Mesh** 可參考官網說明 [https://docs.docker.com/engine/swarm/ingress/](https://docs.docker.com/engine/swarm/ingress/)

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

這邊還是簡單提一下， `scale up` 和 `scale out` 這兩個簡單的名詞:relaxed:

`scale up` 又稱 Vertical Scaling，最常見的就是增加硬體，像是提高 CPU、Ram。

`scale out` 又稱 Horizontal Scaling，可以思考成像 docker swarm 這樣的分散式架構（ 可以無限拓展 ），

通常整體價格會比 `scale up` 低。

相信大家看完下面這張圖會更了解:satisfied:

![](https://i.imgur.com/DM6Bmy9.jpg)

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

接下來推薦大家一個套件 [Docker Swarm Visualizer](https://github.com/ManoMarks/docker-swarm-visualizer)，

顧名思義，他就是可以將 Docker Swarm 視覺化。

run in a docker swarm

```cmd
docker service create --name=viz --publish=8080:8080/tcp --constraint=node.role==manager --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer
```

這時候可以試著瀏覽 [http://192.168.1.107:8080/](http://192.168.1.107:8080/)，應該會看到類似的圖

![](https://i.imgur.com/2wJdVjS.png)

可以發現 6 個 service 分散到每個 machine 裡面。

## Docker Swarm + Django

* [Youtube Tutorial PART 5 - Docker Swarm + Django - 實戰篇](https://youtu.be/AeabcmHvSts)

前面已經用 nginx 帶大家認識 `docker service` 以及 `docker swarm` 了，現在要用 Docker Swarm + Django 來實戰

### 步驟一

首先，要先建立 image，為什麼呢:question: 不是可以使用 build :question:

因為現在要使用 `docker stack` 的方式佈署，而 `docker stack` 強制規定一定要使用 image ，可參考官網 [image-required](https://docs.docker.com/docker-cloud/apps/stack-yaml-reference/#image-required)，

Django 的範例使用之前介紹的 [用 Docker 實戰 Django 以及 Postgre](https://github.com/twtrubiks/docker-tutorial#%E7%94%A8-docker-%E5%AF%A6%E6%88%B0-django-%E4%BB%A5%E5%8F%8A-postgre)

所以先 clone 下來

```cmd
git clone https://github.com/twtrubiks/docker-tutorial.git
```

接著到目錄底下
> cd docker-tutorial`

執行 `docker-compose up`

再開啟另一個 terminal，先使用 `docker ps` 找到正在執行的 web container，

之後就是 commit，可參考下面指令

```cmd
docker commit -m "create" CONTAINER_ID twtrubiks/my_django
```

push image

```cmd
docker push twtrubiks/my_django
```

因為 repo 是 pubilc 的，所以大家可以到這邊查看 [twtrubiks/my_django](https://hub.docker.com/r/twtrubiks/my_django/)，

你可以自己練習操作一遍，或是直接使用我的 image :smirk:

如果你對 `docker push` 不熟，可參考之前的教學 [Docker push image to Docker Hub 教學](https://github.com/twtrubiks/docker-tutorial#docker-registry)。

### 步驟二

建立 `docker-stack.yml`，可參考 [docker-stack.yml](https://github.com/twtrubiks/docker-swarm-tutorial/blob/master/docker-stack.yml)

```yml
version: "3"
services:

  db:
    image: postgres
    environment:
        POSTGRES_PASSWORD: password123
    volumes:
      - db-data:/var/lib/postgresql/data
    ports:
        - "5432:5432"
    networks:
      - backend
    deploy:
      placement:
        constraints: [node.role == manager]

  web:
      image: twtrubiks/my_django
      # volumes:
      #   - api-data:/docker_api
      ports:
        - "8000:8000"
      networks:
        - backend
      depends_on:
        - db
      deploy:
        replicas: 10
        update_config:
          parallelism: 2
        restart_policy:
          condition: on-failure

  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]

networks:
  backend:

volumes:
  db-data:
  # api-data:
```

基本上這個 `docker-stack.yml` 是從 [docker-compose.yml](https://github.com/twtrubiks/docker-tutorial/blob/master/docker-compose.yml) 修改來的，

有注意到嗎？ 已經使用了 [twtrubiks/my_django](https://hub.docker.com/r/twtrubiks/my_django/) 這個剛剛建立出來的 image，

其餘的 `docker-stack.yml` 參數介紹請參考官網 [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)，

這邊基本上都可以找到說明，在頁面上用關鍵字找即可 :relaxed:

### 步驟三

終於可以開始佈署了 :satisfied:

一樣使用三台 machine，vm1 是 Leader

![](https://i.imgur.com/0716ws1.png)

接著 ssh 進去 vm1

![](https://i.imgur.com/CIZyv09.png)

先 clone 一份下來，因為我們需要 `docker-stack.yml`（ 你也可以用其他的方法 ）

```cmd
git clone https://github.com/twtrubiks/docker-swarm-tutorial
```

切換到目錄底下
> cd docker-swarm-tutorial/

![](https://i.imgur.com/0Rot4eX.png)

接著使用 `docker stack deploy` 指令佈署，

```cmd
docker stack deploy --compose-file docker-stack.yml my_app
```

也可以寫成

```cmd
docker stack deploy -c docker-stack.yml my_app
```

`--compose-file` , `-c` 代表 Path to a Compose file

![](https://i.imgur.com/kITmKDl.png)

當使用 `docker service ls` 查看時，可能要等一下:relaxed:

因為每一台機器 ( vm1 vm2 vm3 ) 都需要從 [docker hub](https://hub.docker.com/) pull image 下來，

![](https://i.imgur.com/ajhH6TD.png)

更多 `docker stack deploy` 說明，可參考 [https://docs.docker.com/engine/reference/commandline/stack_deploy/](https://docs.docker.com/engine/reference/commandline/stack_deploy/)

這邊補充一下 `docker stack` 的其他指令

List stacks

```cmd
docker stack ls
```

可參考 [https://docs.docker.com/engine/reference/commandline/stack_ls/](https://docs.docker.com/engine/reference/commandline/stack_ls/)

List the tasks in the stack

```cmd
docker stack ps [OPTIONS] STACK
```

可參考 [https://docs.docker.com/engine/reference/commandline/stack_ps/](https://docs.docker.com/engine/reference/commandline/stack_ps/)

Remove one or more stacks

```cmd
docker stack rm STACK [STACK...]
```

可參考 [https://docs.docker.com/engine/reference/commandline/stack_rm/](https://docs.docker.com/engine/reference/commandline/stack_rm/)

List the services in the stack

```cmd
docker stack services [OPTIONS] STACK
```

可參考 [https://docs.docker.com/engine/reference/commandline/stack_services/](https://docs.docker.com/engine/reference/commandline/stack_services/)

接下來就是 migrate，隨便進去一個 web service 的 container migrate 即可，使用的指令如下，

先查看 container id，並且進入 container

```cmd
docker ps
docker exec -it <Container ID> bash
```

![](https://i.imgur.com/daIIFT0.png)

開始 migrate

```cmd
python manage.py makemigrations musics
python manage.py migrate
```

![](https://i.imgur.com/5YkmSqQ.png)

再建立一個 superuser

```cmd
python manage.py createsuperuser
```

![](https://i.imgur.com/BVzF9mk.png)

到這邊就完成了:smiley:

以我的範例可以瀏覽 [http://192.168.1.105:8000/api/music/](http://192.168.1.105:8000/api/music/) 或

[http://192.168.1.106:8000/api/music/](http://192.168.1.106:8000/api/music/) 或 [http://192.168.1.107:8000/api/music/](http://192.168.1.107:8000/api/music/)

都可以順利看到 :satisfied:

![](https://i.imgur.com/yXRmthx.png)

port 8080 則是 Docker Swarm Visualizer ，瀏覽 [http://192.168.1.105:8080](http://192.168.1.105:8080) 或

[http://192.168.1.106:8080](http://192.168.1.106:8080) 或 [http://192.168.1.107:8080](http://192.168.1.107:8080)

![](https://i.imgur.com/AoEMe4O.png)

雖然一切看起來美好，但有個小缺點，假設我將 vm3 ( [192.168.1.107](192.168.1.107) )  關機（或是因為其他原因這台機器掛了），

然後去瀏覽 [http://192.168.1.107:8000/api/music/](http://192.168.1.107:8000/api/music/) ，你會發現連不進去 :sob:

你總不可能叫使用者改連 [http://192.168.1.105:8000/api/music/](http://192.168.1.105:8000/api/music/) 或 [http://192.168.1.106:8000/api/music/](http://192.168.99.106:8000/api/music/)，

不被打飛才怪 :rage:

所以這時候我們還需要一個 **外部** 的 **load balancer** !!

load balancer 之前也有介紹過，那時候是使用 nginx 介紹的，

可參考 [實戰 Docker + Django + Nginx + uWSGI + Postgres - Load Balance 📝](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-load-balance-tutorial)

我在 [文章](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-load-balance-tutorial#%E5%85%B6%E4%BB%96%E7%9A%84%E8%B2%A0%E8%BC%89%E5%B9%B3%E8%A1%A1) 最後也提到，如果要專注在 load balancer，使用 HAProxy 效果應該會更好，

所以現在，我們就來加上 HAProxy 吧:satisfied:

## Docker Swarm + HAProxy

* [Youtube Tutorial PART 6 - Docker Swarm + HAProxy - 實戰篇](https://youtu.be/GaeLgRtiJEc)

[HAProxy](http://www.haproxy.org/)（ High Availability Proxy ）最常見的用途是提高分散式環境的效能和可靠性，以這個範例，就非常適合使用。

![](https://i.imgur.com/oWLFO83.png)

參考官網 [https://docs.docker.com/engine/swarm/ingress/#using-the-routing-mesh](https://docs.docker.com/engine/swarm/ingress/#using-the-routing-mesh)

注意，這邊是本機中執行，不是在 swarm 中執行了

先切換到 `haproxy-tutorial` 資料夾中
> cd haproxy-tutorial

修改 `haproxy.cfg`，主要是修改成自己的 ip

```cfg
global
        # log /dev/log   local0
        # log /dev/log   local1 notice
        # chroot /var/lib/haproxy
        maxconn 4096
        # user www-data
        # group haproxy
        daemon

defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        retries 3
        option redispatch
        maxconn 2000
        contimeout     5000
        clitimeout     50000
        srvtimeout     50000

# Configure HAProxy to listen on port 80
frontend http_front
   bind *:80
   stats uri /haproxy?stats
   default_backend http_back

# Configure HAProxy to route requests to swarm nodes on port 8000
backend http_back
   balance roundrobin
   server node1 192.168.1.105:8000 check
   server node2 192.168.1.106:8000 check
   server node3 192.168.1.107:8000 check
```

`haproxy.cfg` 的設定真的很多，詳細可以參考 [官網](http://www.haproxy.org/) 說明

接著 build image

```cmd
docker build -t my-haproxy .
```

![](https://i.imgur.com/yd8Ljgd.png)

將他執行起來

```cmd
docker run -p 8080:80  my-haproxy
```

![](https://i.imgur.com/z0g2jQp.png)

當瀏覽 [http://localhost:8080/api/music/](http://localhost:8080/api/music/) 時，就算 vm3 ( 192.168.99.102 )  掛了，我們一樣可以正常使用網頁 :satisfied:

![](https://i.imgur.com/aOiXV3M.png)

HAProxy 會透過 Health Check 檢查是否這台 server 可以處理 request（會將你的 request 導到可以處理的 server 上）

只要還有一台存在，都可以正常使用網頁（不會掛點）。

但也不要開心的太早，雖然有 HAProxy 幫我們處理 load balancer，但是也有可以 HAProxy 那台機器出了問題，

也就是 **單點失效 ( SPOF )  single point of failure**，也就導致整個系統無法運作:scream:

可以使用 HAproxy + **Keepalived** 解決，這部份有機會會再介紹給大家:relaxed:

## Docker Swarm - Manage sensitive data with Docker secrets

* [Youtube Tutorial PART 7 - Docker Swarm Manage sensitive data with Docker secrets - 實戰篇](https://youtu.be/T8mkecPQce4)

如果你不想將敏感資料存在 image 或者程式碼中，可以使用 docker secrets 來管理容器執行時需要的敏感資料，

像是 passwords、ssl certificates 、ssh private keys ......

思考一個問題，當你有開發機、測試機、正式機，然後每個環境都有不同的密碼，這樣管理 swarm 上會非常麻煩，

這時候可以透過 docker secrets 來管理這些密碼，我們只需要知道 secrets name 就可以在這三個環境上運作。

這邊要注意，`Docker secrets` 只能夠使用在 swarm 下，不能夠使用在獨立的 container 中，

更多介紹，請參考 [Manage sensitive data with Docker secrets](https://docs.docker.com/engine/swarm/secrets/)

其餘的 `Docker secrets` 指令可參考 [https://docs.docker.com/engine/reference/commandline/secret/](https://docs.docker.com/engine/reference/commandline/secret/)

簡單的來實戰一下:smile:

先到 swarm 環境中，假設 vm1 是 manager，先 clone 範例

```cmd
git clone https://github.com/twtrubiks/docker-swarm-tutorial.git
```

接著  `cd docker-swarm-tutorial/docker-swarm-secrets/` 到 [docker-swarm-secrets](https://github.com/twtrubiks/docker-swarm-tutorial/tree/master/docker-swarm-secrets) 資料夾底下，

主要只會用到 [docker-stack.yml](https://github.com/twtrubiks/docker-swarm-tutorial/blob/master/docker-swarm-secrets/docker-stack.yml) 這個檔案，這個範例是從 [Docker 基本教學 - 從無到有 Docker-Beginners-Guide](https://github.com/twtrubiks/docker-tutorial) 修改過來的，

修改了 api/django_rest_framework_tutorial/[settings.py](https://github.com/twtrubiks/docker-swarm-tutorial/blob/master/docker-swarm-secrets/api/django_rest_framework_tutorial/settings.py) 這個檔案，修改如下

```python

def secret_path(name):
    path = '/run/secrets/{}'.format(name)
    if not os.path.isfile(path):
        raise Warning(name)
    return path


def secret(name, strip=True):
    with open(secret_path(name), 'r') as f:
        val = f.read()
        if strip:
            val = val.strip()
        return val


DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': secret('my_password'),
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

目的是去讀取路徑中的 `/run/secrets/<secret_name>` 檔案。（ 我們會將 secrets 名稱設定為 my_password ）。

在 Docker 17.05 或更早的版本，secrets 路徑總是會存在 `/run/secrets/` 資料夾裡，

在 Docker 17.06 之後，可以指定路徑（ 沒指定默認路徑也是 `/run/secrets/` ）。

前面說過了，`docker stack` 強制規定一定要使用 image，這邊大家可以自己 build，然後 push 到 [docker hub](https://hub.docker.com/)，

也可以直接使用我幫大家做好的 [twtrubiks/my_swarm_secrets_demo](https://hub.docker.com/r/twtrubiks/my_swarm_secrets_demo/):wink:

接著來看 [docker-stack.yml](https://github.com/twtrubiks/docker-swarm-tutorial/blob/master/docker-swarm-secrets/docker-stack.yml)

```yml
version: '3.1'
services:

    db:
      image: postgres
      environment:
        POSTGRES_PASSWORD_FILE: /run/secrets/my_password
      ports:
        - "5432:5432"
      networks:
        - backend
      volumes:
        - pgdata:/var/lib/postgresql/data/
      secrets:
        - my_password

    web:
      image: twtrubiks/my_swarm_secrets_demo
      ports:
        - "8000:8000"
      networks:
        - backend
      deploy:
          replicas: 4
          update_config:
              parallelism: 2
          restart_policy:
              condition: on-failure
      secrets:
        - my_password
      depends_on:
        - db

volumes:
    api_data:
    pgdata:

networks:
  backend:

secrets:
    my_password:
        external: true
```

解釋幾個名詞，

版本使用 `3.1` 是避免遇到 secrets Additional property secrets is not allowed 這個錯誤訊息。

`POSTGRES_PASSWORD_FILE` 這個是讀取我們創造的 secrets，

`secrets` 則是指定我們創造的 secrets，這邊還要提一個參數 `external`，

當設定為 `true` 時，代表為外部資源，也就是他已經在 docker 中被定義了，

所以當啟動時，不會再去創造他，如果找不到，則會顯示 `secret not found` 錯誤。

詳細的說明可參考

[https://docs.docker.com/compose/compose-file/#secrets](https://docs.docker.com/compose/compose-file/#secrets)

[https://docs.docker.com/compose/compose-file/#external](https://docs.docker.com/compose/compose-file/#external)

接下來就真的要佈署了:grin:

在 vm1 manager 節點下，先建立 secret

```cmd
echo "password123yoyo" | docker secret create my_password -
```

注意最後面有一個 `-`，代表輸入是從標準輸入讀取的。

密碼你要打多少都可以，因為現在我們只需要知道 secrets name 就可以讀取敏感資訊了。

可以使用 `docker secret ls` 查詢，會看到剛剛建立的 my_password

![](https://i.imgur.com/kPwe1oU.png)

開始佈署

```cmd
docker stack deploy -c docker-stack.yml demo_secret
```

![](https://i.imgur.com/RS93Yfz.png)

執行 `docker stack services demo_secret` 確認佈署狀態，

![](https://i.imgur.com/be6cNyI.png)

確定都佈署完成了之後，

可以執行 `docker stack ps demo_secret` 查看分布在各主機的狀況，

![](https://i.imgur.com/m61tm6s.png)

在這邊我們隨便進入一個 container ，
都可以找到 `/run/secrets/my_password` 這個檔案

（ 原因是因為 `db` 以及 `web` 都有指定 secrets ）

```cmd
cat /run/secrets/my_password
```

![](https://i.imgur.com/4kKxWFn.png)

從上圖可以發現，看到剛剛設定的密碼了:smile:

接下來就是 migrate，隨便進去一個 web service 的 container migrate 即可，使用的指令如下，

先查看 container id，並且進入 container

```cmd
docker ps
docker exec -it <Container ID> bash
```

![](https://i.imgur.com/daIIFT0.png)

開始 migrate

```cmd
python manage.py makemigrations musics
python manage.py migrate
```

![](https://i.imgur.com/5YkmSqQ.png)

再建立一個 superuser

```cmd
python manage.py createsuperuser
```

接下來就可以正常使用了

![](https://i.imgur.com/rxoEkG5.png)

## 執行環境

* Mac
* Python 3.6.2
* windows 10

## Reference

* [https://docs.docker.com/](https://docs.docker.com/)
* [http://www.haproxy.org/](http://www.haproxy.org/)
* [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)
* [docker-swarm-visualizer](https://github.com/ManoMarks/docker-swarm-visualizer)
* [Keepalived](http://www.keepalived.org)

## License

MIT license
