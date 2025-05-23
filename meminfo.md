# linux内存meminfo说明

### 检查dmesg日志是否有OOM或内存错误
dmesg | grep -i memory

### 1. 查看完整内存状态
cat /proc/meminfo

### 2. 检查应用层pid占用内存
cat /proc/*/status | grep VmRSS  
grep -r '^VmRSS:' /proc/[0-9]*/status | awk '{split($0,a,"/"); print a[3],$2}' | sort -k2 -nr

### 3. 监控其他内存变化趋势（每2秒刷新）
watch -n 2 "cat /proc/meminfo | grep -E 'MemFree|Cached|Slab|Buffers|KernelStack'"

### 4. 检查slab内存详情
cat /proc/slabinfo  

/tmp # cat /proc/slabinfo  
slabinfo - version: 2.1
##### name            <active_objs> <num_objs> <objsize> <objperslab> <pagesperslab> : tunables <limit> <batchcount> <sharedfactor> : slabdata <active_slabs> <num_slabs> <sharedavail>  
##### zs_handle           1024   1024      8  512    1 : tunables    0    0    0 : slabdata      2      2      0

### 5. 检查大页内存使用
cat /proc/meminfo | grep Huge