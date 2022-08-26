# jenkins
## 查看 jenkins 的运行状态
+ systemctl status jenkins
## 启动 jenkins
+ service jenkins start
## 重启 jenkins 服务
+ cd /opt/
+ sudo java -jar jenkins.war
## jenkins 中邮件模板位置
+ /root/.jenkins/email-templates
## windows slave 机器中，重启
+ 在C:\Users\datalake\Downloads路径下
+ java -jar agent.jar -jnlpUrl http://10.28.172.24:8080/computer/10%2E28%2E172%2E23/jenkins-agent.jnlp -secret fec7397536ed7215d8784eda21c944919cbe2e5148bf34150e9a75cbdf3a5a23 -workDir "D:\jenkins_node"
## 重启 openVpn服务
+ sudo openvpn --daemon --config /etc/openvpn/mobile.ovpn --log-append /var/log/openvpn.log
## jenkins 流水线 retry 功能
+ retry(3)