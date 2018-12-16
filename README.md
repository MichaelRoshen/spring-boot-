# spring-boot-learn

spring boot入门视频： https://www.bilibili.com/video/av33908736/?p=17

java 泛型: https://blog.csdn.net/songkai320/article/details/51822497

Mybatis 在 Spring 下使用多数据源： https://xli1224.github.io/2018/03/11/spring-mybatis-multiple-datasource/

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

