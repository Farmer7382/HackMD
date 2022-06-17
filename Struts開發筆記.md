# Struts開發筆記

### 提交Form表單
> 在畫面按下doQuery，把畫面的值帶到Controller上方

> Controller的doQuery方法跑完之後，回傳success or error，分別導向不同頁面，並把Controller上方的值再帶到即將導向頁面上。 

> input標籤內的id、name不可與onclick="函數名" 一樣，否則會失效。
```
1.
<s:form id="action_form" name="action_form" method="post" enctype="multipart/form-data" action="doDetail.action">

<input class="button" type="button" onclick="this.form.submit()">

</s:form>

2.

<s:form id="form" name="action_form" method="post">

<button class="bbtn btn-styleE" onclick="enter()">確定</button>

</s:form>

function enter()
{
    document.action_form.action=contextPath+"/ybnp0002/doDetail.action";
    document.action_form.submit();
}

3.
function doCancel() 
{
    $("#actionFormDetail").attr("action", contextPath + "/RS1001/doCancel.action");
    $("#actionFormDetail").submit();
}
```
### 專題Form表單
```
<FORM METHOD="post" ACTION="<%=request.getContextPath()%>/backend/emp/emp.do" name="form1" enctype="multipart/form-data">

<button class="btn btn-primary" type="submit" name="action" value="insert">送出新增</button> 

```
### onclick帶參數傳出
```
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
```
<input class="button" type="button" value="<s:text name="button.edit" />" onclick="toEditPage('${viewObj.busCode}','${viewObj.module}','${viewObj.type}','${viewObj.yearStart}',${viewObj.yyyymmdd});" >

function toEditPage(busCode,module,docType,yearStart,YYYYMMDD)
{
	$("#docgen\\.busCode").val(busCode);
	$("#docgen\\.type").val(docType);
	$("#docgen\\.module").val(module);
	$("#docgen\\.yearStart").val(yearStart);
	$("#docgen\\.yyyymmdd").val(YYYYMMDD);
	
	$("#actionform").attr("action",contextPath+"/docgen/updateView.action");
	loadingscreen();
	$("#actionform").submit();
}
```
### 傳值
> Controller取用
```
JSP 整張表單送出，不管是使用

<s:form id="form" name="action_form" method="post" action="query.action">

或

function goUpdate()
{
    $("#detailType").val("create");
    document.action_form.action=contextPath+"/zgl1100/toQuery.action";
    loadingscreen();
    document.action_form.submit();
}


<s:form name="action_form" method="post">
    <div class="table">
        <s:hidden id="detailType" name="detailType"/>
    </div>    
</s:form>   


$("#detailType")會放入form裡面宣告的hidden，再經由action_form帶出去

Function內的值可經由form裡面的hidden/non-hidden id帶出去，好用!!


JSP頁面的值只要name = "dateTest" 和 Controller上方一樣(private String dateTest;)

在送出表單之後，值會自動放入Controller上方，即可在Controller直接拿來用。

(注意:前提必須要有getter/setter存在)    
```
> View取用
```
JSP頁面上，只要name和Controller上方的private變數一樣，就可直接抓Controller的值取來用。
(可以在Controller對於傳進來要出去的值動手腳，本來傳入1改成100)
```
### Ajax方式傳遞
#### JS原始碼
```
function ajaxRequest(url, param, callback, errorCallback) {
	$.ajax({
		contentType : "application/x-www-form-urlencoded; charset=utf-8",
		type : 'post',
		url : url,
		data : param, //以key-value形式上傳資料給伺服器
		async : false,
		dataType : "json", //從伺服器傳回的資料類型
		success : function(data) {
			callback(data);
		},
		error : function(data) {
			errorCallback(data);
		}
	});
}
```

#### JSP(刪除範例)
```
function del()
{
    var key = selectedData[0].paramenterCode;
    param ={"param" : key};
    ajaxRequest(contextPath+"/ybnp0002/doDelete.action",param,ajaxSuccess,ajaxError);
}
```
#### JSP(自動完成範例)
```
function fetchAcntList()
{
    param = {"buCode" : $("#busCodeSelect").val()};
    ajaxRequest(contextPath+"/ybnp0002/ajaxQueryAcntCode.action",param,ajaxSuccessAcnt,ajaxError);
}

function ajaxSuccessAcnt(data)
{

    for(var index in data.acntCodeList){
        acntCodeLists.push({
            label : data.acntCodeList[index],
            value : data.acntCodeList[index]
        });
    }
  
    $("#exGAcnt").autocomplete({
        source : acntCodeLists,
        delay : 0,
        minlength : 0
    });       
}

function ajaxError()
{
    alert("查詢失敗");
}
```
#### Controller (刪除&自動完成)
```
public class Ybnp0002AjaxAction extends AjaxAction {
	private static final long serialVersionUID = -6069099094588998072L;
	private static Logger logger = LogManager.getLogger(Ybnp0002AjaxAction.class);

	private String param;
	private String buCode;
	private List<String> acntCodeList;
	private List<String> journalTypeList;

