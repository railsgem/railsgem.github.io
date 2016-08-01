---
layout: post
title:  "Database system review"
date:   2016-04-14 09:15:09 +1100
categories: Database
---

#目录

* 目录
{:toc}

## 1.Relational Algebra


### 1.1 [PPT](http://120.105.184.250/lwcheng/ppt/kidpps/CHAP05.pdf)

#### 1.1.1 selection 

{% highlight sql %}
  select * from table_a where condition = conditionA.

{% endhighlight %}

It means SELECT something from table_a where **satisfy the conditionA**.


#### 1.1.2 projection 

{% highlight sql %}
  select column_a, columa_b from table_a .


{% endhighlight %}
It means SELECT <strong>COLUMNS<strong> from table_a .

#### 1.1.2 Intersection 

{% highlight sql %}
 table_a intersection table_b
{% endhighlight %}

table_a and table_b must have **same columns and in same order**.
Intersection is to pick out the same tuples both in table_a and table_b.

#### 1.1.3 Join 

{% highlight sql %}
 
slect * from a left join b on a.coulumn = a.column;

{% endhighlight %}

table_a and table_b must have **same columns and in same order**.
Intersection is to pick out the same tuples both in table_a and table_b.

#### 1.1.4 Division 

![alt text]({{ site.baseurl }}/images/QQ20160414-0@2x.png "Logo Title Text 1")

>	REFRENCES:  

>	http://120.105.184.250/lwcheng/ppt/kidpps/CHAP05.pdf
