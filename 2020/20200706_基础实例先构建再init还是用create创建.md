根据基础实例的构建模式，如果是工厂模式，构建的是基类实例，那么一般是通过静态工厂接口来创建，比如create:
```
// ceph_mds.cc
Messenger *msgr = Messenger::create()
```

但是，如果创建的就是类的实例，构建逻辑比较简单，一般直接用构造函数创建：
```
// ceph_mds.cc
mds = new MDSDaemon(g_conf->name.get_id().c_str(), msgr, &mc);
r = mds->init();
```