	public void doDelete() {
		PrintWriter out = null;
		RevalSetting revalSetting = null;
		Map<String, Object> resultMap = new HashMap<String, Object>();

		try {
			ServletActionContext.getResponse().setCharacterEncoding("utf-8");
			out = ServletActionContext.getResponse().getWriter();

			revalSetting = new RevalSetting();
			revalSetting.setParamenterCode(param);
			int count = RevalSettingService.getInstance().deleteByKey(revalSetting);

			if (count == 1) {
				resultMap.put("msg", "該筆資料已刪除");
			} else {
				resultMap.put("msg", "該筆資料刪除失敗");
			}

		} catch (Exception e) {
			e.printStackTrace();
			logger.error(e.getMessage());
		} finally {
			out.print(JSONObject.fromObject(resultMap));
			out.flush();
		}
	}

	public void ajaxQueryAcntCode() {

		Map<String, Object> resultMap = new HashMap<String, Object>();
		PrintWriter out = null;

		try {
			logger.info("取得AcntCode清單");
			super.servletActionContextInfo();
			out = ServletActionContext.getResponse().getWriter();

			acntCodeList = AcntService.getInstance().queryAllAcntCode(buCode);
			resultMap.put("acntCodeList", acntCodeList);

		} catch (Exception e) {
			e.printStackTrace();
			logger.error(e.getMessage());
		} finally {
			out.print(JSONObject.fromObject(resultMap));
			out.flush();
		}
	}


	public String getParam() {
		return param;
	}

	public void setParam(String param) {
		this.param = param;
	}

	public String getBuCode() {
		return buCode;
	}

	public void setBuCode(String buCode) {
		this.buCode = buCode;
	}

	public List<String> getAcntCodeList() {
		return acntCodeList;
	}

	public void setAcntCodeList(List<String> acntCodeList) {
		this.acntCodeList = acntCodeList;
	}

	public List<String> getJournalTypeList() {
		return journalTypeList;
	}

	public void setJournalTypeList(List<String> journalTypeList) {
		this.journalTypeList = journalTypeList;
	}
}

```
#### JSP(抓table範例)
```
	var tempTable = table.getSelectedData();
	var checkArray = new Array();
	for (var i = 0; i < tempTable.length; i++) {
		checkArray.push([tempTable[i].busCode, tempTable[i].TYPE, tempTable[i].DOC_NO, tempTable[i].TREFERNCE, tempTable[i].DOC_DATE]);
	}

	var param ={
			"checkArray": JSON.stringify(checkArray)
	}
	let checkJournalDateListUrl = contextPath + "/Bnp2021001/checkJournalDateList.action";
	var res = ajaxPostReady(checkJournalDateListUrl,param);
    
    
    if(res[0].checkResult == "ERROR"){
    	$("#notID").show();
		$("#notID").html("單據號:"+res[0].docNo+"傳票日期不一致");
		return;
    }
```
#### Controller (抓table)
```
	public void checkJournalDateList() {
		try {
			ServletActionContext.getResponse().setCharacterEncoding("utf-8");
			PrintWriter out = ServletActionContext.getResponse().getWriter();
			JSONArray json = new JSONArray();

			String checkResult = "PASS";
			String docNo = "";
			JSONArray toBeCheckArray = JSONArray.fromObject(checkArray);
			toBeCheckArray.getJSONArray(0).get(0);
			for (int i = 0; i < toBeCheckArray.size(); i++) {
				Aps020pf aps020pf = new Aps020pf();
				JSONArray tempArray = toBeCheckArray.getJSONArray(i);
				aps020pf.setBusCode(tempArray.getString(0));
				aps020pf.setType(tempArray.getString(1));
				aps020pf.setDocNo(tempArray.getString(2));
				aps020pf.setTrefernce(tempArray.getString(3));
				aps020pf.setDocDate(tempArray.getString(4));
				List<Aps020pf> aps020pfList = Aps020pfService.getInstance().queryByAps020pf(aps020pf);
				Set set = new LinkedHashSet();
				for (Aps020pf element : aps020pfList) {
					set.add(element.getJournalDate());
				}

				if (set.size() != 1) {
					checkResult = "ERROR";
					docNo = aps020pfList.get(0).getDocNo();
				}
				break;
			}

			Map<String, String> resultMap = new LinkedHashMap<>();
			resultMap.put("checkResult", checkResult);
			resultMap.put("docNo", docNo);
			out.print(json.fromObject(resultMap));
		} catch (Exception e) {
			Arrays.asList(e.getStackTrace()).stream().forEach(ex -> logger.debug(ex.toString()));
		}

	}
```

#### Struts-config
```
<action name="doDelete" method="doDelete" class="com.asi.ybnp.actions.Ybnp0002AjaxAction"/>

<action name="ajaxQueryAcntCode" method="ajaxQueryAcntCode" class="com.asi.ybnp.actions.Ybnp0002AjaxAction"/>		

<action name="ajaxQueryJournalType" method="ajaxQueryJournalType" class="com.asi.ybnp.actions.Ybnp0002AjaxAction"/>	
```

### 前端筆記

#### 頁面載入時自動執行
```
1.
$(document).ready(function(){
    do something...
});

