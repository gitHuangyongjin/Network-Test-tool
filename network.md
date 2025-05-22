# http访问

### 测试端口是否开启
nc -zv www.baidu.com 80

### curl检查http情况
curl -v -I https://www.baidu.com

### curl 检查http链接速度情况
curl -s -o /dev/null -w "http_code: %{http_code}\ndns_time:%{time_namelookup}\ntime_connect:%{time_connect}\ntime_transfer:%{time_starttransfer}\ntime_total: %{time_total}s\ndown_speed: %{speed_download} bytes/s\n" https://www.jd.com

http_code: 200  
dns_time:0.030695  
time_connect:0.295198  
time_transfer:0.345109  
time_total: 0.345532s  
down_speed: 0 bytes/s  

#### 输出说明
time_namelookup: DNS解析时间  
time_connect: TCP连接时间，三次握手时间  
time_starttransfer: 从建立连接到接收到第一个字节的时间  
time_total: 传输的总时间  
speed_download: 下载速度，单位为字节/秒  
time_appconnect: 建立SSL连接的时间  
time_pretransfer: 从客户端发送请求到服务器接收第一个字节的时间  
time_redirect: 重定向时间  


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