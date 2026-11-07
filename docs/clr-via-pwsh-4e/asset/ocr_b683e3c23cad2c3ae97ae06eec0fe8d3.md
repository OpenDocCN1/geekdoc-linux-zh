```
public IEnumerator<T> GetEnumerator();
}
```

```
// 一个无序 key/value 对集合
public class ConcurrentDictionary<TKey, TValue> : IDictionary<TKey, TValue>,
    ICollection<KeyValuePair<TKey, TValue>>, IEnumerable<KeyValuePair<TKey, TValue>>,
    IDictionary, ICollection, IEnumerable {

    public ConcurrentDictionary();
    public Boolean TryAdd(TKey key, TValue value);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue this[TKey key] { get; set; }
    public Boolean TryUpdate(TKey key, TValue newValue, TValue comparisonValue);
    public Boolean TryRemove(TKey key, out TValue value);
    public TValue AddOrUpdate(TKey key, TValue addValue,
        Func<TKey, TValue> updateValueFactory);
    public TValue GetOrAdd(TKey key, TValue value);
    public Int32 Count { get; }
    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator();
}
```

所有这些集合类都是“非阻塞”的。换言之，如果一个线程试图提取一个不存在的元素（数据项），线程会立即返回；线程不会阻塞在那里，等着一个元素的出现。正是由于这个原因，所以如果获取了一个数据项，像 **TryDequeue、TryPop、TryTake** 和 **TryGetValue** 这样的方法全都返回 **true**；否则返回 **false**。

一个集合“非阻塞”，并不意味着它就不需要锁了。**ConcurrentDictionary** 类在内部使用了 **Monitor**。但是，对集合中的项进行操作时，锁只被占有极短的时间。**ConcurrentQueue** 和 **ConcurrentStack** 确实不需要锁；它们两个在内部都使用 **Interlocked** 的方法来操纵集合。一个 **ConcurrentBag** 对象（一个 bag）由大量迷你集合对象构成，每个线程一个。线程将一个项添加到 bag 中时，就用 **Interlocked** 的方法将这个项添加到调用线程的迷你集合中。一个线程试图从 bag 中提取一个元素时，bag 就检查调用线程的迷你集合，试图从中取出数据项。如果数据项在那里，就用一个 **Interlocked** 方法提取这个项。如果不在，就在内部获取一个 **Monitor**，以便从另一个线程的迷你集合提取一个项。这称为一个线程从另一个线程“窃取”一个数据项。

注意，所有并发集合类都提供了 **GetEnumerator** 方法，它一般用于 C# 的 **foreach** 语句，但也可用于 LINQ。对于 **ConcurrentStack、ConcurrentQueue** 和 **ConcurrentBag** 类，**GetEnumerator** 方法获取集合内容的一个“快照”，并从这个快照中返回元素；实际集合的内容可能在使用快照枚举时发生改变。**ConcurrentDictionary** 的 **GetEnumerator** 方法不获取它的内容的快照。因此，在枚举字典期间，字典的内容可能改变；这一点务必注意。还要注意的是，**Count** 属性返回的是查询时集合中的元素数量。如果其他线程同时正在集合中增删元素，这个计数可能马上就变得不正确了。

**ConcurrentStack、ConcurrentQueue** 和 **ConcurrentBag** 这三个并发集合类都实现了 **IProducerConsumerCollection** 接口。接口定义如下：

```
public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
    Boolean TryAdd(T item);
    Boolean TryTake(out T item);
    T[] ToArray();
```