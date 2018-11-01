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
We are creating two users, identified by userA and userB, of type Person, named A and B respectively. Then we create a relationship identified by "follows" of type FOLLOWS between userA and userB.
