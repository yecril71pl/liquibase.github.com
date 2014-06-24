---
layout: default
title: Labels
---

# Labels #

"Labels" in Liquibase are tags you can add to changeSets to control which will be executed in any particular migration run. Any string can be used for the label name and they are checked case-insensitively.

When you run Liquibase though any of the available methods, you can pass in an expression defining the labels to run. Only changeSets marked with the matching labels..

If you don't assign a label to a changeSet, it will run all the time, regardless of what label expression you pass in to Liquibase.

If you do not specify a label expression when you run Liquibase, ALL labels will match.

Here is an example of a change set using the labels attribute:
{% highlight xml %}
   <changeSet id="2" author="bob" labels="test">
        <insert tableName="news">
            <column name="id" value="1"/>
            <column name="title" value="Liquibase 0.8 Released"/>
        </insert>
        <insert tableName="news">
            <column name="id" value="2"/>
            <column name="title" value="Liquibase 0.9 Released"/>
        </insert>
    </changeSet>
{% endhighlight %}

## Labels vs. Contexts

Labels are similar to [contexts](contexts.html) in that both can be used to control which changeSets execute. The difference is in where complex selector logic can be defined. 
With contexts, you can only define a set of contexts at runtime, but can specify a complex expression in your changeSet. 
With labels, you can only define a set of labels in your changeSet but can specify a complex expression at runtime. 

Use labels if the logic to know which changeSets to run is known or is changed at runtime, or if the person doing the deployment wants more control of the changeSets to run. 

Use contexts if the logic to know which changeSets to run is known when writing the changeLog, or if the person writing the changeSet wants more control of the changeSets to run.       

## Label Expression Syntax ##

At runtime, an expression for selecting labels can be specified using AND, OR, ! and parentheses. Without parentheses the order of operations are "!" then "AND" then "OR".

__Examples:__

 * --labels="!test"
 * --labels="v1.0 or map"
 * --labels="v1.0 or map"
 * --labels="!qa and !master"

 Using a "," to separate labels works like an OR operation but with the highest precedence.

 __Examples:__

  * "test, qa" is the same as "test OR qa"
  * "test, qa and master" is the same as "(test) OR (qa and master)

__Availability:__

* Labels are available in Liquibase 3.3.0+
