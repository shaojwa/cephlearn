#### 20210421
1. DM/RCache多线程代码何如
2. DM shutdown处理
3. DM lsm quota计算
4. object的hash不再计算，直接用object中的seed

#### 20210129
从下周(20210201)开始，测试那边就要开始投入测试，在过年前发现的问题不提单；年后发现的问题提简易单。

#### 20201123
1. 代码格式需改，修改前：2164行，修改后2394行。
1. 添加dm模块调试接口

#### 20201120 代码review
1. 补齐读相关的quota计算需要考虑仔细
1. quota申请是否需要对齐
1. dm_write_obj_data()接口可以用void就不要返回值
1. opproc有冲突检测么？
1. 写数据opproc和读操作。（怎么配合）
1. opproc先写DM（同步给mingjingou）
1. 先up选对
1. 写-写流程简化
1. 有操作挂着时，下刷如何进行。
1. dm_read_obj_data() 接口不需要sem
1. 去掉不需要的操作
1. 后续op操作，和刷盘如何配合

#### 20201120
1. 测试用例补充测试以及bug修复。（完成）
2. ROW数据补齐读代码修改（ROW接口有修改）（完成）
3. 代码检视及问题修改（完成）
4. 增加可测试性命令 （完成50%）

#### 20201110 代码review
1. ht_hash()接口需要改进。
1. node_set改为实例数组，不用指针数组。
1. hn_get_object() 简化函数实现。
1. dm_conflict_check() 在内部down掉sem。
1. dm_conflict_post() 不查 conflict。
1. obj_write_fragment中的锁不需要。
1. 直接写ptr就可以
1. 清元数据（在刷完盘之后）
1. 补齐之后，元数据要不要更新（找yinhuiyu对齐）