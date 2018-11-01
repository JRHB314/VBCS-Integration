<h2> Lab 500: Connecting VBCS to GrapheneDB Database </h2>

Graph databases are...

1. Set up GrapheneDB Database

create account<br>
create database<br>
hobby sandbox<br>
Name database<br>
leave other defaults<br>
hit create database<br>
open neo4j browser<br>
Neo4j uses [Cypher](https://neo4j.com/developer/cypher-query-language/) to code. Read up on it if you want to know more.<br>
Here are some basic concepts:<br>
-It's meant to resemble ascii art<br>
-Nodes are surrounded by parantheses to resemble circles<br>
-Relationships are described in arrows<br>
```
CREATE (nodeA)
CREATE (nodeB)
CREATE (nodeA)-[realtionship:TYPE]->(nodeB)
```
We can add properties to these nodes and relationships. Go to the tob of the browser tool, copy and paste this code, then hit run.
```
CREATE (userA:Person {name:"A"})
CREATE (userB:Person {name:"B"})
CREATE (userA)-[follows:FOLLOWS]->(userB)
return userA, userB, follows
```
We are creating two users, identified by userA and userB, of type Person, named A and B respectively. Then we create a relationship identified by "follows" of type FOLLOWS between userA and userB.<br>
Now try running this code:
```
CREATE (userC:Person {name:"C"})
CREATE (userA)-[follows:FOLLOWS]->(userC)
return userA, userC, follows
```
Note that A comes up blank. Because we created A in a previous statement, it no longer knows what we mean by userA. We have to go find userA and userC in order to continue using them. <br>

```
MATCH (userA:Person {name:"A"})
MATCH (userC:Person {name:"C"})
CREATE (userA)-[follows:FOLLOWS]->(userC)
return userA, userC, follows
```
However, notice that blank node is still following C! To get rid of it, hover over it and mark down it's id number. 
Run this code:
```
MATCH (n) where id(n) = # DETACH DELETE n
```
But be sure to replace "#" with the id you marked down. This deletes the node and detaches it, that is, deletes all of its relationships.<br>
Run this code to see all of our nodes so far:
```
START n=node(*) MATCH (n)-[r]->(m) RETURN n,r,m; //show all nodes and relationships
```
Now, let's say C has 5 followers. That quickly becomes tedious to code individually, so we can use a FOREACH loop.
```
MATCH (userC:Person {name:"C"})
FOREACH (name in ["follower1","follower2","follower3","follower4","follower5"] |
  CREATE (:Person {name:name})-[:FOLLOWS]->(userC))
```
Then to display all of C's followers:
```
MATCH (cFollowers)-[:FOLLOWS]->(userC:Person {name:"C"})
RETURN userC, cFollowers
```


<br><br><br>
```
MATCH (n) OPTIONAL MATCH (n)-[r]-() DELETE n,r //clear all nodes and relationships
```
