---
layout: default
title: Spring
---

# Spring Integration #

Liquibase can be run in a [Spring](http://www.springframework.org) environment by declaring a liquibase.spring.SpringLiquibase bean.

## Example ##

{% highlight xml %}
<bean id="liquibase" class="liquibase.integration.spring.SpringLiquibase">
      <property name="dataSource" ref="myDataSource" />
      <property name="changeLog" value="classpath:db-changelog.xml" />
      <property name="contexts" value="test, production" />
 </bean>
{% endhighlight %}

## Available Attributes ##

* beanName
* changeLog
* contexts
* labels
* dataSource
* defaultSchema
* dropFirst **since 2.0.2**
* parameters
* resourceLoader
