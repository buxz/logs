# hash表
1. hash表中查找某个数据的平均查找次数为1，因为在hash表中，存放
在其中的数据和他的存储位置是用hash()函数关联的
2. hash表是长度为11的线性表，

# 数据存入hash表过程（以存储数字6为例）
1. 对 6 用hash函数计算一下，结果为1，
2. 把 6 放入到索引号是1的位置。
3. 当我们要从中找6这个元素时，直接根据hash函数计算6的索引位置，然
后直接从1号索引中找到它

# hash冲突问题
>两个不同的对象经过hash函数计算后，会有相同的hash值
1. java的hashMap对象采用“链地址法”解决该问题
    - 为所有hash值为i的对象建立一个同义词链表
    - 存入6时，如果发现1号位置被占，会新建一个链表节点放入6
    - 取出6时，发现1号位置里不是6，就会沿着链表依次查找
    - hash函数设计合理，可以保证同义词链表的长度被控制在一个
    合理的范围

# key值为自定义对象的时候需要重写hashCode()/equals()方法
```
public class Keys {
    private Integer id;
    public Keys(Integer id) {
        this.id = id;
    }
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    @Override
    public int hashCode() {
        return id.hashCode();
    }
    @Override
    public boolean equals(Object obj) {
        if (!(obj instanceof Keys)){
            return false;
        }else {
            return this.getId().equals(((Keys) obj).getId());
        }
    }
}
public class HashMapTest {
    public static void main(String[] args) {
        Keys k1 = new Keys(1);
        Keys k2 = new Keys(1);
        System.out.println(k1.hashCode());
        System.out.println(k2.hashCode());
        HashMap<Keys,String> hashMap = new HashMap<>();
        hashMap.put(k1,"Key with id is 1");
        System.out.println(hashMap.get(k2));
        System.out.println(hashMap.get(k1));
    }
}
```

1. 重写hashCode()
    - 存k1时，是根据它id的hash值，假设这里是100，把k1对象放入到对应的位置。而取k2时，是先计算它的hash值（由于k2的id也是1，这个值也是100），随后到这个位置去找。
2. 重写equals()
    - HashMap是用链地址法来处理冲突，也就是说，在100号位置上，有可能存在着多个用链表形式存储的对象。它们通过hashCode方法返回的hash值都是100
    - 由于我们在Key对象里没有定义equals方法，系统就不得不调用Object类的equals方法。由于Object的固有方法是根据两个对象的内存地址来判断，所以k1和k2一定不会相等，通过hashMap.get(k2)依然得到null
    - 重写 equals(),只要两个对象都是Key类型，而且它们的id相等，它们就相等。