---
date: 2021-09-19
layout: post
slug: 
title: "Finding the PL/Python Path for your PostgreSQL Server"
categories:
- PosgreSQL
tag:
- postgres 
- plpython
- python
---

If you need to get the python path used by plpython you can create a new function that prints out the system paths. 

To get started, create a function called `python_path` or whatever you want to call it:

~~~sql
CREATE FUNCTION python_path ()
    RETURNS text[]
AS $$
    import sys
    return [p for p in sys.path]
$$ LANGUAGE plpython3u;
~~~

Now you can the paths by running a select query with the function:

~~~sql
SELECT UNNEST(python_path());
~~~

For me the output looks like this:

![image](https://user-images.githubusercontent.com/10215346/133931582-f9ae1bb9-bf70-4acf-b042-c159fc25092f.png)
