# LAMS
LAMS, the Learning Activity Management System, is an open source Learning Design system for designing, managing and delivering online collaborative learning activities. Publicly available learning designs have been downloaded from [LAMS](https://lamscommunity.org/register/?return%5furl=%2fdotlrn%2findex) official website, analyzed and stored in a relational database.

### Storage 
The RDBMS [PostgreSQL](https://www.postgresql.org/) has been used to store the instructional design sequences. The database can be reproduced using the [lamsdb.dump](https://github.com/fanagnou/LAMS/blob/master/lamsdb.dump) file.
To reconstruct the database type in the PostgreSQL interactive terminal : 

```bash
$ pg_dump db_name < lamsdb.dump
```

### Structure
LAMS learning designs are represented as sequences of learning activities and are stored in XML files. Learning activities can be either simple or complex. The complex activities are used to describe the construction of sub-sequences of activities within an instructional design. A common example that causes the creation of nested sub-sequences is the division of the Learners into groups where each group has to complete different tasks. The most common example of simple activities are the Tools, which are self-contained modules that form most of the "functionality" that the Learner interacts with in LAMS. Each Tool links to an another XML file which includes the attributes and the content of the module. More information about the LAMS Tool Activities can be found in [lams activities](https://wiki.lamsfoundation.org/display/lamsdocs/Activities). All the possible activity types and the rest attributes of a learning activity are described in the java class [Activity.java](https://github.com/lamsfoundation/lams/blob/master/lams_common/src/java/org/lamsfoundation/lams/learningdesign/Activity.java) can be found.
<br>
#### Complex Activities:
<ul>
    <li>FLOATING_ACTIVITY_TYPE: It ts used to initialize a sequence. Some learning designs might include a mini complementary sequence</li>
</ul>
