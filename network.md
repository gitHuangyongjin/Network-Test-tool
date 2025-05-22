### 测试端口是否开启
nc -zv www.baidu.com 80

### curl检查http情况
curl -v -I https://www.baidu.com

### curl 检查http链接速度情况
curl -o /dev/null -s -w %{time_namelookup}::%{time_connect}::%{time_starttransfer}::%{time_total}::%{speed_download}"\n" "http://sina.cn"
输出结果：
%{time_namelookup}::%{time_connect}::%{time_starttransfer}::%{time_total}::%{speed_download}



### 检查DNS是否被污染
nslookup github.com
dig github.com

#### 1. 强制使用公共DNS
curl --resolve www.baidu.com:443:180.101.50.188 -I https://www.baidu.com

#### 2. 检查是否被代理拦截
env | grep -i proxy  # 查看是否有代理设置
unset ALL_PROXY no_proxy

#### 3. 完全绕过本地网络设置
curl --interface eth0 -I https://www.baidu.com