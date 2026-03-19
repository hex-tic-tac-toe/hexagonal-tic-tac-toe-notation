# Hexagonal Tic Tac Toe Notation

<!-- Add description -->

## Version 1

### Grammar

```
<game>        ::=  <metadata>? <turn>*
<metadata>    ::= <data>* ";" "\n"?
<data>        ::= <key> "[" <value> "]"  <- defined in below `Meta Attributes`

<turn>        ::= <coordinate> <coordinate> ";" "\n"?
<coordinate>  ::= "[" <integer> "," <integer> "]"

<integer>     ::= <sign> <digit>
<sign>        ::= "-"?
<digit>       ::= [0-9]*
```

### Example

```
name[GameName 0]platform[WebsiteXY 0]playercross[BlueWhale 0]playercircle[GreenSnake 0]timecontrol[Fischer 60+5]endreason[win]winner[cross]datetime[2026-03-18 23:20:14];[-1,0][0,1];[-1,1][-2,2];[1,-1][-5,5];[-1,2][1,0];[5,0][-3,2];[-2,1][1,2];[0,2][-1,5];[0,3][-1,3];[-2,3][1,3];[0,4][3,0];[-1,4][4,-1];[0,-1][5,-1];[-3,3][-2,5];[-3,5][-1,9];[-4,4][-5,4];[-6,6][-5,3];[-2,4][-3,4];[-6,4][-3,1];[-3,6][-4,7];[-5,8][-2,-1];[-4,2][-7,5];[-2,0][0,5];
```

### Meta Attributes

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

`<timecontrol> ::= <integer> ("+" <integer>)?` is `basetime+increment`
