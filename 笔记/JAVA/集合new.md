#队列queue
先进先出
#迭代器Iterator接口
##java.util.Iterator
只有4个方法  
1. E next();返回下一个元素  
2. boolean hasNext();是否还有下一个  
3. void remove();删除上次调用next方法时返回的元素。remove方法不能连续调用两次。
4. default void forEachRemaining(Consumer<? super E> action)   
java迭代器是位于两个元素之间，最开始位于第一个元素的前面， 所有在执行remove方法之前，必须要执行next方法
![avatar](..\imgs\4.png)

	循环集合的两种方式
	List<String> list = new ArrayList<>();
    list.add("213");
    list.add("432");
    list.add("66");
	Iterator<String> iterator = list.iterator();
	1、
	while (iterator.hasNext()) {
        System.out.println(iterator.next());
    }

	2、
    iterator.forEachRemaining(item->{
        System.out.println(item);
    });
	
#Collection接口
Collection接口继承了Iterable接口    
1. Iterator<E> iterator();返回一个用于访问集合中每个元素的迭代器  
2. int size();返回当前存储在集合中的元素个数  
3. boolean isEmpty();如果集合中没有元素，返回true  
4. boolean contains(Onject obj);如果集合中包含了一个与obj相等的对象，则返回true  
5. boolean containsAll(Collection<?> other);如果这个集合包含other集合中的所有元素，返回true  
6. boolean add(Object element);将一个元素添加到集合中   
7. loolean addAll(Collection<? extends E> other);将other集合的所有元素添加到这个集合  
8. boolean remove(Object obj);从这个集合中删除obj，如果删除成功，返回true  
9. boolean removeAll(Collection<?> other);从这个集合中删除other集合中存在的所有元素    
10. default boolean removeIf(Prediacte<? super E> filter);从这个集合中删除filter返回true的元素  

		list.removeIf(item->{
            if (item.equals("213")) {
                return true;
            }
            return false;
        });
11. void clear();从这个集合中删除所有元素  
12. boolean retainAll(Collection<?> other);从这个集合中删除所有与other集合中元素不一样的元素  
13. Object[] toArray();返回这个集合的对象数组  
#集合框架中的接口
![avatar](..\imgs\5.png)  
上图：集合框架中的接口  
**集合有两个基本接口：Collection和Map**
#Map是键值对
#List是有序集合
**集合框架中有两种有序集合。由数组支持的有序集合可以快速的随机访问，因此适合使用List方法并提供一个整数索引来访问；由链表支持的有序集合，随机访问很慢，所以最好使用迭代器遍历**
#Set接口等同于Collection,Set不允许添加重复的元素

	已经存在的元素无法添加进去
![avatar](..\imgs\6.png) 
#具体的集合
![avatar](..\imgs\7.png)   
集合框架中的类
##链表
**Linkedlist**    
数组和数组列表在数组的中间删除元素要要付出很大的代价，因为处于被删除元素之后的所有元素都要向数组的前端移动  
java中，所有链表实际上都是双向链接的  
链表是一个有序集合  
只有对自然有序的集合使用迭代器添加元素才有实际意义  
1. Object get(n);获取链表的第n个元素；该方法效率很低
###ListIterator接口
1. E previous()；返回越过的对象  
2. boolean hasPrevious();判断前面是否还有元素  
3. void add(E element);在迭代器位置前面增加一个元素  
4. void remove();删除的是迭代器上一次越过的元素，如果上一次调用的是next方法，则删除的是迭代器左边的元素。如果上一次调用的是previous方法，则删除的是右边的元素。且remove方法不能连续调用两次。  
5. void set(E newValue);用newValue取代调用next或previous方法返回的上一个元素
6. int nextIndex();返回下一次调用next方法时返回元素的整数索引  
7. previousIndex();返回下一次调用previous方法时返回元素的整数索引      
一个迭代器指向另一个迭代器刚刚删除的元素前面，现在这个迭代器就是无效的。如果迭代器发现它的集合被另一个迭代器修改了，或是被该集合自身的方法修改了，就会抛出一个ConcurrentModificationException()异常。  
**对于并发修改列表有一个奇怪的例外，添加元素、删除元素可以检测到，但是set方法不被视为结构性修改，无法检测**
###java.util.List`<E>`
1. ListIterator`<E>` listIterator()

		返回一个列表迭代器，以便用来访问列表中的元素
