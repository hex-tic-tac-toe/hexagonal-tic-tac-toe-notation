# Hexagonal Tic Tac Toe Notation


## Version 1

```json
{
  "metadata": {
    "name": "Game Name",
    "place": "Website XY", // TODO: could have another variable name
    "utc_datetime": "YYYY-MM-DD HH:MM:SS",
    "player_cross": "Blue Wale",
    "player_circle": "Green Snake",
    "time_control": "10s+5s", // TODO: (example fischer) finding example for other formats should be easy
    "end_reason": ""  // TODO: [win (6 in a row),time,resign,forfeit]??,
    "winner": "cross" || "circle"
  },
  // Cross starts first and always plays on [0,0] and sets the anchor for all following moves relative to [0,0]
  "moves": [
    [-1,-1], 
    [-2,-1],
    ...
  ]
}
```

### Meta Attributes

| Variable | Type   | Options | 
| -------- | ------ | ------- | 
| name     | string | -       |
