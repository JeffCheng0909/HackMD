# 佈版SOP & 帳密

SVN:
1. 先同步化接著PULL，確認檔案是最新版本Git/SVN
2. 在Eclipse確認該版本的差異檔案，刪除Debug時加入的不必要程式碼
3. COMMIT + PUSH

測試機:
1. 匯出WAR檔(.class)
2. war檔丟過去遠端連線測試機
3. 單支class檔案.zip丟過去測試機
4. 停用jboss
5. 備份原測試機war檔From(jboss\standalone\deployments) To(jboss\standalone\bak)
6. 將抽換檔案備份ZIP放到D:\Asgard\
7. 單支單支程式照路徑替換(D:\jboss-as-.Final.FISSC_IMS\standalone\deployments\)
8. 刪除standalone/tmp資料夾
9. 開啟jboss

//盛餘不丟war檔，丟抽換class檔案.zip過去


> 包版(剔除不要的檔案，包成WAR檔) > 佈版

> 上版流程: SVN > 我們測試機 > 客戶測試環境

### SVN:
1. 右鍵專案 > Team > 與檔案庫同步
2. 右鍵更改檔案名 > 提交


### Git:(小烏龜)
1. 先做pull看是否有他人修改
2. clone下來的資料夾 > 右鍵git commit to XXX
3. 最後commit & push


### Command:
git checkout dev	換你要的線別
git pull	        同步UPDATE
git add	.	        把檔案傳到本地的Repository
git commit	
git log
:wq
<br>

* 差異佈版: 只更新server一部分資料，單支單支程式抽換。
* 整包佈版: 整包全部更換，設定檔除外。(盛餘鋼鐵專案佈版說明)
* 基本上在客戶端佈版都是整包佈版，兆豐跟富邦較特別需差異佈版，並提供差異清單。

### 兆豐門戶通布版
C:\jboss-as-7.1.1.Final.FISSC_IMS\standalone\deployments(要備份的舊檔案) >移動至 C:\share\佈版備份\oldIMS_FinGate(放原始old檔案) 

新的war檔   > C:\share\佈版備份.zip

### 盛餘布版
進入192.168.5.98 
D:\jboss-as-7.1.1.Final\standalone\deployments\FinancialSystem.war

啟動jboss後，資料夾會自動改成dodeploy，有時候沒動的話要自己改。

### 遠端帳密
```
192.168.5.91 遠端帳密(康泰納仕)
帳號 : SunSystemsAdmin
密碼 : eas123456

192.168.5.211 遠端帳密(IMS_FinGate)
帳號 : administrator
密碼 : !@34QWer

192.168.5.98 遠端帳密(盛餘)
帳號 : jim_kuo
密碼 : 123456

```

### 資料庫帳密
```
//MS-SQL
192.168.5.233資料庫帳密(盛餘周邊)
帳號 : sa
密碼 : 123456

192.168.5.98資料庫帳密(盛餘SunAccount、兆豐-門戶通)
帳號 : sa
密碼 : 123456

192.168.5.92資料庫帳密(康泰納仕)
帳號 : sa
密碼 : 123456

192.168.5.241資料庫帳密(兆豐投資SmartQuery)
帳號 : sa
密碼 : 123456


//Oracle
192.168.5.205資料庫帳密(兆豐再保)
Service name : xe
帳號 : ck_rff
密碼 : PAssw0rd

```

### 各客戶資料庫寫入位置
```
-盛餘-
98 : SunSystemsData.dbo.SYS_A_SALFLDG
233 : FISSYS.dbo.PFAP_SALFLDG

-Others-
98 : SunSystemsData.dbo.SYS_A_SALFLDG
98 : FISSYS.dbo.PFAP_SALFLDG

```






