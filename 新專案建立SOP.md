# 新專案建立SOP

### SVN
* install subclipse (SVN tool from Marketplace)

* install jbossTool (ServerTool from Marketplace)

* 建立專案資料夾

* Jboss copy一包丟入專案資料夾

* 替換standalone.xml檔案 at Jboss File > configuration

* 刪除不必要deployments

* Eclipse右上Open Perspective > 瀏覽SVN檔案庫 > 建立新的SVN檔案庫 > Url > VPN取出為 > 以工作專案方式取出

* 確認JDK版本，專案右鍵 > properties > Libraries > JRE System Library > Edit > Installed JREs > Add > Standard VM > Directory > C:/java/JDKxxx > 改為最下面default選項

* 下方Create new server > Jboss7.1 > 改path為專案Jboss路徑 & Alternate JRE select

* 專案右鍵 > properties > projectFacets > 右邊Runtimes Jboss打勾

* 存在專案匯到Serer > 底下Server右鍵 > Add&Remove > 移到右邊

* Project > Clean

* localhost:8080 or 8081(看standalone.xml http:)/專案名

* http://localhost:8081/FinancialSystem/

* 帳號:asi 密碼:123456

### Git
#### 使用command
* 專案資料夾右鍵 > Git Bash Here >command(git clone 路徑)

* turtle switch checkout to dev

* eclipse匯入

#### 使用小烏龜
* 先至儲存庫管理複製URL (http://svn.asgard.com.tw:8088/Bonobo.Git.Server/ckra.git)

* 建立新資料夾 > 資料夾右鍵gti clone

* 下載完畢後，點開專案資料夾，右鍵 tortosiGit > 選checkout

* eclipse要import Existing Maven Projects


### JDK版本
* 華大成1.7 
* 康泰納仕1.6
* 兆豐FinGate1.7 (Account資訊在FISSC DB)
* 盛餘1.6
* 富邦證1.6



jboss 7.1以上改為WildFly

公司使用WildFly有問題，客戶要用到7.1以上的話要改為Tomcat



### 富邦證note
SVN路徑:
```
https://svn.asgard.com.tw/svn/Sunsystem/
https://svn.asgard.com.tw/svn/Sunsystem/FubonFinancialSystem
https://svn.asgard.com.tw/svn/Sunsystem/fubon/trunk/Schedule
https://svn.asgard.com.tw/svn/Sunsystem/fubon/trunk/FubonSecSystem
https://svn.asgard.com.tw/svn/Sunsystem/SunAccount
https://svn.asgard.com.tw/svn/Sunsystem/fubon/trunk/Settlement


#Settlement localhost與測試機功能選項完全不同   localhost只有資料交換查詢能用

#FubonSecSystem環境架設須注意:
1.Web Deployment Assembly路徑須修正，才會有Web App Library
2.將SunAccount的com所有class複製過來引用
```

### 兆豐再保note
1. 總共要下四個Maven專案，從儲存庫管理抓路徑
* ckra /develop
* asiauth /develop
* asicommon /master
* asicommon4jwt /master

2. 安裝node.js

3. 安裝Help / Eclipse Marketplace / Spring Tools 4

4. ojdbc.zip解壓縮放在 C:\Users\jeff_cheng\.m2\repository\com\oracle

5. 載完之後Maven Update Project  (選Force Update)

6. 更改hosts檔案  C:\Windows\System32\drivers\etc\hosts
```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

192.168.50.170 ckra-ck.apps.ocp45.asgard.com.tw
192.168.50.170 asiauthah-south-china.apps.ocp45.asgard.com.tw
192.168.50.170 console-openshift-console.apps.ocp45.asgard.com.tw
192.168.50.170 oauth-openshift.apps.ocp45.asgard.com.tw
```

7. 在C:\Asgard\Ckra\ckra\src_vue的剪貼路徑上打cmd

8. 執行npm install & 執行npm run build

9. 專案右鍵Run As > Run Configurations > Spring Boot App > asiauth and ckra > Arguments / Program arguments輸入 --spring.profiles.active=dev

10. 啟動按Boot Dashboard，asiauth & ckra兩個專案都要開起來。

11. 登入網址 http://localhost:10201/ckra/login  
帳號:admin 密碼:123456

12. Json報錯處理 / Windows / Preference / Validation / Manual & Build uncheck

13. Pom報錯處理 / 只Project Clean父類 asicommon & asicommon4jwt