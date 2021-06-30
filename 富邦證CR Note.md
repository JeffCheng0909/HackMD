# 富邦證CR Note

### JSP表單傳送

```
//方法1:

表頭
<s:form id="form" name="action_form" method="post" action="query.action">

表尾
<input class="button" type="button" id="viewPage" value="瀏覽" onclick="this.form.submit()" >
```

```
//方法2:

表頭
<s:form id="form" name="action_form" method="post">

表尾
<input class="button" type="button" id="viewPage" value="瀏覽" onclick="javascript:goTest();" >

函式 (onclick後經由函式傳出)
function goTest()
{
    document.action_form.action=contextPath+"/PLEH001/query.action";
    document.action_form.submit();
}

```
```
//onclick帶參數:

<div class="table">
    <display:table id="viewObj" name="requestScope.codeset2List" class="default" pagesize="15" requestURI="/zgl1100/view.action">
        <display:column property="pk01" titleKey="gl.zgl1100.companyCode" sortable="true" />
        <display:column property="pk02" titleKey="gl.zgl1100.depCode" sortable="true" />
        <display:column property="pk03" titleKey="gl.zgl1100.seqCode" sortable="true" />
        <display:column property="txt1" titleKey="gl.zgl1100.top2Code" sortable="false" />
        <display:column class="last" titleKey="label.common.function">
            <input class="button" type="button" value="<s:text name="button.edit" />" onclick="updData('${viewObj.pk01}', '${viewObj.pk02}','${viewObj.pk03}','${viewObj.txt1}');" >
            <input class="button" type="button" value="<s:text name="button.delete" />" onclick="delData('${viewObj.pk01}', '${viewObj.pk02}','${viewObj.pk03}','${viewObj.txt1}');" >
        </display:column>
    </display:table>
</div>


//$("#detailType")設定到Form表單內相對應的ID，經由action_form傳出
function updData(_pk01, _pk02, _pk03, _txt1)
{
    $("#detailType").val("update");
    $("#detailPk01").val(_pk01);
    $("#detailPk02").val(_pk02);
    $("#detailPk03").val(_pk03);
    $("#detailTxt1").val(_txt1);
    document.action_form.action=contextPath+"/zgl1100/toQuery.action";
    loadingscreen();
    document.action_form.submit();
}
```

### 專題Form表單
```
<FORM METHOD="post" ACTION="<%=request.getContextPath()%>/backend/emp/emp.do" name="form1" enctype="multipart/form-data">

<button class="btn btn-primary" type="submit" name="action" value="insert">送出新增</button> 

```

### 傳值

```
//Controller取用

JSP 整張表單送出，不管是使用

<s:form id="form" name="action_form" method="post" action="query.action">

或

function goUpdate()
{
    $("#detailType").val("create");
    $("#detailPk01").val($("#bu").val());
    $("#detailPk02").val($("#depId").val());
    document.action_form.action=contextPath+"/zgl1100/toQuery.action";
    loadingscreen();
    document.action_form.submit();

(註:$("#detailType")會放入form裡面宣告的hidden，再經由action_form帶出去)
(*註:Function內的值可經由form裡面的hidden/non-hidden id帶出去，好用!!)
}

JSP頁面的值只要name = "dateTest" 和 Controller上方一樣(private String dateTest;)

*在送出表單之後，值會自動放入Controller上方，即可在Controller直接拿來用。


(注意:前提必須要有getter/setter存在)



<s:form name="action_form" method="post">
<div class="table">
    <s:hidden id="selectBu" name="selectBu"/>
    <s:hidden id="selectDepId" name="selectDepId"/>
    <s:hidden id="detailPk01" name="detailPk01"/>
    <s:hidden id="detailPk02" name="detailPk02"/>
    <s:hidden id="detailPk03" name="detailPk03"/>
    <s:hidden id="detailTxt1" name="detailTxt1"/>
    <s:hidden id="detailType" name="detailType"/>
```

```
//View取用

*JSP頁面上，只要name和Controller上方的private變數一樣，就可直接抓Controller的值取來用。
(可以在Controller對於傳進來要出去的值動手腳，本來傳入1改成100)
```

```
//Obj特殊用法

view.jsp:
name="pageObj.busType" 在view像是set進去


Controller:
private VoucherSelectPage pageObj;

要使用必須再get出來
pageObj.getBusType();


query.jsp:
name="pageObj.busType"  在query像是get出來顯示
```