2. ListIterator`<E>` listIterator(int index)

		返回一个列表迭代器，该迭代器指向索引为n的元素前面的位置
3. void add(int i,E element)

		在给定位置添加一个元素
4. void addAll(int i,Collection<? extends E> elements)

		将某个集合中的所有元素添加到给定位置
5. E remove(int i)

		删除给定位置的元素并返回这个元素
6. E get(int i)

		获取指定位置的元素
7. E set(int i,E element)

		用新元素取代给定位置的元素，并返回原来那个元素
8. int indexOf(Object element)

		返回与指定元素相等的元素在列表中第一次出现的位置，没有则返回-1
9. int lastIndexOf(Object element)

		返回与指定元素相等的元素在列表中最后一次出现的位置，没有则返回-1
###java.util.ListIterator`<E>`
1. void add(E newElement)

		在当前位置前添加一个元素
2. void set(E newElement)

		用新元素取代next或previous上次访问的元素。如果在next或previous上次调用之后列表被修改了，则抛出一个IllegalStateException异常
3. boolean hasPrevious()

		当反向迭代列表时，还有可供访问的元素，返回true
4. E previous()

		返回前一个对象，如果已经到头了，就抛出一个NoSuchElementException异常
5. int nextIndex()

		返回下一次调用next方法时将返回元素的索引
6. int previousIndex();

		返回下一次调用previous方法时将返回元素的索引
###java.util.LinkedList`<E>`
1. LinkedList()

		构造一个空链表
2. LinkedList(Collection<? extends E> elements)

		构造一个链表，并将集合中所有元素添加到链表中
3. void addFirst(E element);
4. void addLast(E element);

		将元素添加到列表的头部或者尾部
5. E getFirst()
6. E fetLast()

		返回列表头部或尾部元素
7. E removeFirst()
8. E removeLast()

		删除并返回列表头部或尾部的元素
#数组列表
###Vector
Vector的所有方法都是同步的，适合多线程，效率低  
ArrayList的方法不是同步的，适合单线程，效率高    
###散列表hashtable  
散列表为每个对象计算一个整数，称为散列码。散列码是由对象的实例域产生的一个整数，具有不同实例域的对象将产生不同的散列码。  
在JAVA中，散列表用链表数组实现。每个列表被称为桶（bucket），要想查找表中对象的位置，就要先计算它的散列码，然后与桶的总数取余，所得的结果就是保存这个元素的桶的索引。     
###Set
set是没有重复元素的元素集合。 set的add方法首先在集中查找要添加的对象，如果不存在，则将对象添加进去   
HashSet类，实现了基于散列表的集。contains方法被重新定义，只在某个桶中查找元素，而不必查看集合中的所有元素    
如果散列表太满，就需要再散列，就是需要创建一个桶数更多的表，并将所有元素插入到这个新表中，然后丢弃原来的表。  
**装填因子：**默认0.75，即如果表中超过75%的位置已经填入元素，这个表就会用双倍的桶数自动地进行再散列  
**注意：在更改集中的元素时要小心，如果元素的散列码发生改变，元素在数据结构中的位置也会发生改变**
###java.util.HashSet`<E>`
1. HashSet()

		构造一个空散列表
2. HashSet(Collection<? extends E> elements)

		构造一个散列集，并将集合中的所有元素添加到这个散列集中
3. HashSet(int initialCapacity)

		构造一个空的具有指定容量（桶数）的散列集
4. HashSet（int initialCapacity,float loadFactory）

		构造一个具有指定容量和装填因子（0.0~1.0）的空散列表
###java.lang.Object
1. int hashCode()

		返回这个对象的散列码
#树集
###TreeSet：有序集合
可以以任意顺序将元素插入到集合中。在对集合进行遍历时，每个值将自动按照排序后的顺序呈现  
要使用树集，必须能够比较元素。这些元素必须实现Comparable接口，或者构建集时必须提供一个Comparator
###java.util.TreeSet`<E>`
1. TreeSet()

		构造一个空树集，元素将按实现的Comparable接口进行排序
2. TreeSet(Comparator<? super E> comparator)

		构造一个空树集，元素将按照提供的比较器进行排序
3. TreeSet(SortedSet<E> s)

		构造一个空树集，并增加一个集合或有序集中的所有元素
