# Hexagonal Tic Tac Toe Notation

<!-- Add description -->

## Version 1

### Example

```json
{
  "metadata": {
    "name": "Game Name",
    "platform": "Website XY",
    "utc_datetime": "YYYY-MM-DDTHH:MM:SSZ",  // ISO 8601
    "player_cross": "Blue Whale",
    "player_circle": "Green Snake",
    "time_control": "10+5",      
    "end_reason": "win",            
    "winner": "cross"               
  },
  
  "moves": [
    [[0, 0],[-1, -1]], // Circle
    [[-2, -1],[-3,-1,]], // Cross
    ...
  ]
}
```

### Meta Attributes

| Variable        | Type          | Description                              | Options / Format                                                 |
| --------------- | ------------- | ---------------------------------------- | ---------------------------------------------------------------- |
| `name`          | string / null | Display name of the match                | —                                                                |
| `platform`      | string / null | Website or app where the game was played | —                                                                |
| `utc_datetime`  | string        | Game start time in UTC                   | ISO 8601: `YYYY-MM-DDTHH:MM:SSZ`                                 |
| `player_cross`  | string        | Name of the cross (X) player             | —                                                                |
| `player_circle` | string        | Name of the circle (O) player            | —                                                                |
| `time_control`  | string / null | Time control format                      | Fischer `"10+5"`, sudden death `"60"`, untimed `null` in seconds |
| `end_reason`    | string        | How the game ended                       | `"win"` `"time"` `"resign"` `"forfeit"` `"draw"`                 |
| `winner`        | string / null | Who won                                  | `"cross"` `"circle"` `null` (draw)                               |


### Moves

The first move is always done by `cross` and is located at `[0,0]` and therefore **never** appears in the list of `"moves"`. 
All following moves are relative to the first `cross` move.
All turn must include exactly two coordinates<!-- TODO: (can winning tile be exeptions?) -->.
Moves coordinates must follow the [axial coordinate system](https://www.redblobgames.com/grids/hexagons/#:~:text=Axial%20coordinates) and therefore be in the order: `[q, r]`.


#### Time Format

**Current supported time controls are:**
- Absolute
- Fischer
- Untimed

Time format is defined with the following grammer:

```
<time_control> ::= <main>"+"<increment>
<main>         ::= { <digit> }
<increment>    ::= { <digit> }
<digit>        ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
```

Both `<main>` and `increment` are in seconds.