```
//JSP頁面取值寫法

皆可取值:
<tr><td><s:property value="%{pageObj.busType}" /></td></tr>
<tr><td><s:property value="pageObj.busType" /></td></tr>			
<tr><td><s:text name="%{pageObj.busType}"/></td></tr>
<tr><td><s:text name="pageObj.busType"/></td></tr>
<tr><td><s:text name="test"/></td></tr>

```

### 調用方法原理
```
同一個class內，兩個不同方法，可直接在A方法內調用B方法，不用new新物件。
(non-static 調用 non-static/static)


public class PLEH001Action extends ASIAction
{

    public String[] getLicenseList() {
        return licenseList;
    }


    public String query() throws Exception {
        String[] bbb = getLicenseList();
    }

}
```
```
public class Method {

    public void run(){
        System.out.println("run");
    }

    public void sport(){
        run();
    }
   
}
```
```
public class Method {

    public void run() {
        System.out.println("run");
    }


    class Method2 {

        public void sport() {
            run();    
        }   
    }
    
}
```

> 出現Mapper Register Error，可能是1.部署檔未註冊 2.DB連線設定問題 3.Mapper.xml內容有誤


### 部署檔
```

tableNameMapper


listKey= cloumn name
listValue= cloumn name


properites需在struts.xml註冊


mapper需在configFIS.xml、configSunData.xml等(連DB部屬檔)註冊





AcntServiceHelper
String table = companyRef + "_JNL_DEFN";

(Table name = Acnt ; Class name = Acnt)



var list = $('#busTypes1 option:selected').val();
```
### DB連線
```
當要連接多個不同DB時，需注意ServiceHelper連線設定getSessionXXX();

//ConnectionFactory
SqlSession session = ConnectionFactory.getSessionSunData().openSession();
```
### 多個Table Join
```
Table aaa (ABCD欄位)
Table bbb (DEFG欄位)
Table ccc (GHIJ欄位)

1.選一個主要的Mapper.xml(aaa)，將三個Mapper.xml所有欄位都加入，並剔除重複的(ABCDEFGHIJ)，放在同一個 
<resultMap id="BaseResultMap" type="com.asi.voucher.models.Search" >裡面。

加入新增SQL語法EX: Select ABCDEFGHIJ From aaa Join bbb、ccc Table。

2.在aaaMapper加入新增的method

3.建立一個新的class，放入所有三個table所有欄位並剔除重複的(ABCDEFGHIJ)。
```
### Mapper.xml取值
```
//將要傳遞的參數包在一個類裡面(Gen出來的那個類)

JnlDefn class:
private Short uniqueRefMemo;


JnlDefnMapper:
int updateByPrimaryKey(JnlDefn record);


JnlDefnMapper.xml:
UNIQUE_REF_MEMO = #{record.uniqueRefMemo,jdbcType=SMALLINT}
```
### 傳參數進Mapper寫法(XXX_JNL_DEFN)
```
//Service
    public List<JnlDefn> listAll(String copmanyRef) throws ServiceException
    {
        return helper.listAll(copmanyRef);
    }

//ServiceHelper
    public List<JnlDefn> listAll(String companyRef) throws ServiceException
    {
        SqlSession session = ConnectionFactory.getSession(DataSourceConstant.SunSystemsData)
                .openSession();
        List<JnlDefn> returnList = null;
        String table = companyRef + "_JNL_DEFN";

        try
        {
            JnlDefnMapper mapper = session.getMapper(JnlDefnMapper.class);
            returnList = mapper.selectByAll(table);
        }
        finally
        {
            session.close();
        }
        return returnList;
    }
}

//Mapper
    List<JnlDefn> selectByAll(@Param("table")
    String table);

//Mapper.xml
 <select id="selectByAll" resultMap="BaseResultMap" parameterType="java.lang.String"  >
    select
   	<include refid="Base_Column_List" />
    from ${table}
    order by JOURNAL_TYPE
  </select>


#注意ServiceHelper & Mapper的傳遞參數排列順序要一致，否則會傳值錯誤。


#{}與${}的區別:
#{}拿到值之後，拼裝sql，會自動對值添加引號”
#{}看到SQL指令會是問號
${}則把拿到的值直接拼裝進sql，如果需要加單引號”，必須手動添加，一般用於動態傳入表名或字段名使用，同時需要添加屬性statementType=”STATEMENT”，使用非預編譯模式STATEMENT。


values (#{busCd,jdbcType=VARCHAR}, #{idNo,jdbcType=VARCHAR}
```
### Param
```
@Param注解

在方法参数的前面写上@Param("参数名")，表示给参数命名，名称就是括号中的内容

public Student select(@Param("aaaa") String name,@Param("bbbb")int class_id);

给入参 String name 命名为aaaa，然后sql语句....where  s_name= #{aaaa} 中就可以根据aaaa得到参数值了。
```
### Select 自訂虛擬欄位
```
//可在Select自訂虛擬欄位，藉由傳入參數，顯示在SQL查詢頁面上。(建立原本不存在的公司別)

SELECT '${paramBusSql}' as busKey, XXX From Table;
```
### 時間轉換
```
java中時間格式要求大小寫嚴格，我們都知道在oracle中時間格式,yyyy-mm-dd 和yyyy-MM-dd 效
果是一樣的,但是在java程式碼中卻是不一樣的。

出現這樣的原因是java中時間格式MM和mm是不一樣的.需要將yyyy-mm-dd改成yyyy-MM-dd。



//時間字串轉成milliseconds or timestamp

        String str = "2021/05/29";
        try {
            DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd");
            Date date = dateFormat.parse(str);
            Timestamp timestamp = new Timestamp(date.getTime());
            System.out.println("milliseconds = "+date.getTime());
            System.out.println("timestamp = ="+timestamp);
        } catch(ParseException e ){
            e.printStackTrace();
        }
```
### 按照IN輸入順序排序
```
WHERE HELD_JNL_NUM IN(286,276,268,271,284,285)

ORDER BY CHARINDEX(cast(HELD_JNL_NUM as VARCHAR(255)), '286,276,268,271,284,285') 
```

