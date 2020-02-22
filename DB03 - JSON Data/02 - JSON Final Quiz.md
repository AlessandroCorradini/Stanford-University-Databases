# JSON Final Quiz

Each multiple-choice quiz problem is based on a "root question," from which the system generates different correct and incorrect choices each time you take the quiz. Thus, you can test yourself on the same material multiple times. We strongly urge you to continue testing on each topic until you complete the quiz with a perfect score at least once. Simply click the "Reset" button at the bottom of the page for a new variant of the quiz.

After submitting your selections, the system will score your quiz, and for incorrect answers will provide an "explanation" (sometimes for correct ones too). These explanations should help you get the right answer the next time around. To prevent rapid-fire guessing, the system enforces a minimum of 10 minutes between each submission of solutions.

## Multiple Choice

### [Q1] Which of the following is NOT a valid JSON object?

```
{ "name": "Smiley",
  "age": 20,
  "phone": { "888-123-4567", "888-765-4321" },
  "email": "smiley@xyz.com",
  "happy": true }  [X]
```

```
{ "name": "Smiley",
  "age": 20,
  "phone": null,
  "email": null,
  "happy": true }
```

```
{ "name": "Smiley",
  "age": 20,
  "phone": "888-123-4567",
  "email": "smiley@xyz.com",
  "happy": "true" }
```

```
{ "name": "Smiley",
  "age": 20,
  "phone": "888-123-4567",
  "email": "smiley@xyz.com",
  "happy": true }
```

### [Q2] Which of the following is NOT a valid JSON array?

```
[ 1, 2, "dog", "cat", true, false, [],
  {"pet":"dog", "fun":true} ]
```

```
[ 1, 2, "dog", "cat", true, false, [1, "dog", null], {} ]
```

```
[ 1, 2, "dog", "cat", true, false, [1, "dog", null],
  {"pet":"dog", "fun":true} ]
```

```
[ 1, 2, dog, cat, true, false, [1, "dog", null],
  {"pet":"dog", "fun":true} ] [X]
```

### [Q3] Consider the following JSON Schema specification:

```
{
  "type": "object",
  "properties":
    { "ItemID": { "type":"string", "pattern":"Item*" },
      "ItemName": { "type":"string" },
      "Price": { "type":"integer", "minimum":10, "maximum":100 },
      "Sellers": { "type":"array", "maxItems":3,
                   "items": { "type":"string" }},
      "Ratings": { "type":"array",
                   "items":
                      { "type": "object",
                        "properties": {"Rater":
                                       {"type": "string", "optional": true},
                                       "Score":
                                       {"type": "integer", "minimum":1,
                                        "maxiumum":5}}}},
      "AvgRating": { "type":"number", "optional":true },
      "FreeShipping": {"type":"boolean" }
    }
}
```

Select, from the choices below, the JSON data that is valid according to the JSON Schema specification above.


```
{ "ItemID": "Item123",
  "ItemName": "desk",
  "Price": 50,
  "Sellers": ["Amy","Ben"],
  "Ratings": {"Rater":"Amy", "Score":5},
  "AvgRating": 3.33,
  "FreeShipping": true }
```
```
{ "ItemID": "Item123",
  "ItemName": "desk",
  "Price": "50",
  "Sellers": ["Amy","Ben"],
  "Ratings": [{"Rater":"Amy", "Score":5}, {"Score":1},
              {"Rater":"Carl", "Score":4}],
  "AvgRating": 3.33,
  "FreeShipping": true }
```
```
{ "ItemID": "Item123",
  "ItemName": "desk",
  "Price": 50,
  "Sellers": ["Amy","Ben"],
  "Ratings": [{"Rater":"Amy", "Score":5}, {"Score":1},
              {"Rater":"Carl", "Score":4}],
  "AvgRating": 3.33,
  "FreeShipping": [true] }
```
```
{ "ItemID": "Item123",
  "ItemName": "desk",
  "Price": 50,
  "Sellers": [ ],
  "Ratings": [{"Rater":"Amy", "Score":5}, {"Score":1},
              {"Rater":"Carl", "Score":4}],
  "AvgRating": 3.33,
  "FreeShipping": true } [X]
```

[Q4] Consider the following JSON data:

```
{ "A": [1,1,2,2], "B": {"C":3, "D":4}, "E":[5,6,true], "F": {"G": [null,7]} }
```

Which of the following could NOT be included as part of a JSON Schema specification that is satisfied by the JSON data above? Assume that every letter ("A", "B", "C", ...) appears in the JSON Schema specification exactly once.

```
"B": {"type":"object",
      "properties": {"C": {"type":"integer"},
                     "D": {"type":"integer"}}}
```
```
"A": {"type":"array", "maxItems":10, 
      "items":{"type":"integer"}}
```
```
"F": {"type":"object",
      "properties": {"G": {"type":"array",
                           "items": {"type":["null","integer"]}}}}
```
```
"B": {"type":"object", "additionalProperties":false,
      "properties": {"C": {"type":"integer"}}}      [X]
```