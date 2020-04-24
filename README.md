## 環境準備

### Linux 環境

1. 安裝必要的依賴


    sudo apt-get update && sudo apt-get install -y vim python-pip curl git
    
    
    pip install docker-compose

2. 安裝 Docker
    
    
    詳細步驟參照： [https://docs.docker.com/install/](https://docs.docker.com/install/)

### Windows 環境


Windows 下的安裝僅供體驗，勿在生產環境使用。如有必要，請使用虛擬機安裝 Linux 並將 OJ 安裝在其中。

以下教程僅適用於 Win10 x64 下的 `PowerShell`

1. 安裝 Windows 的 Docker 工具
2. 右擊右下角 Docker 圖標，選擇 Settings 進行設置
3. 選擇 `Shared Drives` 菜單，之後勾選你想安裝 OJ 的盤符位置（例如勾選D盤），點擊 `Apply`
4. 輸入 Windows 的賬號密碼進行文件共享
5. 安裝 `Python`、`pip`、`git`、`docker-compose`，安裝方法自行搜索。

## 開始安裝

1. 請選擇磁盤空間富餘的位置，運行下面的命令

    `git clone -b 2.0 https://github.com/QingdaoU/OnlineJudgeDeploy.git && cd OnlineJudgeDeploy`

2. 啟動服務

    `docker-compose up -d`

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
