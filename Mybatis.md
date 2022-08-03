# Mybatis

### 概述
```
是一個框架，對DB table做映射的一個套件

DB a table - Mybatis a.java

Mybatis會產出model & Mapper

主要兩個部分:Example(原生)、自訂

為了因應不同需要，會在Mapper自訂新方法(SQL語句)

Mapper.xml & Mapper.java

盡量用原生的方法，避免欄位修正時需要進去修正，而可以直接重產出Mapper。
```
### 使用資料夾執行
```
generatorConfig_FISSYS_HOTA.xml:

<jdbcConnection driverClass="net.sourceforge.jtds.jdbc.Driver"
    connectionURL="jdbc:jtds:sqlserver://192.168.5.92/FISSYS_HOTA"
    userId="sa"
    password="123456">
</jdbcConnection>
連線資訊  新增新的DB只要改一次

targetPackage  資料路徑(必須要改)

tableName  (必須要改)


generate.bat觸發檔:
generatorConfig_FISSYS_HOTA.xml(要改成資料夾內要GEN的文件名稱)


src file 可以先delete   每次點bat檔之後都會自己生出來
```
```
//兆豐再保

import maven project

download MyBatis Generator 1.4.0

open gereratorConfig.xml and Run as MyBatis Generator

open Gencoder.java and run Run as Java Application
```
### 語法
```
3.撰寫Mybites SQL語法的時候
原符号       <        <=      >       >=       &        '        "
替换符号    &lt;    &lt;=   &gt;    &gt;=   &amp;   &apos;  &quot;

and H.dply_bgn &lt;=  #{DPLY_BGN,jdbcType=TIMESTAMP} 

4.  example例項解析
方法        說明
example.setOrderByClause(“欄位名 ASC”);     添加升序排列條件，DESC為降序
example.setDistinct（假）    去除重複，boolean型，true為選擇不重複的記錄。

條件.andXxxIsNull   新增欄位xxx為null的條件

條件.andXxxIsNotNull     新增欄位xxx不為null的條件

條件。andXxxEqualTo（值）        新增xxx欄位等於value條件

條件。andXxxNotEqualTo（值）  新增xxx欄位不等於value條件

條件.andXxxGreaterThan（值）   新增xxx欄位大於value條件

條件。andXxxGreaterThanOrEqualTo（值）       新增xxx欄位大於等於value條件//

條件。andXxxLessThan（值）      新增xxx欄位小於value條件

條件。andXxxLessThanOrEqualTo（值）     新增xxx欄位小於等於value條件//

條件.andXxxIn（列表<？>） 新增xxx欄位值在List<？>條件

條件.andXxxNotIn（列表<？>）   新增xxx欄位值不在List<？>條件

條件.andXxxLike（“％” + value +“％”）     新增xxx欄位值為value的模糊查詢條件

條件.andXxxNotLike（“％” + value +“％”）       新增xxx欄位值不為value的模糊查詢條件

條件。andXxxBetween（值1，值2）        新增xxx欄位值在value1和value2之間條件

條件。andXxxNotBetween（值1，值2）   新增xxx欄位值不在value1和value2之間
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
```
### Param
```
#{}與${}的區別:
#{}拿到值之後，拼裝sql，會自動對值添加引號”
#{}看到SQL指令會是問號
${}則把拿到的值直接拼裝進sql，如果需要加單引號”，必須手動添加，一般用於動態傳入表名或字段名使用，同時需要添加屬性statementType=”STATEMENT”，使用非預編譯模式STATEMENT。

#{trefernce,jdbcType=VARCHAR}  
${trefernce}  //後面不用寫jdbcType

//有無@Param差別
@Param("record") Aps010pf record
BUS_CODE = #{record.busCode,jdbcType=VARCHAR},   

Aps010pf record
BUS_CODE = #{busCode,jdbcType=VARCHAR}


//只有有寫@Param，就全部都要寫
List<String> selectBeforeEvaluate(@Param("record") Aps010pf record,  @Param("paramenterCode") String paramenterCode); 

//回傳StringList
<select id="selectBeforeEvaluate"
    parameterType="com.asi.bnp.models.Aps010pf" resultType="java.lang.String">
    SELECT LEFT(DOC_NO,5) FROM APS010PF 
    where BUS_CODE = #{record.busCode,jdbcType=VARCHAR}
    and LEFT(DOC_NO,5) = #{paramenterCode,jdbcType=VARCHAR}
</select>
```
### 多個Table Join
```
必須把resultMap都複製到要寫Join的那支xml檔案裡
<resultMap id="acntResultMap" type="com.asi.printsys.syncsys.models.Acnt">
    <result column="ACNT_CODE" property="acntCode" jdbcType="CHAR" />
    <result column="UPDATE_COUNT" property="updateCount" />
    <result column="LAST_CHANGE_USER_ID" property="lastChangeUserId" />
    <result column="LAST_CHANGE_DATETIME" property="lastChangeDateTime" />
    <result column="DESCR" property="descr" />
</resultMap>

<resultMap id="acntAnlCatResultMap" type="com.asi.printsys.syncsys.models.AcntAnlCat">
    <result column="ANL_CAT_ID" property="anlCatId" jdbcType="CHAR" />
    <result column="ACNT_CODE" property="acntCode" jdbcType="CHAR" />
    <result column="UPDATE_COUNT" property="updateCount" />
    <result column="LAST_CHANGE_USER_ID" property="lastChangeUserId" />
    <result column="LAST_CHANGE_DATETIME" property="lastChangeDateTime" />
    <result column="ANL_CODE" property="anlCode" jdbcType="CHAR" />
</resultMap>

```
```
    <select id="getAcntAnlCatListByDto" parameterType="com.asi.printsys.syncsys.dto.AcntSyncDto" resultMap="acntAnlCatResultMap">
        SELECT F99_ACNT_ANL_CAT.ANL_CAT_ID,
            F99_ACNT.ACNT_CODE,
            F99_ACNT.UPDATE_COUNT,
            F99_ACNT.LAST_CHANGE_USER_ID, 
            F99_ACNT.LAST_CHANGE_DATETIME,
            F99_ACNT_ANL_CAT.ANL_CODE,
            F99_ACNT.DESCR 
        FROM F99_ACNT LEFT OUTER JOIN F99_ACNT_ANL_CAT
        ON F99_ACNT.ACNT_CODE = F99_ACNT_ANL_CAT.ACNT_CODE 
        AND F99_ACNT_ANL_CAT.ANL_CAT_ID = '03'
        WHERE ( F99_ACNT.ACNT_CODE BETWEEN #{acntStartId} AND #{acntEndId} )
        AND ( F99_ACNT.LAST_CHANGE_DATETIME BETWEEN #{startDate,jdbcType=TIMESTAMP} 
        AND DATEADD(day, 1, #{endDate,jdbcType=TIMESTAMP}) )
    </select>
```
```
//mapper.xml

<resultMap id="BaseResultMap" type="com.asi.voucher.models.Search" >  表頭

<select id="query" parameterType="com.asi.voucher.models.Search" resultMap="BaseResultMap">  方法
```
### 處理char bug
```
//設定generatorConfig.xml

		<javaModelGenerator
			targetPackage="com.asi.huanan.service.dao.mybatis.model"
			targetProject="mybatis_daos_gen" >
		 <property name="trimStrings" value="true" />	
		</javaModelGenerator>
```
```
    public void setCancelCrossedMark(String cancelCrossedMark) {
        this.cancelCrossedMark = cancelCrossedMark == null ? null : cancelCrossedMark.trim();
    }
```