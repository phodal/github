#创建Pull Request

除了创建项目之外，我们也可以创建Pull Request来做贡献。

##第一个PR

我的第一个PR是给一个小的Node的CoAP相关的库的Pull Request。原因比较简单，是因为它的README.md写错了，导致我无法办法进行下一步。

		 const dgram       = require('dgram')
		-    , coapPacket  = require('coap-packet')
		+    , package     = require('coap-packet')

很简单，却又很有用的步骤，另外一个也是：

```
 else
   cat << END
 $0: error: module ngx_pagespeed requires the pagespeed optimization library.
-Look in obj/autoconf.err for more details.
+Look in objs/autoconf.err for more details.
 END
   exit 1
 fi
``` 

##CLA

CLA即Contributor License Agreement，在为一些大的组织、机构提交Pull Request的时候，可能需要签署这个协议。他们会在你的Pull Request里问你，只有你到他们的网站去注册并同意协议才会接受你的PR。

以下是我为Google提交的一个PR

![Google CLA](./img/google-cla.png)

以及Eclipse的一个PR

![Eclipse CLA](./img/eclipse-cla.png)

他们都要求我签署CLA。