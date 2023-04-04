# 確認項目  
## ①APサーバーの名前とバージョン  
```  
$ ps aux | grep -i 'puma\|unicorn\|webrick\|thin'  
```  
をたたき、  
```  
ec2-user 11356  0.3 11.5 976108 115232 pts/4   Sl+  03:40   0:01 puma 5.6.5 (tcp://0.0.0.0:8080) [raisetech-live8-sample-app]
ec2-user 15699  0.0  0.0 119428   912 pts/6    S+   03:49   0:00 grep --color=auto -i puma\|unicorn\|webrick\|thin
```  
との結果が表示されたことから、  
>APサーバの名前：puma  
APサーバのVersion：5.6.5  
  
と判断。  

## ②サンプルアプリケーションで使った DB サーバー（DB エンジン）の名前と、今 Cloud9 で動作しているバージョン  
raisetech-live8-sample-app/database.ymlに  
![スクリーンショット (512).png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3276773/57416265-d1a1-add3-743e-16df46ce3bd9.png)
と記述されており、また  
```  
$ mysql --version
```  
のコマンドからの結果で  
```
mysql  Ver 8.0.32 for Linux on x86_64 (MySQL Community Server - GPL)  
```  
との結果が得られたことから、  
>DBサーバの名前：MySQL  
DBサーバのVersion：8.2.32  
  
と判断。  

## ③Rails の構成管理ツールの名前  
使用している構成管理ツールはBundlerで
```  
$ bundle -v  
```  
の入力で　　
```  
Bundler version 2.3.14
```  
が得られる。
>構成管理ツールの名前：Bundler    
構成管理ツールのVersion：2.3.14  

## ④サーバを終了させた際のアクセスの可否  
変更前  
![スクリーンショット (515).png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3276773/6e53cc28-361e-3e1d-e6ea-9ed6d8fbeb9f.png)  

APサーバを停止させた場合  
![スクリーンショット (514).png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3276773/25f315b7-1ab1-8f1d-ef60-6754a3df0aff.png)  
上記の画面に変化。  

DBサーバを停止させた場合  
![スクリーンショット (513).png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3276773/e5fb2cf3-151f-438e-aae0-5a9e5d2db92f.png)
上記の画面に変化。以下再起動のために使用したコマンド  
```  
$ sudo service mysqld stop //MySQLの停止
$ sudo service mysqld start //MySQLの起動
```  

以上からどちらかでもサーバが停止するとアクセス不可となるが、再起動により元通りにアクセス可能となった。
