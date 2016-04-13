---
layout: post
title:  "SQL View cannot contain a subquery?!"
date:   2016-03-16 08:15:09 +1100
categories: Database
---
* 目录
{:toc}

There are two situations:

- **1. BUG？**

Actually,in Oracle Database, View can contain a sub-query.

However,in MYSQL5, there is a [bug](http://bugs.mysql.com/bug.php?id=16757), you cannot use sub-query in a from clause.
‌
{% highlight ruby %}
[24 Jan 2006 21:19] Neil Pierson
Description:
As you are already aware, 
"mysql> CREATE VIEW v3 AS SELECT * FROM 
-> (SELECT s1 FROM t1) AS x; 
ERROR 1349 (HY000): View's SELECT contains a subquery in the FROM clause 
You can't create a view if the view's SELECT definition has a FROM clause that contains a subquery. This restriction is a flaw."

The removal of this restriction would be *greatly* appreciated!

How to repeat:
CREATE VIEW v3 AS SELECT * FROM (SELECT s1 FROM t1) AS x;

Suggested fix:
I was sorta hoping you guys could fix it.
{% endhighlight %}

- **2. UPDATE VIEW**

The SQL UPDATE VIEW command can be used to modify the data of a view.

All views are not updatable. So, UPDATE command is not applicable to all views. An updatable view is one which allows performing an UPDATE command on itself without affecting any other table.

When a view can be updated?

  1. The view is defined based on one and only one table.
  2. The view must include the PRIMARY KEY of the table based upon which the view has been created.
  3. The view should not have any field made out of aggregate functions.
  4. The view must not have any DISTINCT clause in it's definition.
  5. The view must not have any GROUP BY or HAVING clause in it's definition.
  6. The view must not have any SUBQUERIES in it's definitions.
  7. If the view you want to update is based upon another view, the later should be updatable.
  8. Any of the selected output fields (of the view) must not use constants, strings or value expressions.

>[bug]:http://bugs.mysql.com/bug.php?id=16757

[bug]:http://bugs.mysql.com/bug.php?id=16757