### Map
```
//Map放入另外一個Map
queryMap.putAll(tempMap)
```


### BigDecimal
```
#初始宣告必須用new並給初始值

#add之後要重新指向回原本的值

        BigDecimal x = new BigDecimal("0");
        BigDecimal y = new BigDecimal("1");
        BigDecimal z = new BigDecimal("2.22");

        x = x.add(y);
        x = x.add(z);
        System.out.println(x); //3.22

```

### SQL處理金額問題
```
SELECT (SELECT LOC FROM DEPT2 WHERE dept2.deptno = b.deptno),(SELECT DNAME FROM DEPT2 WHERE dept2.deptno = b.deptno),DEPTNO AS F FROM EMP2 B;
```


### JAVA處理金額問題
```
public class Fubon {

    private String no;
    private String name;
    private String amount;

    public String getNo() {
        return no;
    }

    public void setNo(String no) {
        this.no = no;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAmount() {
        return amount;
    }

    public void setAmount(String amount) {
        this.amount = amount;
    }

    public static void main(String[] args) {

        List<Fubon> list = new ArrayList<Fubon>();

        Fubon a = new Fubon();
        a.no="001";
        a.name="Jack";

        Fubon b = new Fubon();
        b.no="002";
        b.name="Tom";
        list.add(a);
        list.add(b);

        List<Fubon> listAdd = new ArrayList<Fubon>();
        Fubon c = new Fubon();
        c.no="001";
        c.amount="777";

        Fubon d = new Fubon();
        d.no="002";
        d.amount="888";

        listAdd.add(c);
        listAdd.add(d);


        for(Fubon y : list){
            for(Fubon z : listAdd){
                if(z.getNo().equals(y.getNo())){
                    y.amount  = z.getAmount();
                }
            }
        }

        for(Fubon x:list){
            System.out.println(x.no);
            System.out.println(x.name);
            System.out.println(x.amount);
        }

```
### IF判斷式長按鈕及表單
```
    <s:if test="%{axs010pfList.size>0}">
        <input id="doSend" name="doSend" class="button" type="button" value="批次過帳"/>
    </s:if>
    
    <s:if test="%{axs010pfList.size>0}">
        <table id="axs010pfListTable" class="bPaginate">
        <thead>
        <tr>
            <th><input type="checkbox" name="chkAll" id="chkAll">全選</th>
            <th><s:text name="lbl.payment.param.ma.companyCode"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.type"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.no"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.period"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.transdate"/></th>
            <th><s:text name="lbl.payment.param.ma.currency"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.postdate"/></th>
            <th><s:text name="label.common.custCode"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.money"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.paymentTerm"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.paymentMethod"/></th>
            <th><s:text name="lbl.receipt.ZAR0100.dueDate"/></th>
            <th><s:text name="label.common.function"/></th>				
        </tr>
```