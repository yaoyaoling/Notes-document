* web.config

```xml
<!-- 
	参数配置
	System.Configuration.ConfigurationSettings.AppSettings["key"]; 
	ConfigurationManager.AppSettings["key"].ToString();
-->
<configuration>
    <appSettings>
        <add key="key" value="xxx"/>
    </appSettings>
</configuration>


<!--
	数据库连接字符串(web.config来配置)
  	ConfigurationManager.ConnectionStrings["dbConn"].ToString();
	System.Configuration.ConfigurationManager.ConnectionStrings["dbConn"].ConnectionString;
	System.Web.Configuration.WebConfigurationManager.ConnectionStrings["dbConn"].ToString();
 -->
<connectionStrings>
    <add name="dbConn" connectionString="Data Source=.;Initial Catalog=test;User ID=sa;Password=" providerName="System.Data.SqlClient"/>
</connectionStrings>


 
```

