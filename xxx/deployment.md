#中转部署结构
支持两种中转的部署结构，当然，不使用中转的情况下，可以全部部署到内部网络。
##方式一：
![](/assets/App中转部署图2.jpg)
App中转方式，如上图，APPserver作为中转服务的客户端，所有客户端连接到中转服务，然后所有的调用请求通过ICE的反向代理转发到对应的APPserver中进行处理。APPserver和ERPserver都部署在企业内网内。

##方式二：
![](/assets/ERP中转部署图2.jpg)
Erp中转方式，如上图，ERPserver作为中转服务的客户端，APPserver通过中转服务，对ERPserver发出调用请求。客户端和APPserver都部署在企业外网，只有ERPserver部署在企业内网。

##中转密钥
通过工具，生成中转密钥 【ForwardKey】文件，密钥内容类似如下：

```
<?xml version="1.0" encoding="utf-8"?>
<ForwardService>
  <para adapterName="ForwardCenter" />
  <para serverAddress="forward.labelcloud.cn" />
  <para serverPort="8080" />
  <para domainNumber="260000065" />
  <para clientId="Ypq6e7vxK" />
  <para clientSecret="c52ca688ee7b4a6898e78314db784717" />
  <para machineCode="7CFA5E5C-6559A281-CEB2EE89-9278E722" />
  <para sericeName="260000065#7021" />
  <para enable="true" />
</ForwardService>
```
* 按方式一部署的时候，需要把中转密钥放到APPserver和客户端的运行目录下。
* 按方式二部署的时候，需要把中转密钥放到ERPserver运行目录下，并修改Appserver中unity_communication.confg的配置指向中转服务。配置参考如下：
```
      <register type="IServiceCenter" mapTo="IceClientProxy">
        <lifetime type="singleton"/>
        <constructor>
          <param name="adapterName">
            <value value="ForwardCenter"/>
          </param>
          <param name="serverAddress">
            <value value="forward.labelcloud.cn"/>
          </param>
          <param name="serverPort">
            <value value="8080"/>
          </param>
          <param name="connectionNotify">
            <dependency type="IConnectionStatusNotify" name="localObj" />
          </param>
        </constructor>
        <property name="ForwardName" value="260000065#7029"/>
        <property name="ForwardType" value="Client"/>
      </register>
```


