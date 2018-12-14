# spring-boot-learn

spring boot入门视频： https://www.bilibili.com/video/av33908736/?p=17

java 泛型: https://blog.csdn.net/songkai320/article/details/51822497

Mybatis 在 Spring 下使用多数据源： https://xli1224.github.io/2018/03/11/spring-mybatis-multiple-datasource/

```ruby
List按属性去重
public static <T> Predicate<T> distinctByKey(Function<? super T, ?> keyExtractor) {
    ConcurrentHashMap<Object, Boolean> map = new ConcurrentHashMap<>(16);
    return t -> map.putIfAbsent(keyExtractor.apply(t),Boolean.TRUE) == null;
}
list.stream().filter(distinctByKey(Person::getName)).collect(Collectors.toList())
```
  
tips:
```ruby
String apiResult = HttpClientPoolUtil.get(url, request.getHeader("Cookie"));
JSONObject jsonApiResult = JSON.parseObject(apiResult);
List<Map> list = JSON.toJavaObject(jsonApiResult.getJSONArray("data"), List.class);
```
