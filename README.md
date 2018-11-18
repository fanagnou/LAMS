# LAMS
LAMS, the Learning Activity Management System, is an open source Learning Design system for designing, managing and delivering online collaborative learning activities. Publicly available learning designs have been downloaded from [LAMS](https://lamscommunity.org/register/?return%5furl=%2fdotlrn%2findex) official website, analyzed and stored in a relational database.

### Storage 
The RDBMS [PostgreSQL](https://www.postgresql.org/) has been used to store the instructional design sequences. The database can be reproduced using the [lamsdb.dump](https://github.com/fanagnou/LAMS/blob/master/lamsdb.dump) file.
To reconstruct the database type in the PostgreSQL interactive terminal : 

```bash
$ pg_dump db_name < lamsdb.dump
```

### Structure 
Learning Design are represented as sequences of learning activities.


