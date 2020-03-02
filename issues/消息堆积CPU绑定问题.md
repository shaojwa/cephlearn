#### IRQ 绑定
    
    IRQ bindings 也叫IRQ affinity，IRQ 亲和性。

#### 问题

消息队列堆积

#### 分析

16个CPU使用率不均衡，top命令之后按1可以看到每个cpu的适用情况（man top -> Startup Defaults）。
其中，按1 cpu 模式，2 node模式， H 线程模式。

linux内核支持把不同的终端绑定到不同的CPU上， 即IRQ Affinity。

#### 如何查看各个CPU所处理的中断

    cat /proc/interrupts
    
在我的机子上， enp8s0f0 和 enp8s0f1 都集中在前4个CPU
    
#### 查看某个irp的CPU倾向

    cat /proc/irq/90/smp_affinity // 90是irq号
    
#### 停止自动平衡

    systemctl status irqbalance
    /etc/init.d/irqbalance stop

####  场景

手动设置 affinity，一般只在特殊的场景下使用，比如多网卡多硬盘的网络存储服务器。

#### 参考

    https://www.vpsee.com/2010/07/load-balancing-with-irq-smp-affinity/
