### route结果

        Kernel IP routing table
        Distination   Gateway     Genmask         Flags Metric Ref  Use Iface
        10.132.32.0   0.0.0.0     255.255.254.0   U     0       0   0   ethA01-0
        link-local    0.0.0.0     255.255.0.0     U     1002    0   0   ethA01-0

### 在网卡配置添加GATEWAY之后：
        
        Kernel IP routing table
        Distination   Gateway     Genmask         Flags Metric Ref  Use Iface
        default       gateway     0.0.0.0         UG    0       0   0   ethA01-0      
        10.132.32.0   0.0.0.0     255.255.254.0   U     0       0   0   ethA01-0
        link-local    0.0.0.0     255.255.0.0     U     1002    0   0   ethA01-0        
        link-local    0.0.0.0     255.255.0.0     U     1003    0   0   ethA01-1
        172.16.84.0   0.0.0.0     255.255.255.0   U     0       0   0   ethA01-1
      
