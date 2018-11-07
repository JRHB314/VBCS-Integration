# rels listed

This page needs one last Service Connection. Create a `Neo4j Relationship List` connection, with the same settings as before except for Request and Response.<br>
<br>
Put in this code for Request:
```
{
 "statements": [
  {
   "statement": "MATCH (users)-[:FOLLOWS]-(userA:Person {name:'YukiTsukino'}) return users.name"
  }
 ]
}
```
Note, the relationship type being returned will be further specified in specific REST calls later. 
And this should be the Response:
```
{
    "results": [
        {
            "columns": [
                "users.name"
            ],
            "data": [
                {
                    "row": [
                        "VelmaGarcia"
                    ],
                    "meta": [
                        null
                    ]
                },
                {
                    "row": [
                        "JohanLitwick"
                    ],
                    "meta": [
                        null
                    ]
                },
                {
                    "row": [
                        "RajeshBishnoi"
                    ],
                    "meta": [
                        null
                    ]
                },
                {
                    "row": [
                        "RajeshBishnoi"
                    ],
                    "meta": [
                        null
                    ]
                },
                {
                    "row": [
                        "BobFlinstone"
                    ],
                    "meta": [
                        null
                    ]
                },
                {
                    "row": [
                        "RachelWebb"
                    ],
                    "meta": [
                        null
                    ]
                }
            ]
        }
    ],
    "errors": []
}
```



