# Hexagonal Tic Tac Toe Notation

<!-- Add description -->

## Version 1

### Grammar

```
<game>        ::=  <metadata>? <turn>*
<metadata>    ::= <data>+ ";"
<data>        ::= <key> "[" <value> "]"  <- defined in below `Meta Attributes`

<turn>        ::= <turn_number> <coordinate> <coordinate> <amount_of_threats>? ";"
<turn_number> ::= <digits> "."
<coordinate>  ::= "[" <integer> "," <integer> "]" 
<amount_of_threats> ::= "!"*

<integer>     ::= <sign> <digits>
<sign>        ::= "-"?
<digits>       ::= [0-9]+
```

- `turn_number` starts with `1.`.
- `amount_of_threats`: each `!` represents a threat. Adding it is optional.
- Whitespace charaters can be added for better readability and can be ignored during parsing (exept `<value>`).


### Example

```
name[GameName 0]platform[WebsiteXY 0]playercross[BlueWhale 0]playercircle[GreenSnake 0]timecontrol[Fischer 60+5]endreason[win]winner[cross]datetime[2026-03-18 23:20:14];
1. [-1,0][0,1];
2. [-1,1][-2,2];
3. [1,-1][-5,5];
4. [-1,2][1,0];
5. [5,0][-3,2];
```

### Meta Attributes

All attributes are optional. Having `version` is strongly recommended.

| Key            | Description                              | Value                                                           |
| -------------- | ---------------------------------------- | --------------------------------------------------------------- |
| `version`      | version of notation                      | integer                                                         |
| `name`         | Display name of the match                | string                                                          |
| `platform`     | Website or app where the game was played | string                                                          |
| `utcdatetime`  | Game start time in UTC                   | ISO 8601: `YYYY-MM-DD HH:MM:SS`                                 |
| `playercross`  | Name of the cross (X) player             | string                                                          |
| `playercircle` | Name of the circle (O) player            | string                                                          |
| `timecontrol`  | Time control format                      | string                                                          |
| `endreason`    | How the game ended                       | string - `win` `time` `resign` `draw`                           |
| `winner`       | Who won                                  | string - `cross` `circle`                                       |


### Moves

The first move is always done by `cross` and is located at `[0,0]` and therefore **never** appears in the list of turns.
All following moves are relative to the first `cross` move, meaning the first recorded turn is made by `circle`.
Each turn must include exactly two coordinates<!-- TODO: (can winning tile be exceptions?) -->.
Move coordinates must follow the [axial coordinate system](https://www.redblobgames.com/grids/hexagons/#:~:text=Axial%20coordinates) and therefore be in the order: `[q, r]`.

![Example Diagram](https://github.com/hex-tic-tac-toe/hexagonal-tic-tac-toe-notation/blob/main/assets/grid-example.png)

### Time Format

Currently supported time controls are:

- Absolute
- Fischer

`<timecontrol> ::= <integer> ("+" <integer>)?` represents `basetime+increment`
