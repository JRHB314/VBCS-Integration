

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

Now, our final set of variables.<br>

- getFollowersPt1 `{ "statements": [ { "statement": "MATCH (followers)-[:FOLLOWS]->(user:Person {name: '`
- getFollowersPt2 `' }) return followers"  } ]}`
- getFollowingPt1 `{  "statements": [   {    "statement": "MATCH (following)<-[:FOLLOWS]-(user:Person {name:'`
- getFollowingPt2 `'}) return following"   }  ] }`
- getMutualsPt1 `{  "statements": [   {    "statement": "MATCH (user:Person {name:'`
- getMutualsPt2 `'})-->(mutuals)-->(user) return mutuals"   }  ] }`

We're almost there, we just need to set up our Action Chains.<br>
<br>
Let's start with `loadFollowers`. First action will be Assign Variables. Click on `title` on the right. Fill in the bottom box with `"Followers"`. It will automatically add double curly brackets around the value.<br>
{img}<br>
<br>
Next, Call REST Endpoint. Select  `Neo4j Relations List`, then map the request body:<br>
{img}<br>
<br>
Drag and Drop a For Each action. Map its `items` array to the REST endpoint's `data` array. <br>
{img}<br>
<br>
For each element in `data` the loop will run. <br>
<br> Now we need to add one more piece of logic, an If action to check whether or not we are on the first element in data. This is because what we will do next is append each follower name to our `relationsList` string. That is,<br>
`relationsList = follower1 + follower2 + follower3...`<br>
But if we simply always append to the end of relationsList, when we pull up the next list, say of mutuals, it'll display:<br>
`relationsList = follower1 + follower2 + follower3... + mutual1 + mutual2...`<br>
Instead of what we want,<br>
`relationsList = mutual1 + mutual2...`<br>
So, for the first element of the list, we should overwrite the `relationsList` variable, rather than append to the end of it.<br>
