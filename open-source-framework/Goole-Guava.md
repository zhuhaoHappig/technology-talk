## Goole Guava

===

### 一、缓存相关
如果服务上要使用本地缓存，可以考虑使用guava框架。Guava Cache与ConcurrentMap很相似，但也不完全一样。最基本的区别是ConcurrentMap会一直保存所有添加的元素，直到显式地移除。相对地，Guava Cache为了限制内存占用，通常都设定为自动回收元素。在某些场景下，尽管LoadingCache 不回收元素，它也是很有用的，因为它会自动加载缓存。

#### Guava Cache适用于：

* 你愿意消耗一些内存空间来提升速度。
* 你预料到某些键会被查询一次以上。
* 缓存中存放的数据总量不会超出内存容量。

```
 private Cache<String, UserAuthTokenRecord> localCache = CacheBuilder.newBuilder().maximumSize(200000)
            .initialCapacity(100000).expireAfterWrite(30, TimeUnit.SECONDS).<String, UserAuthTokenRecord>build();
            
```

### 缓存回收

* ##### 基本容量的回收

  1）设置了初始值和最大容量上限，如果逼近容量上限，就会触发回收机制。
  
* ##### 定时回收

	1）expireAfterAccess(long, TimeUnit)：缓存项在给定时间内没有被读/写访问，则回收。请注意这种缓存的回收顺序和基于大小回收一样。
	
	2）expireAfterWrite(long, TimeUnit)：缓存项在给定时间内没有被写访问（创建或覆盖），则回收。如果认为缓存数据总是在固定时候后变得陈旧不可用，这种回收方式是可取的。

* #####基于引用的回收




参考资料：


[http://ifeve.com/google-guava-cachesexplained/](http://ifeve.com/google-guava-cachesexplained)
