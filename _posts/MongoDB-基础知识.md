---
title: MongoDB-基础知识
date: 2020-02-25 21:30:53
tags:
- MongoDB
categories: MongoDB
---

## GridFS

GridFS基于MongoDB的分布式文件存储系统,GridFS是一种将大型文件存储在MongoDB的文件规范。所有官方支持的驱动均实现了GridFS规范。GridFS是MongoDB中的一个内置功能，可以用于存放文件。

GridFS 使用两个集合来存储一个文件：fs.files与fs.chunks

### 与文件系统的区别

1. 文件系统到了后期会变的很难管理，同时不利于扩展。而GridFS却正好相反，它基于MongoDB的文件系统，便于管理和扩展
2. GridFS 会将大文件对象分割成多个小的chunk(文件片段),一般为256k/块,每块chunk将作为MongoDB的一个文档(document)被存储在chunks集合中。这一点对于很大的内容文件非常有用

### 使用场景

1. 如果你的文件系统对每个目录下文件的个数有限制（或者太多，将会影响文件的打开速度等）
2. 如果你希望访问一个超大的文件，而不希望将它全部加入内存，而是分段读取，那么GridFS天生就具备这种能力，你可以随意访问任意片段



### C#实现
- 上传
```js
var bucket = new GridFSBucket(database, new GridFSBucketOptions()
{
    BucketName = "my_bucket",
    ChunkSizeBytes = 256 * 1024, //块大小
});
Console.WriteLine("开始上传!");
using (var fs = File.OpenRead("test.iso"))
{
    bucket.UploadFromStream("test.iso", fs);
}
Console.WriteLine("上传完成.");
```
- 下载
```js
Console.WriteLine("开始下载");
var id = new ObjectId("5e551e65d93bc21cdc8973d6");
var bytes = bucket.DownloadAsBytes(id);

using (var target = File.Create("test1.iso"))
{
    bucket.DownloadToStream(id, target);
}
Console.WriteLine("下载完成");
```
- 查询
```js
var filter = new {filename = "123.jpg"};
var result = bucket.Find(filter.ToBsonDocument()).ToList();
```