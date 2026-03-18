# Hexagonal Tic Tac Toe Notation

<!-- Add description -->

## Version 1

### Grammar

```
<game>        ::=  <metadata>? "\n"? <turn>*
<metadata>    ::= <data>* ";"
<data>        ::= <key> "[" <value> "]"
<key>         ::= <string>
<value>       ::= <version>
                | <datetime>
                | <timecontrol>
                | <string> <integer>
                | <string>
                

<turn>        ::= <coordinate> <coordinate> ";" "\n"?
<coordinate>  ::= "[" <integer> "," <integer> "]"

<version> ::= <digit>
<timecontrol> ::= <string> <integer> ("+" <integer>)?
<datetime> ::= <digit> "-" <digit> "-" <digit> " " <digit> ":" <digit> ":" <digit> 

<string>      ::= ([a-z] | [A-Z])*
<integer>     ::= <sign> <digit>
<sign>        ::= "-"?
<digit>       ::= [0-9]*
```

### Example

```
name[GameName 0]platform[WebsiteXY 0]playercross[BlueWhale 0]playercircle[GreenSnake 0]timecontrol[Fischer 60+5]endreason[win]winner[cross];[-5,1][-1,-1];[-2,-1][-3,-1];
```

### Meta Attributes

| Key            | Description                              | Options / Format                                                |
| -------------- | ---------------------------------------- | --------------------------------------------------------------- |
| `version`      | version of notation                      | —                                                               |
| `name`         | Display name of the match                | —                                                               |
| `platform`     | Website or app where the game was played | —                                                               |
| `utcdatetime`  | Game start time in UTC                   | ISO 8601: `YYYY-MM-DD HH:MM:SS`                                 |
| `playercross`  | Name of the cross (X) player             | —                                                               |
| `playercircle` | Name of the circle (O) player            | —                                                               |
| `timecontrol`  | Time control format                      | Fischer `Fischer 60+5`, sudden death `60`                       |
| `endreason`    | How the game ended                       | `win` `time` `resign` `forfeit` `draw`                          |
| `winner`       | Who won                                  | `cross` `circle` — omit on draw                                 |


### Moves

The first move is always done by `cross` and is located at `[0,0]` and therefore **never** appears in the list of turns.
All following moves are relative to the first `cross` move, meaning the first recorded turn is made by `circle`.
Each turn must include exactly two coordinates<!-- TODO: (can winning tile be exceptions?) -->.
Move coordinates must follow the [axial coordinate system](https://www.redblobgames.com/grids/hexagons/#:~:text=Axial%20coordinates) and therefore be in the order: `[q, r]`.

#### Time Format

**Currently supported time controls are:**
- Absolute
- Fischer

`<timecontrol> ::= <integer> ("+" <integer>)?` is `basetime+increment`
 Untimed games omit the `timecontrol` key entirely.
