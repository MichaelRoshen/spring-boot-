# spring-boot-learn

spring boot入门视频： https://www.bilibili.com/video/av33908736/?p=17

java 泛型: https://blog.csdn.net/songkai320/article/details/51822497

Mybatis 在 Spring 下使用多数据源： https://xli1224.github.io/2018/03/11/spring-mybatis-multiple-datasource/

分布式锁的实现与应用场景对比: https://blog.csdn.net/lemon89/article/details/52796775

分布式锁的几种实现方式: https://www.cnblogs.com/austinspark-jessylu/p/8043726.html

Spring boot 异步开发之异步请求: https://www.jianshu.com/p/fb34041fa0a3

spring boot--使用异步请求，提高系统的吞吐量: https://blog.csdn.net/liuchuanhong1/article/details/78744138

tomcat7中maxConnections、maxThreads、acceptCount的含义及关系: https://blog.csdn.net/kaka20099527/article/details/53285348/

```ruby
List<Person> list = new ArrayList<>();
        list.add(new Person("name", 1));
        list.add(new Person("name", 2));
        list.add(new Person("name", 3));

//        累加 {name=6}
        Map<String, Integer> result1 = list.stream().collect(Collectors.toMap(Person::getName, Person::getAge, (p1, p2) -> p1+p2));
//        去重{name=1}
        Map<String, Integer> result2 = list.stream().collect(Collectors.toMap(Person::getName, Person::getAge, (p1, p2) -> p1));
//        去重{name=3}
        Map<String, Integer> result2 = list.stream().collect(Collectors.toMap(Person::getName, Person::getAge, (p1, p2) -> p1));

```

```ruby
List按属性去重
    //差集
    private List<Person> reducePersons(List<Person> list1, List<Person> list2) {
        Set<String> set = new HashSet<>();
        list2.stream().forEach(x -> {
            set.add(x.getName());
        });
        List<Person> reduceList = list1.stream().filter(item -> !set.contains(item.getName())).collect(Collectors.toList());
        return result;
    }

    //交集
    private List<Person> intersectionPerson(List<Person> list1, List<Person> list2) {
        Set<String> set = new HashSet<>();
        list2.stream().forEach(x -> {
            set.add(x.getName());
        });
        List<Person> reduceList = list1.stream().filter(item -> set.contains(item.getName())).collect(Collectors.toList());
        return result;
    }

    //并集
    private List<Person> unionDistinctPerson(List<Person> list1, List<Person> list2) {
        List<Person> list=new ArrayList<Person>();
        list.addAll(list1);
        list.addAll(list2);
        List<Person> uniqEventList = list.stream().filter(distinctByKey(Person::getName)).collect(Collectors.toList());
        return result;
    }

    public static <T> Predicate<T> distinctByKey(Function<? super T, ?> keyExtractor) {
        ConcurrentHashMap<Object, Boolean> map = new ConcurrentHashMap<>(16);
        return t -> map.putIfAbsent(keyExtractor.apply(t),Boolean.TRUE) == null;
    }
```
  
tips:
```ruby
String apiResult = HttpClientPoolUtil.get(url, request.getHeader("Cookie"));
JSONObject jsonApiResult = JSON.parseObject(apiResult);
List<Map> list = JSON.toJavaObject(jsonApiResult.getJSONArray("data"), List.class);
```

List按一个或多个对象属性去重
```ruby
List<User> unique2 = list.stream().collect(
                collectingAndThen(
                        toCollection(() -> new TreeSet<>(Comparator.comparing(o -> o.getName() + ";" + o.getAge()))), ArrayList::new)
        );

List<User> unique1 = list.stream().collect(
                collectingAndThen(
                        toCollection(() -> new TreeSet<>(Comparator.comparing(User::getName))), ArrayList::new));

```

Java Stream API groupingBy()  https://www.jdon.com/50132
