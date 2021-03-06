## 環境準備

### Linux 環境

1. 安裝必要的物件

    ```bash
    sudo apt-get update && sudo apt-get install -y vim python-pip curl git
    pip install docker-compose
    ```
    
2. 安裝 Docker
   
   - 卸載舊版本
        Docker的舊版本為docker，docker.io或docker-engine。如果已安裝，請卸載它們：
        
        ```bash
        sudo apt-get remove docker docker-engine docker.io containerd runc
        ```
           
    - 使用存儲庫安裝
        在新主機上首次安裝Docker Engine之前，需要設置Docker存儲庫。之後就可以從存儲庫安裝和更新Docker。

        - 設置存儲庫
            更新apt軟件包索引並安裝軟件包以允許apt通過HTTPS使用存儲庫：
        
            ```bash
            sudo apt-get update
            ```

            ```bash
            sudo apt-get install \
                apt-transport-https \
                ca-certificates \
                curl \
                gnupg-agent \
                software-properties-common
            ```

        - 添加Docker的官方GPG密鑰：
        
            ```bash
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
            ```

            9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88通過搜索指紋的後8個字符，驗證您現在是否擁有帶有指紋的密鑰 。
        
            ```bash
            sudo apt-key fingerprint 0EBFCD88
            ```
            
            結果應為
            ```
            pub   rsa4096 2017-02-22 [SCEA]
                  9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
            uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
            sub   rsa4096 2017-02-22 [S]
            ```
3. 安裝DOCKER引擎
    - 更新apt程序包索引，並安裝
        - 最新版本的Docker Engine：
    
            ```
            sudo apt-get update
            sudo apt-get install docker-ce docker-ce-cli containerd.io
            ```
        - 安裝特定版本:
            要安裝特定版本的Docker Engine，請在存儲庫中列出可用版本，然後選擇並安裝：
            
            ```bash
            apt-cache madison docker-ce
            ```
            
            應該看到類似如下的表:
            
            ```
            docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
            docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
            docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
            docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
            ...
            ```
            輸入
            
            ```bash
            sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
            ```
            
    - 通過運行hello-world 映像來驗證是否正確安裝了Docker Engine 。
    
        ```bash
        sudo docker run hello-world
        ```
        
        此命令下載測試圖像並在容器中運行它。容器運行時，它會打印參考消息並退出。
         
    詳細步驟參照： [https://docs.docker.com/install/](https://docs.docker.com/install/)

### Windows 環境 (無測試過)


Windows 下的安裝僅供體驗，勿在生產環境使用。如有必要，請使用虛擬機安裝 Linux 並將 OJ 安裝在其中。

以下教程僅適用於 Win10 x64 下的 `PowerShell`

1. 安裝 Windows 的 Docker 工具
2. 右擊右下角 Docker 圖標，選擇 Settings 進行設置
3. 選擇 `Shared Drives` 菜單，之後勾選你想安裝 OJ 的盤符位置（例如勾選D盤），點擊 `Apply`
4. 輸入 Windows 的賬號密碼進行文件共享
5. 安裝 `Python`、`pip`、`git`、`docker-compose`，安裝方法自行搜索。

## 開始安裝

1. 請選擇磁盤空間富餘的位置，運行下面的命令

    ```bash
    git clone -b 2.0 https://github.com/QingdaoU/OnlineJudgeDeploy.git && cd OnlineJudgeDeploy
    ```

2. 啟動服務

    ```bash
    docker-compose up -d  
    ```
    
    - 如果出現
    
        ```
        your_name@ubuntu:~/OnlineJudgeDeploy$ docker-compose up -d
        ERROR: Couldn't connect to Docker daemon at http+docker://localunixsocket - is it running?
        ```
        
        處理方式如下:
        
        - 將當前用戶加入 docker 群組，在【Terminal】中輸入下方指令
            
            ```bash
            sudo gpasswd -a ${USER} docker
            ```
                
         - 退出當前用戶，在【Terminal】中輸入下方指令
                
            ```bash
            sudo su
            ```
            
         - 再次切换到 your_name 用戶，在【Terminal】中輸入下方指令
            
            ```bash
            su your_name
            ```
         - 啟動 docker-compose，在【Terminal】中輸入下方指令
            
            ```bash
            docker-compose up -d
            ```
    
    根據網速情況，大約5到30分鐘就可以自動搭建完成，全程無需人工干預。

    等命令執行完成，然後運行 `docker ps -a`，當看到所有的容器的狀態沒有 `unhealthy` 或 `Exited (x) xxx` 就代表 OJ 已經啟動成功。

## 盡情享用吧

通過瀏覽器訪問服務器的 HTTP 80 端口或者 HTTPS 443 端口，就可以開始使用了。後台管理路徑為`/admin`, 安裝過程中自動添加的超級管理員用戶名為 `root`，密碼為 `rootroot`， **請務必及時修改密碼**。

不要忘記閱讀文檔 http://docs.onlinejudge.me/

## 定制

2.0 版將一些常用設置放到了後台管理中，您可以直接登錄管理後台對系統進行配置，而無需進行代碼改動。

若需要對系統進行修改或二次開發，請參照各模塊的**README**，修改完成後需自行構建Docker鏡像並修改`docker-compose.yml`

## 遇到了問題？

請參照: [http://docs.onlinejudge.me/](http://docs.onlinejudge.me/#/onlinejudge/faq) ，如有其他問題請入群討論或提issue。