###java.util.SortedSet`<E>`
1. Comparator<? super E> comparator()

		返回用于对元素进行排序的比较器。如果元素用Comparable接口的compateTo方法进行比较则返回null
1. E first ()

		回有序集中的最大元素，即第一个元素
2. E last()

		回有序集中的最小元素，即最后一个元素
###java.util.NavigableSet`<E>`
1. E higher(E value)

		返回大于value的最小元素，没有返回null
2. E lower(E value)

		返回小于value的最大元素，没有返回null
3. E ceiling(E value)

		返回大于等于value的最小元素，没有返回null
4. E floor(E value)

		返回小于等于value的最大元素，没有返回null
6. E pollFirst()

		删除并返回这个集中的最大元素，集为空时返回null
7. E pollLast()

		删除并返回这个集中的最小元素，集为空时返回null
8. Iterator<E> descendingIterator()

		返回一个按照递减顺序遍历集中元素的迭代器
**TreeSet(实体类)实现了NavigableSet接口，NavigableSet接口继承了SortedSet接口，SortedSet接口继承了Set接口**
#队列与双端队列
###队列
有效的在尾部添加一个元素，在头部删除一个元素。
###双端队列
有两个端头的队列，即双端队列，可以有效的在头部和尾部同时添加和删除元素，不支持在队列中间添加元素  
Deque接口，由ArrayDeque和LinkedList类实现。这两个类都提供了双端队列，并且在必要的时候可以增加队列的长度。
###java.util.Queue`<E>`
1. boolean add(E element)
2. boolean offer(E element)

		如果队列没有满，则将这个元素添加到双端对联的尾部并返回true.如果队列满了，第一个方法抛出IllegalStateException，而第二个方法返回false
3. E remove()
4. E poll()

		如果队列不空，删除并返回这个队列的头部元素。如果队列是空的，第一个方法抛出NoSuchElementException，而第二个方法返回null
5. E element()

		如果队列不空，返回这个队列头部元素，但不删除。如果队列空，第一个方法返回一个NoSuchElementException异常，第二个方法返回null
###java.util.Deque`<E>`
1. void addFirst(E element)
2. void addLast(E element)
3. boolean offerFirst(E element)
4. boolean offerLast(E element)

		将给定的元素添加到双端队列的头部或者尾部。如果队列满了，前两个方法抛出一个IllegalStateException异常，后两个方法返回false
5. E removeFirst()
6. E removeLast()
7. E pollFirst()
8. E pollLast()

		如果队列不为空，删除并返回队列头部的元素。如果队列为空，前两个方法将抛出一个NoSuchElementException异常，后两个返回null
9. E getFirst()
10. E getLast()
11. E peekFirst()
12. E peekLast()

		如果队列非空，返回队列头部和尾部的元素，但不删除。如果队列为空，前面两个方法将抛出一个NoSuchElementException，而后面两个方法返回null
###java.util.ArrayDeque`<E>`
1. ArrayDeque()
2. ArrayDeque(int initialCapacity)

		用初始容量16或给定的初始容量构造一个无限双端队列
###优先级队列（PriorityQueue）
优先级队列中的元素可以按照任意顺序插入，但是在执行remove的时候，每次删除的都是优先级最高的元素，即最小的元素。习惯上将1设为最高优先级  
**PriorityQueue保存的对象必须实现Comparable接口或者在构造器中提供一个Comparator对象**

	PriorityQueue<Student> students = new PriorityQueue<>((t1,t2)->{
        int n = Integer.compare(t1.getAge(), t2.getAge());
        return n;
    });
#映射
java为映射提供了两个通用的实现：HashMap和TreeMap  
散列映射对键进行散列；树映射用键的整体顺序对元素进行排序，并将其组成搜索树。散列或比较函数只能作用于键，与键相关的值不能进行散列或比较      
**键值必须唯一，如果对同一个键进行两次put，则第二次的值会取代第一次的值**  
**map的键和值可以为null**
##java.util.Map<K,V>
1. v get(Object key)

		获取与键对应的值，如果没有这个对象，返回null
2. default V getOrDefault(Object key, V defaultValue)

		获取与键关联的值，如果不存在，则返回defaultValue
