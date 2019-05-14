# spring-boot-learn

## spring boot
- 入门视频： https://www.bilibili.com/video/av33908736/?p=17
- 异步开发之异步请求: https://www.jianshu.com/p/fb34041fa0a3
- 使用异步请求，提高系统的吞吐量: https://blog.csdn.net/liuchuanhong1/article/details/78744138
- 优雅编码之：Lombok加持：https://www.jianshu.com/p/c88b0f17f62a
- Spring MVC/Boot 统一异常处理最佳实践：http://www.zhaojun.im/springboot-exception/
- Spring Boot 使用hibernate validator校验: https://www.cnblogs.com/mr-yang-localhost/p/7812038.html
- Spring Boot 全局异常处理 与 Hibernate Validator校验框架整合：https://blog.csdn.net/Anenan/article/details/84313934
- Spring Boot 2.x 拦截器 https://my.oschina.net/u/182501/blog/1808140
- Springboot系列文章之过滤器 vs 拦截器 https://juejin.im/post/5ba3bdae6fb9a05cfc54d16d
- Filter、interception、AOP之间对比: https://www.jianshu.com/p/cd9875bd7161
- Spring Boot整合Ehcache实现缓存功能: https://www.jianshu.com/p/112a11d2918b
- 用自定义注解做点什么 https://juejin.im/entry/57e496fd7db2a20063a24a3a
- Java自定义注解 https://www.jianshu.com/p/a08e7e9ed765
- 日志管理器（异步操作记录日志的线程池) :https://blog.csdn.net/huangbaokang/article/details/74229845
- springboot使用注解的方式记录用户业务操作实战 ：http://www.voidcn.com/article/p-vyhiuwez-bow.html 
- 项目：https://github.com/stylefeng/Guns
- 深入理解Java线程池：ScheduledThreadPoolExecutor: https://www.jianshu.com/p/925dba9f5969

## java基础
- java 泛型: https://blog.csdn.net/songkai320/article/details/51822497
- ThreadLocal-面试必问深度解析: https://www.jianshu.com/p/98b68c97df9b
- JVM 的 工作原理，层次结构 以及 GC工作原理 https://segmentfault.com/a/1190000002579346#articleHeader6

## java效率工具
- Dozer 使用 https://dunwu.github.io/blog/page/7/
- Dozer 使用 https://www.hollischuang.com/archives/1613

## 算法实战
- java递归生成树形结构菜单： https://blog.csdn.net/LDY1016/article/details/85784001
- 无限级菜单/权限树该如何设计：http://www.zhaojun.im/permission-tree/

## Mybatis
- Mybatis 在 Spring 下使用多数据源： https://xli1224.github.io/2018/03/11/spring-mybatis-multiple-datasource/
- SpringBoot mybatis三种整合方式 https://my.oschina.net/wangnian/blog/667764
- SpringBoot 集成 mybatis http://www.apigo.cn/2018/08/12/springboot6/


## 分布式
- 分布式锁的实现与应用场景对比: https://blog.csdn.net/lemon89/article/details/52796775
- 分布式锁的几种实现方式: https://www.cnblogs.com/austinspark-jessylu/p/8043726.html

## 开发工具
- live template: intellij idea live template: https://www.youtube.com/watch?v=Q-aNE0RvBlg
- Matt Raible’s IntelliJ IDEA Live Templates: https://github.com/mraible/idea-live-templates

## 消息队列
- 消息队列及常见消息队列介绍1: https://cloud.tencent.com/developer/article/1006035
- 消息队列及常见消息队列介绍2:https://segmentfault.com/a/1190000015301449
- 消息队列面试，https://segmentfault.com/a/1190000015301449?utm_source=tag-newest
- kafaka介绍 https://www.cnblogs.com/skying555/p/7903457.html

## tomcat
- tomcat7中maxConnections、maxThreads、acceptCount的含义及关系: https://blog.csdn.net/kaka20099527/article/details/53285348/

## 设计模式
- 设计模式——空对象模式（Null Object Pattern）：https://www.cnblogs.com/hihtml5/p/6411161.html

## 学习计划
- 学习地图 http://blog.itpub.net/31555445/viewspace-2222297/


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