2.
$(function(){
    do something...
});
```
#### 事件監控
```
$("#busCodeSelect").change(function(){
    $("#exGAcnt").val("");
    busCode = $("#busCodeSelect").val();
});


$("#parametersCode").on("change", function(){
    var parametersCode = $(this).val();
    if(parametersCode.length!=5){
        alert("請輸入五位數代碼");
        $("#parametersCode").val('');
    }
});
```


#### 引入語法
```
<!--引入外部JS方法-->
<script src="<s:url value="/js/ybnp/ybnp0002.js"/>" type="text/javascript"></script>
```
### 選單標籤
```
1.<s:select>
<td class="field">				
    <s:select id="qryDocgenKey.busCode" list="companyList" listKey="companyref" listValue="companyref+'-'+companyname" name="qryDocgenKey.busCode"></s:select>
</td>
//list可以是model List，companyref、companyname為model內的欄位名
//listKey = 傳到後端
//listValue = 前端畫面顯示


2.<s:textfield>
//<s:標籤>要使用%{exGAcnt}
<div class="tableInp">
    <s:textfield id="exGAcnt" name="exGAcnt" value="%{exGAcnt}"/>
</div>


3.<s:checkboxlist>
//Action設定即可載入頁面選中
<s:checkboxlist name="selectcompany" list="companyList" listKey="companyref" listValue="companyref+'-'+companyname" value="%{selectcompany}"/>

private ArrayList<String> selectcompany;
selectcompany = new ArrayList<>();
selectcompany.add("GAF");
selectcompany.add("CAF");
selectcompany.add("SAF");


4.<s:radio>
//傳radio選中值至Controller & 傳遞Controller至radio選中
<td class="field"><s:radio name="account.status" list="#{'1':'啟用','0':'停用'}" /></td>


5.<c:if>
<c:if test="${flag == 'I'}">
    <option value="">請選擇公司別</option>
</c:if>

<s:if test='#attr.viewObj.status=="U"'>
    已使用
</s:if>

<s:if test="%{axs010pfList.size>0}">
    <input id="doSend" name="doSend" class="button" type="button" value="批次過帳"/>
</s:if>


6.
//disabled會導致後端取不到值，改用readonly
$("#paramenterCode").attr("readonly",true);

$("#paramenterCode").attr("readonly",true);


6.
//屬性是button會導致後端取不到值
<div class="tableInp">

6.
//屬性是button會導致後端取不到值
<div class="tableInp">
    <input type="button" name="txtAcntCode" value="" class="input" onclick="openWindow(this)" id="txtAcntCode">
</div>

解法:
//在form表單內宣告，再重新賦值給新的變數，傳回後端
<s:hidden id="acntCode" name="acntCode"/>

function enter()
{
$("#acntCode").val($("#txtAcntCode").val());

document.action_form.action=contextPath+"/ybnp0002/doDetail.action";
document.action_form.submit();
}


7."${sLedgerList}"可取到後端的List
<select id="sLedgerSelect" class="form-select" aria-label="Default select example">
    <c:forEach var="value" items="${sLedgerList}">
        <option value="${value}">${value}</option>
    </c:forEach>
</select>

7.可顯示後端的String List值
<c:forEach var="value" items="${errorMsg}"> 
  <p>${value}</p> 
</c:forEach> 

7."${description}"可取到後端的值
<div class="tableInp" style="width: 60%; float: left;">
    <input type="text" name="description" value="${description}">
</div>


//JSP頁面取值寫法

皆可取值:
<tr><td><s:property value="%{pageObj.busType}" /></td></tr>
<tr><td><s:property value="pageObj.busType" /></td></tr>			
<tr><td><s:text name="%{pageObj.busType}"/></td></tr>
<tr><td><s:text name="pageObj.busType"/></td></tr>
<tr><td><s:text name="test"/></td></tr>
```
> VO.特殊用法
```
後端:
Account account

account = AccountService.getInstance().query(Integer.parseInt(UserUtil.getUserId()));


Account model:
	private String username;

前端:可用name取到值顯示在畫面上
<s:textfield name="account.username" maxlength="20" size="60" />
```
```
view.jsp:
name="pageObj.busType" 在view像是set進去


Controller:
private VoucherSelectPage pageObj;

要使用必須再get出來
pageObj.getBusType();


query.jsp:
name="pageObj.busType"  在query像是get出來顯示
```
### 定序衝突
```
SELECT A.DESCR,(A.ACNT_CODE collate Chinese_Taiwan_Stroke_CI_AS) AS ACNT_CODE
,A.ACNT_TYPE,B.REM001 
FROM [SunSystemsData].dbo.PK1_ACNT A JOIN [FISBNP].dbo.APS020PF B 
ON (ACNT_CODE collate Chinese_Taiwan_Stroke_CI_AS) = ACCNT_CODE;

ACCNT_CODE 定序為:Chinese_Taiwan_Stroke

ACNT_CODE  定序為:Latin1_General_BIN

將ACNT_CODE 對照為Chinese_Taiwan_Stroke_CI_AS 即可解決
```