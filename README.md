# LAMS
LAMS, the Learning Activity Management System, is an open source Learning Design system for designing, managing and delivering online collaborative learning activities. Publicly available learning designs from [LAMS Community](https://lamscommunity.org/register/?return%5furl=%2fdotlrn%2findex) have been analyzed and stored in a database that can be easily queried to get instructional insights.

## Storage
[PostgreSQL](https://www.postgresql.org/) RDBMS has been used to store the learning design sequences. The database can be reproduced using the [lamsdb.dump](https://github.com/fanagnou/LAMS/blob/master/lamsdb.dump) file.
To reproduce the database, type in the PostgreSQL interactive terminal:

```bash
$ pg_dump db_name < lamsdb.dump
```

## Structure
LAMS learning designs are represented as Sequences of Learning Activities. Activities mostly pertain to Tools, which are self-contained modules that form most of the "functionality" that the Learner interacts with in LAMS, and the remaining activities have organisational puproses. Activities are divided into simple and complex. Simple activities include Tools, Groupings of learners or Gates that control the flow of sequence, whereas complex activities are used to describe the insertion of sub-sequences within an instructional design. A common example that causes the creation of nested sub-sequences is the division of the Learners into groups where each group has to complete different tasks. More information about the LAMS Tool Activities can be found in [lams activities](https://wiki.lamsfoundation.org/display/lamsdocs/Activities). All the possible activity types and the rest attributes of a learning activity are described in the java class [Activity.java](https://github.com/lamsfoundation/lams/blob/master/lams_common/src/java/org/lamsfoundation/lams/learningdesign/Activity.java).
<br>
#### Complex Activities
Complex Activities can refer to branchings of the main learning sequence, tasks that need to be done in parallel or optional activities. Some special cases are the following:
<ul>
    <li>FLOATING_ACTIVITY_TYPE: It ts used to initialize a learning sequence. Some learning designs might also contain a separate floating activity which can provide complementary information such as teacher notes or study content</li>
    <li>SEQUENCE_ACTIVITY_TYPE: This is an auxiliary type used to represent the connection between a complex activity and the sub-sequences it produces</li>
</ul>
Activities of type PARALLEL_ACTIVITY_TYPE, OPTIONS_ACTIVITY_TYPE or FLOATING_ACTIVITY_TYPE cause sub-sequences that consists only of a single Tool activity in contrast to the rest of the complex activity types that can produce longer sub-sequences.

