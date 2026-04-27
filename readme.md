# Cloudflare IP 在线测试工具

[演示地址https://test.33322111.xyz ](https://test.33322111.xyz) 已开防护墙，仅CN区域访问可测速。


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
4.已支持IPV6测速，IPV4段、IPV6仅可用段已固定在index文件代码，可自行修改
5.卡Cloudflare通配ssl证书bug，支持SSL，使用"https://"访问

##  如何部署
### 三个二级域名，test.xxx.com作为网页前端，t.xxx.com作为后端NS解析，test.t.xxx.com作为后端测速（一定是t.xxx.com的下一级域名，生成SSL泛域名证书）。
1.  forks项目，修改forks项目下script.js文件第1行的域名为自己域名，然后找到该项目下Settings的Pages，Branch选择master /root文件夹，输入自定义域名Custom domain（填入前端域名test.xxx.com）勾选Enforce HTTPS ，保存部署。
2.  自己域名服务商：NS托管到Cloudflare。
3.  Cloudflare后台：新建Workers，复制项目中Cloudflare Workers配置文件的代码，记得修改 “ xxx.com ” 为“test.xxx.com”（网页前端），此处前面不加“.”，并为该Workers添加域名 “ .test.t.xxx.com ”（后端测速）和路由“ *.test.t.xxx.com/* ”（不要漏掉域名前后的符号*/），检查该托管域名下 SSL/TLS →→ 边缘证书 “*.test.t.xxx.com, xxx.com, test.t.xxx.com”状态有效后，进入下一步。
4. Cloudflare后台：DNS添加子域名*.t(注意前面有*和.)，对应三条NS记录分别为ns-hetzner.sslip.io、ns-ovh.sslip.io、ns-do-sg.sslip.io，（NS托管到sslip.io项目），同时前端域名test.xxx.com  CNAME解析自己域名到该Github项目Pages网址，开启橙色云朵，成功CNAME后，对应的Github项目下会有个CNAME文件，内容为自己前端域名。
5.  Cloudflare后台：SSL/TLS →→ 加密设置为完全（严格），DNS →→ 勾选 多提供商 DNS。


##  计划更新
 1. 增加Cloudflare Pages部署
## 🙏 致谢

本项目基于 [TulvL/cloudflare-ip-tester](https://github.com/TulvL/cloudflare-ip-tester) 做了些改进，感谢原作者TulvL的贡献。

