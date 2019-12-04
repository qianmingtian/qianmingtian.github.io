<!--
 * @Author: 千铭天
 * @Date: 2019-11-01 17:23:55
 * @LastEditors: 
 * @LastEditTime: 2019-11-01 17:29:20
 * @Description:  
 -->
# git clone server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile

今天在运行git clone命令时遇到如下错误：

在here 看到之前有人遇到过同样的问题，现将解决思路提供如下。

主要的问题是你的linux系统并不信任你所要git的网站，所以通不过系统安全认证。解决方案有两个：第一，告诉系统这个网站是可信任的；第二，关闭系统的安全认证，这个有些极端了。

告诉系统这个网站是可信任的
由于这个方法操作起来比较繁琐，我并没有采用这种方法，但是将这种方法的具体步骤提供给大家。


> You need to check the web certificate used for your gitLab server, and add it to your </git_installation_folder>/bin/curl-ca-bundle.crt. 
To check if at least the clone works without checking said certificate, you can set: 

```git
export GIT_SSL_NO_VERIFY=1 
or 
git config --global http.sslverify false
```

But that would be for testing only, as illustrated in “SSL works with browser, wget, and curl, but fails with git“, or in this blog post.

Check your GitLab settings, a in issue 4272.

To get that certificate (that you would need to add to your curl-ca-bundle.crt file), type a:
``` shell
echo -n | openssl s_client -showcerts -connect yourserver.com:YourHttpGilabPort 2>/dev/null  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'
(with yourserver.com being your GitLab server name)
```
To check the CA (Certificate Authority issuer), type a:
```shell
echo -n | openssl s_client -showcerts -connect yourserver.com:YourHttpGilabPort 2>/dev/null  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'| openssl x509 -noout -text | grep "CA Issuers" | head -1
```
to identify the location of curl-ca-bundle.crt, you could use the command
```git
curl-config --ca
```
## 关闭系统的安全认证
我使用的是这种简单粗暴的方式，关闭验证。这种方式能在很短时间内收到效果，如果没有耐心进行上面的设置的话，可以采用下面的命令。打开终端，在命令行中输入如下命令即可：

``` git 
export GIT_SSL_NO_VERIFY=1
```