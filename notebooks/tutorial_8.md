# JDBC Exercise

**1. Log in to `dbsrv1`.**

```bash
ssh -i ~/.ssh/id_rsa -o IdentitiesOnly=yes {username}@dbsrv1.cdf.utoronto.ca
```

**2. Create a directory to work in and go there.**

```bash
mkdir -p jdbc-practise
cd jdbc-practise
```

**3. Copy the required files.**

```bash
cp ~csc343h/fall/public_html/in_class/w6/code/* .
```

```bash
$ ls
Example.java  jelly-beans.sql
```

**4. Connect to postgreSQL.**

```bash
psql csc343h-$(id -un)
```

**5. Import `jelly-beans.sql`.**

```psql
=> \i jelly-beans.sql  
CREATE TABLE
INSERT 0 11
```

**6. Look around.**

```psql
=> \d
          List of relations
 Schema |  Name   | Type  |  Owner   
--------+---------+-------+----------
 public | guesses | table | t4stroka
(1 row)
```

```psql
=> select * from guesses;
 number |   name    | guess | age 
--------+-----------+-------+-----
      1 | Cole      |   365 |   5
      2 | Avery     |   585 |   5
      3 | Sam       |   502 |  12
      4 | Madeleine |   511 |  18
      5 | Cole      |   450 |   5
      6 | Michael   |  1000 |  12
      7 | Mackenzie |   700 |   5
      8 | Mackenzie |   701 |   5
      9 | Micah     |   498 |   4
     10 | Jiaqi     |   509 |   4
     11 | Jamieson  |   502 |   6
(11 rows)
```

```psql
=> select * from guesses where age > 10;
 number |   name    | guess | age 
--------+-----------+-------+-----
      3 | Sam       |   502 |  12
      4 | Madeleine |   511 |  18
      6 | Michael   |  1000 |  12
(3 rows)
```

```psql
=> \q
```

**7. & 8. Get your bearings in the code.**

I used vim, but you may favour some other editor.  Then put your cdf username in the two spots in place of mine.

```bash
vim Example.java
```

**9. Compile.**

```bash
javac Example.java
```

**10. And run -- Ta-da!  You have connected Java to SQL.**

```bash
# $ java -cp /local/packages/jdbc-postgresql/postgresql-42.2.4.jar: Example
$ export CLASSPATH=/local/packages/jdbc-postgresql/postgresql-42.2.4.jar:
$ java Example
Cole guessed 365
Avery guessed 585
Cole guessed 450
Mackenzie guessed 700
Mackenzie guessed 701
Micah guessed 498
Jiaqi guessed 509
Jamieson guessed 502
Look up who? 
Mackenzie
   Mackenzie guessed 700
   Mackenzie guessed 701
```

----

## Notes

Create ssh tunnel to database.

```bash
ssh -i ~/.ssh/id_rsa -o IdentitiesOnly=yes -nNL 5432:localhost:5432 {username}@dbsrv1.cdf.utoronto.ca
```
