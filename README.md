# mybatis-page-plugin
This is a mybatis plugin for pagenation.


### Usage

1. 在mysql的config文件中添加如下配置
```xml

  <plugins>
    <plugin interceptor="com.xjd.mybatis.page.PageInterceptor">
      <property name="databaseType" value="mysql"/>
    </plugin>
  </plugins>
```

2. 修改原来Mapper类中的方法(可以采取重载的方式，这样可以不影响原有方法)
```java

	List<TestBean> selectByCity(String city);

	List<TestBean> selectByCity(@Param("city") String city, Pagination page);
```

3. 最后在程序中使用
```java

	Page<TestBean> page = new Page<TestBean>(1, 20); // 第1页取20条
	List<TestBean> list = testMapper.selectByCity("SH", page); // 调用重载方法
	page.setResultList(list); // 注意此处要自己设值

	// 使用查询出来的结果...
```