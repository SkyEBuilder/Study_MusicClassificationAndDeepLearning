# 一些想法
根据给出的数据: 

21 Columns, 9 Decimal,6 integral,5 string, 1 bool

其中Trackid是base-62编码出的str，可以在[Spotify](https://developer.spotify.com/documentation/web-api/concepts/spotify-uris-ids)上看到，这个是这个数据集的KEY，可以转换成数字,训练中用不到

track_genre虽然是str,但只有114个独特值，直接变成enum便于后续使用。

还有三个str分别表示艺术家，专辑名，单曲名，应该用不到

还有一个没名字的序号列也丢掉。

所以最后进入内存的应该是15 Columns, 8or9 Decimal,8or7 integral, 1 bool;其中

popularity和catagory不会同时出现，因为它们的任务是独立的

由于对于分类训练来说，没有更改数据集的需求，也没有查询特定数值的需求，对每一列使用连续地址的array存储是读取效率最快的。

# Model Building
把`track_genre` one-hot 编码，防止连续数值导致一些问题

# 现在完成的工作有
1. 对于训练用不到的序列删除了，产出了[Processed_dataset](processed_dataset.csv)
2. 使用SKlearn的MLP做了初步尝试，准确率从16%->22%，代码在[tests](tests.ipynb)

# 计划中的工作
1. 部署mindSpore环境（似乎完成了）
2. 在mindSpore上复现已经完成的内容
3. 一些文书工作：记录现有的进度，写成报告的样子