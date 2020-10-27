# Intrusion-detection-rules
入侵检测规则
Suricata是一个优秀的开源入侵检测系统，此项目记录安全运营人员提取的高质量Suricata IDS规则,欢迎大家提交。 

规则分类：

sid类型：
0~1000000   Sourcefire VRT 保留
2000001~2999999     EMerging Threats(ET)
3000000~3999999     公用
信息嗅探（Information_sniffing） 3000000---3000999
漏洞利用（Exploit）
审计行为（Audit Behavior）
恶意通信（Malicious Communication）
暴力破解（Exhaustive Attack）
协议分析（Protocol Analysis）
安全管理（Security Management）
rev为规则版本每次修改递增，metadata添加创建日期与创建人
reference为引用来源/参考资料，例如某CVE编号，或者修复方案，攻击说明等。
alert http any any -> any any (msg:"webshell_caidao_php"; flow:established; content:"POST";
http_method; content:".php"; http_uri; content:"base64_decode"; http_client_body;  sid:3004001; 
rev:1; metadata:created_at 2018_11_14, by al0ne;)

规则命名方式：

规则分类+协议名称+简要描述

示例：
