#中转部署结构
支持两种中转的部署结构，当然，不使用中转的情况下，可以全部部署到内部网络。
##方式一：
![](/assets/App中转部署图2.jpg)
App中转方式，如上图，APPserver作为中转服务的客户端，所有客户端连接到中转服务，然后所有的调用请求通过ICE的反向代理转发到对应的APPserver中进行处理。APPserver和ERPserver都部署在企业内网内。

##方式二：
![](/assets/ERP中转部署图2.jpg)
Erp中转方式，如上图，ERPserver作为中转服务的客户端，APPserver通过中转服务，对ERPserver发出调用请求。客户端和APPserver都部署在企业外网，只有ERPserver部署在企业内网。