3. V put(K key,V value)

		将键与对应的值插入到映射中。如果这个键已经存在，新对象将取代就对象。这个方法将返回键对应的旧值，如果这个键以前没有出现过则返回null。
4. void putAll(Map<? extends K,? extends V> entries)

		将给定映射中的所有条目添加到这个映射中
5. boolean containsKey(Object key)

		如果在映射中已经有这个键，返回true
6. boolean containsValue(Object value)

		如果映射中已经有这个值，返回true
7. default void forEach(BiConsumer<? super K,? super V> action)

		对这个映射中的所有键/值对应用这个动作
		staff.forEach((k,v)->{
            System.out.println("k = " + k + ", v = " + v);
        });
8. V putIfAbsent(K key,V value)

		如果key不存在，则将key和value添加到映射中，并且返回null。如果key存在，则返回key对应的value
##java.util.HashMap<K,V>
1. HashMap()
2. HashMap(int initialCapacity)
3. HashMap(int initialCapacity,float loadFactor)

		用给定的容量和装填因子构造一个空散列映射。默认的装填因子是0.75
##java.util.TreeMap(K,V)
1. TeeeMap()
	
		为实现Comparable接口的键构造一个空的树映射
2. TreeMap(Comparable<? super K> c)

		构造一个树映射，并使用一个指定的比较器对键进行排序
3. TreeMap(Map<? extends K,? extends V> entries)

		构造一个树映射，并将某个映射中的所有条目添加到树映射中
4. TreeMap(SortedMap<? extends K,? extends V> entries)

		
		构造一个树映射，将某个有序映射中的所有条目添加到树映射中，并使用与给定的有序映射相同的比较器
##java.util.SortedMap<K,V>
1. Comparator<? super K> comparator()

		返回对键进行排序的比较器。如果用的Comparable接口的compareTo方法进行比较的，返回null
2. K firstKey()
3. K lastKey()

		返回映射中最小元素和最大元素
##java.util.Map<K,V>
1. default V merge(K key, V value, BiFunction<? super V,? super V,? extends V> remappingFunction)

		Map<String, Integer> map = new HashMap<>();
		map.merge("abc", 2,(oldV,newV)->{
                return oldV + newV;
            });
		如果map中不存在键"abc"或者map中"abc"键对应的值为null，则将（"abc",2）添加到映射中，如果map中存在abc键，且值不为null，则将键abc对应的值改为return的值。oldV是旧值，newV是2
2. default V compute(K key, BiFunction<? super V,? super V,? extends V> remappingFunction)

		Map<String, Integer> map = new HashMap<>();
		map.compute("abc" ,(key, value) -> {
            System.out.println("k = " + key);
            System.out.println("v = " + value);
            return 6;
        });
		
		将map中键abc对应的值改为return的值。value为abc对应的旧值。
		如果abc不存在，则将键abc和return的值添加到map中
		如果abc不存在或者abc对应的值为null，value的值就是null。
3. default V computeIfPresent(K key,BiFunction<? super V,? super V,? extends V> remappingFunction)

		Map<String, Integer> map = new HashMap<>();
        map.put("abc", 12);
        map.computeIfPresent("abc",(k,v)->{
            System.out.println("k = " + k);
            System.out.println("v = " + v);
            return 22;
        });
        System.out.println(map);
		
		只有当map存在key时，并且key对应的值不为null，才执行后面方法里的逻辑并且将key对应的值改为return的值；否则什么都不做。
4. default V computeIfAbsent(K key,BiFunction<? super V,? extends V> remappingFunction)

		Map<String, Integer> map = new HashMap<>();
        map.computeIfAbsent("abc",(k)->{
            System.out.println("k = " + k);
            return 12;
        });
        System.out.println(map);
		只有当map中不存在abc键，或者abc键对应的值为null时，才执行后面的方法，将键abc和return的值添加到map中，本例中k的值就是"abc"。否则什么都不做
5. default void replaceAll(BiFunction<? super V,? super V,? extends V> remappingFunction)

		对映射的每一项应用后面的函数，将key对应的value设置成return的值。
		Map<String, Integer> map = new HashMap<>();
        map.put("a", 1);
        map.put("b", 2);
        map.replaceAll((key,value)->{
            System.out.println("v = " + key);
            System.out.println("k = " + value);
            return 12;
        });
        System.out.println(map);
		
		
		
		



		
		








