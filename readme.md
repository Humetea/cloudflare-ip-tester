# Cloudflare IP 在线测试工具

[演示地址https://33322111.xyz ](https://33322111.xyz) 


## 原有功能

1. HTTP(s)响应时间测试
2. 平均下载速度测试（使用不同大小的文件测试）
3. 进行批量测试。
4. 显示每个任播 IP 的实际位置（根据 /cdn-cgi/trace判断）
5. 针对每个IP中的多个测试进行简单的统计分析
6. 适配移动设备（目前仅测试过安卓系统）
7. 导出测试结果

##  改进功能

1. 添加随机生成IP数量（上限5000，下限1）
2. 添加停止测试功能
3. 中文汉化
4. Cloudflare IP段已固定在index文件代码，可自行修改
5. 支持SSL，可以使用"https://"访问

##  如何部署

1.  forks项目，修改forks项目下script.js文件第1行的域名为自己域名，然后找到该项目下Settings的Pages，Branch选择master /root文件夹，输入自定义域名Custom domain，勾选Enforce HTTPS 保存部署。
2.  自己域名服务商：NS托管到Cloudflare，同时还要添加三条NS记录：名称都填@，记录值分别为ns-hetzner.sslip.io、ns-ovh.sslip.io、ns-do-sg.sslip.io（只解析一级域名，因为cf免费版只对一级域名颁发通配型ssl证书，注意abc.xxx.com为二级域名）。
3.  Cloudflare后台：DNS--设置--开启多提供商 DNS；DNS记录 CNAME解析自己域名到该Github项目Pages网址，成功CNAME后，可开启橙色云朵，对应的Github项目下会有个CNAME文件，内容为自己域名。
4.  Cloudflare后台：SSL/TLS 加密设置为完全（严格）。
5.  Cloudflare后台：新建Workers，复制项目中Cloudflare Workers配置文件的代码，记得修改 “ xxx.com ” 为自己域名，并为Workers添加路由 “ *.自己域名/* ”。

##  计划更新
 1. 增加Cloudflare Pages部署
 2. 增加ipv6测速功能
## 🙏 致谢

本项目基于 [TulvL/cloudflare-ip-tester](https://github.com/TulvL/cloudflare-ip-tester) 做了些改进，感谢原作者TulvL的贡献。

