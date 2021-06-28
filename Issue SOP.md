# Issue SOP

### 流程

* Web功能設定找關鍵字，搜尋EX:/syu_payment/zap0170/view.action

1. struts-config.xml (程式進入點說明書Action name & 成功/失敗後轉的網頁地址)
2. actions.java
3. tiles.xml(別名對應真實JSP檔名)
<br>

**按下一個button，會有兩個部分要看**
1. 導頁 struts-config.xml > 導頁說明 tiles.xml
2. 邏輯 action.java
<br>

```
//XXXaction.java
execute() = 按下sidebar button的第一個執行動作，對應//struts-config.xml的最前面區塊，如下:

<package name="syuPaymentZAP0170" namespace="/syu_payment/zap0170" extends="default_setting">
    <action name="view" class="com.asi.apar.actions.Zap0170Action">
        <interceptor-ref name="store">
            <param name="operationMode">RETRIEVE</param>
        </interceptor-ref>
        <interceptor-ref name="asiStack" />
            <result name="success" type="tiles">syu_payment_zap0170.view</result>
    </action>
    
    
    <action name="doQuery" method="doQuery" class="com.asi.apar.actions.Zap0170Action">
        <result name="success" type="tiles">syu_payment_zap0170.view</result>  
        <result name="dataError" type="tiles">syu_payment_zap0170.view</result>
    </action>    
```
```
//到tile.xml找name為syu_payment_zap0170.view 接著看value找明確頁面

    <definition name="syu_payment_zap0170.view" extends="main.common">
        <put-attribute name="body" value="/jsps/apar/payment/zap0170/zap0170Query.jsp" />
    </definition>
```

**寫入DB流程**
```
PfapSalfldg.java、ASalfldg.java = VO 


Zap0260Service = Service

Zap0260ServiceHelper insertDB(); = DAO  (ServiceHelper = dao 對DB作動，開啟/關閉DB連線)


PfapSalfldgMapper *insert(); (對DB作動)

PfapSalfldgMapper.xml    <insert id="*insert" parameterType="com.asi.apar.models.PfapSalfldg" >  (SQL語句)




Zap0250Dto包含 List<ASalfldg> salfldgList、List<PfapSalfldgDto> syuPfapSalfldgList
```




### DB command
JRNAL_TYPE(AR)  >  TREFERENCE(AP202101-0008) 

select*from[SunSystemsData].[dbo].[MED_A_SALFLDG]
where JRNAL_NO=1015

select*from FISSYS.dbo.ASGJournalNumber

FISSYS.dbo.VENDOR

com.asi.apar.dao.mappers.SASalfldgMapper.selectForZap0160-Inline

### Debug mode 不進斷點解法
1. window / Java / Installed JREs / Edit / JRE name: jdk
2. JBoss Tools / Source Lookup / Always
3. 執行dubug時跳出Edit Source Lookup Path 導向當下Java Project