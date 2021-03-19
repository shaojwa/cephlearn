这些书存储中的基本改变，每个存储系统都会有这些问题，因为这些问题的存在，而导致新方法的引入，比如因为RMW的存在，而引入ROW。

#### block-size 块大小

磁盘块大小，是对磁盘进行操作的最小粒度，也成为原子粒度，比如对普通机械硬盘，这个最小粒度为512B，即一个扇区，现在SSD普遍使用的更大的块大小，例如4KB。

#### RMW
Read Merge Write，写入数据不足块大小时，需要先读取原有块，然后合并，最后写入。这会引入两个问题就，一个是读惩罚，一个写操作触发了一个额外的读操作。
一个是在覆盖写的过程中，可能因为掉电而导致的数据丢失。

#### ROW
因为RMW问题的存在，所以需要引入方法，办法就是在覆盖写时，直接写入新的数据，然后写完成之后，更新元数据，最后释放原有空间。
但是根据长短法则，这个方法的缺点是，数据在磁盘分布的连续性。进过多次ROW之后，原本连续的数据块已经变得离散。

#### COW
写的时候，把原有数据拷贝到别的地方，新的数据写入到原有的位置，蓝书上说法有错。