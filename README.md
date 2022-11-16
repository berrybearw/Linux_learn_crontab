# Linux_learn_crontab
排程 crontab 簡介

參考 : [https://ubuntuqa.com/zh-tw/article/10392.html](https://ubuntuqa.com/zh-tw/article/10392.html)

設定一個定時啟動程序
---

- 簡介

```bash
情境 : 寫一支一直檢查 系統狀況程序 
然後想設定 何時才檢查
那麼可以用 Linux 提供的設置 crontab 
登入 用戶後
輸入 crontab -e 
( 預設是 vi 編輯器 )
開始編輯吧 
```

- 常用

```
crontab -l 查看自己的 crontab

crontab -u 名稱 -l 顯示特定使用者 crontab

crontab -e 編輯 crontab

crontab -u 名稱 -e 編輯特定使用者 crontab

crontab -r 刪除全部的 crontab
```

- 範例

```bash
#every 3 minute run abc015
*/3 * * * * . /u1/etc/chenv 2; sh abc015 >>/u1/123/app/4xx/abc015_log.log 2>&1

#日期寫log
"/u1/123/app/4xx/$(date +"\%Y\%m\%d")_abc015.log" 2>&1

#每小時執行程式
* */1 * * * . /u1/etc/chenv 2; sh abc022 >> "/u6/123/sync_tmp/abc022_log/$(date +"\%Y\%m\%d")_abc022.log" 2>&1
```

- 其他設定介紹

![image](https://user-images.githubusercontent.com/96226780/202190474-582f9878-505c-421b-9f0d-52c856cb9b72.png)

![image](https://user-images.githubusercontent.com/96226780/202190507-af496c80-f9ae-44f2-878f-ac79615a8f96.png) 
    
![image](https://user-images.githubusercontent.com/96226780/202190584-e57199c2-14b8-4c05-a014-6be60d546ea9.png)
   
排程更新
---

```bash
ex - /var/spool/cron/root <<%%
a
*/1 * * * * sh /u3/bin/abc.sh
.
wq!
%%
```

排程執行目錄
---
    
登入 root 查看 
    
/var/log/cron
    
![image](https://user-images.githubusercontent.com/96226780/202191423-dd4675c3-d985-4839-a829-30738f071719.png)

搜尋想找的程序名稱 , 會看到幾點有運行

![image](https://user-images.githubusercontent.com/96226780/202191462-adabed4b-2fab-4879-bcf4-14285b545446.png)
    

除了⼀般使⽤者各⾃的排程⼯作之外，

還有⼀類的是屬於系統的排程⼯作，這類的設定寫在

/etc/crontab 檔案與 /etc/cron.d/ ⽬錄下的各個設定檔

多了⼀個使⽤者名稱

![image](https://user-images.githubusercontent.com/96226780/202193059-c4035a2a-4053-4bac-ba56-b6b5055b64ce.png)


限制使⽤者使⽤ crontab
---

```
系統安全性的考量，限制只有特定的使⽤者可以使⽤ crontab ，
可以透過系統的 /etc/cron.allow 或 /etc/cron.deny 兩個檔案來設定。
/etc/cron.allow
這個檔案存在，則只有被列在這裡的帳號可以使⽤ crontab ，其餘帳號皆禁⽌使⽤，
也就是⽩名單。
/etc/cron.deny
如果這個檔案存在，則被列在這裡的使⽤者都禁⽌使⽤ crontab ，也就是⿊名單。
/etc/cron.allow 與 /etc/cron.deny 設定檔在列出帳號時，語法都相同，每⼀⾏寫⼀個帳號名稱。
如果 /etc/cron.allow 與 /etc/cron.deny 兩個設定檔都不存在，則就只有系統管理者
root 能夠使⽤ crontab
```
