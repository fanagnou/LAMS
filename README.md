# LAMS
LAMS, the Learning Activity Management System, is an open source Learning Design system for designing, managing and delivering online collaborative learning activities. Publicly available learning designs from [LAMS Community](https://lamscommunity.org/register/?return%5furl=%2fdotlrn%2findex) have been analyzed and stored in a database that can be easily queried to get instructional insights.

## Design Structure
LAMS learning designs are represented as Sequences of Learning Activities. Activities mostly pertain to Tools, which are self-contained modules that form most of the "functionality" that the Learner interacts with in LAMS, and the remaining activities have organizational purposes. Activities are divided into simple and complex. Simple activities include Tools, Groupings of learners or Gates that control the pace of the lesson, whereas complex activities are used to describe the insertion of sub-sequences within an instructional design. A common example that causes the creation of nested sub-sequences is the division of the Learners into groups where each group has to complete different tasks. More information about the LAMS Tool Activities can be found in [lams activities](https://wiki.lamsfoundation.org/display/lamsdocs/Activities). All the possible activity types and the rest attributes of a learning activity are described in the java class [Activity.java](https://github.com/lamsfoundation/lams/blob/master/lams_common/src/java/org/lamsfoundation/lams/learningdesign/Activity.java).
<br>
#### Complex Activities
Complex Activities can refer to branchings of the main learning sequence, tasks that need to be done in parallel or optional activities. Some special cases are the following:
<ul>
    <li>FLOATING_ACTIVITY_TYPE: Refers to the [Support Activities](https://wiki.lamsfoundation.org/display/lamsdocs/Support+Activities) which are tasks that do not have to be completed in order to Finish a lesson.</li>
    <li>SEQUENCE_ACTIVITY_TYPE: This is an auxiliary type used for representing the sub-sequences created within a learning design by a complex activity </li>
</ul>
Activities of type PARALLEL_ACTIVITY_TYPE, OPTIONS_ACTIVITY_TYPE or FLOATING_ACTIVITY_TYPE cause sub-sequences that consists only of a single Tool activity in contrast to the rest of the complex activity types that can produce longer sub-sequences.

## Database Storage
[PostgreSQL](https://www.postgresql.org/) DBMS has been used to store the learning design sequences. The database can be reproduced using the [lamsdb.dump](https://github.com/fanagnou/LAMS/blob/master/lamsdb.dump) file.
To reproduce the database, type in the PostgreSQL interactive terminal:

```bash
$ pg_dump db_name < lamsdb.dump
```
#### DB Tables
<ul>
    <li> sequences(id, title, user_id, length, total_activities)</li>
    <li>activities(id, sequence_id, type, title, subsequences)</li>
    <li>activities_info(id, sequence_id, type,  data)</li>
    <li>subsequences(id, sequence_id, parent_id, activities, main)</li>
</ul>

Learning designs are stored in the table sequences and the lenght attribute refers to the main sequence of the lesson as this is displayed in the preview mode of LAMS design. In table subsequences, both the main sequence and the sub-sequences of a lesson  are stored. The parent_id refers to the complex activity that causes the creation of the a sub-sequence ad it is used for retrieving all the possible paths within a lesson without requiring joins with other tables. Information about the Learning activities is stored in the remaining tables. The activities_info table is used for storing the content Tool Activities in jsonb datatype.

#### Statistics


|              type              | frequency|
--------------------------------|-----------
| TOOL_ACTIVITY_TYPE             |     15964|
| GROUPING_ACTIVITY_TYPE         |       652|
| PERMISSION_GATE_ACTIVITY_TYPE  |       467|
| PARALLEL_ACTIVITY_TYPE         |       368|
| TOOL_BRANCHING_ACTIVITY_TYPE   |       166|
| GROUP_BRANCHING_ACTIVITY_TYPE  |       153|
| OPTIONS_ACTIVITY_TYPE          |       141|
| CHOSEN_BRANCHING_ACTIVITY_TYPE |       123|
| SYNCH_GATE_ACTIVITY_TYPE       |        94|
| FLOATING_ACTIVITY_TYPE         |        68|
| SCHEDULE_GATE_ACTIVITY_TYPE    |        39|
| CONDITION_GATE_ACTIVITY_TYPE   |        34|
| OPTIONS_WITH_SEQUENCES_TYPE    |        29|
   
Most common tool types and their frequency



