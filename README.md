# Intrusion-detection-rules
入侵检测规则<br>
Suricata是一个优秀的开源入侵检测系统，此项目记录安全运营人员在学习和成长的过程中总结的的Suricata IDS规则,欢迎大家交流与分享。 

# 规则分类：
    0~1000000   Sourcefire VRT 保留
    2000001~2999999     EMerging Threats(ET)
    3000000~3999999     公用
    信息嗅探（Information_Sniffing） 3000000---3000999
    漏洞利用（Exploit） 3001000---3001999
    审计行为（Audit_Behavior） 3002000---3002999
    恶意通信（Malicious_Communication）3003000---3003999
    暴力破解（Exhaustive_Attack） 3004000---3004999
    协议分析（Protocol_Analysis）3005000-3005999
    其它（Other）3006000-3006999
# 规则命名方式：
        协议名称+规则分类+攻击手法
        HTTP_Malicious_Communicationg_webshell_china_chopper_php
# 示例：
        rev为规则版本每次修改递增，metadata添加创建日期与创建人
        reference为引用来源/参考资料，例如某CVE编号，或者修复方案，攻击说明等。
        alert http any any -> any any (msg:"HTTP_Malicious_Communicationg_webshell_china_chopper_php"; flow:established; content:"POST";
        http_method; content:".php"; http_uri; content:"base64_decode"; http_client_body;  sid:3003000; 
        rev:1; metadata:created_at 2020_10_28, by alex;)

