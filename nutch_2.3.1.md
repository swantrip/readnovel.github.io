# Nutch2.3.1源码开发环境搭建

## 源码下载
下载地址：http://nutch.apache.org/downloads.html 
解压后得到目录apache-nutch-2.3.1，进入该目录。

## 修改配置文件
修改配置文件conf/nutch-site.xml:

   <!-- Put site-specific property overrides in this file. -->

    <configuration>
    
    	<!--此参数主要用于在IDE环境开发模式运行，在构建输出的runtime部署运行请注释或删除此项参数-->
    	<!-- Just for development, please remove this plugin.folders for production env -->
        <property>
            <name>plugin.folders</name>
            <value>./src/plugin</value>
        </property>

        <!--基于gora的爬虫数据底层存储机制，-->
        <!--官方文档及推荐为HBase，本项目默认配置为MongoDB。需要同步配置gora.properties文件中相关参数。-->
        <property>
                <name>storage.data.store.class</name>
                <value>org.apache.gora.mongodb.store.MongoStore</value>
                <description>Default class for storing data</description>
        </property>

        <property>
                <name>http.agent.name</name>
                <value>Your Nutch Spider</value>
        </property>
	</configuration>
	
	
修改ivy/ivy.xml文件 取消mongodb注释:

` <!-- Uncomment this to use MongoDB as Gora backend. -->    
<dependency org="org.apache.gora" name="gora-mongodb" rev="0.6.1" conf="*->default" /> `

修改conf/gora.properties文件配置mongodb:

`############################
# MongoDBStore properties  #
############################
gora.datastore.default=org.apache.gora.mongodb.store.MongoStore
gora.mongodb.override_hadoop_configuration=false
gora.mongodb.mapping.file=/gora-mongodb-mapping.xml
gora.mongodb.servers=localhost:27017
gora.mongodb.db=nutchFocuse
#gora.mongodb.login=login
#gora.mongodb.secret=secret`


编译项目 导入


 