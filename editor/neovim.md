# My (Neo)Vim Commands and Keybindings

## Modes

| Keybinding   | Description |
|--------------|-------------|
|<kbd>ESC</kbd>| Normal mode. |
|<kbd>A</kbd>  | Appending mode. |
|<kbd>I</kbd>  | Insert mode. |
|<kbd>V</kbd>  | Simple visual mode. |
|<kbd>SHIFT</kbd> + <kbd>V</kbd>| Multi-line visual mode. |


## Normal Mode
### Windows
#### Navigation

| Keybinding / Command                           | Description                      |
|------------------------------------------------|----------------------------------|
| <kbd>CTRL</kbd> + <kbd>W</kbd> + <kbd>H</kbd>  | Move to the window to the left.  |
| <kbd>CTRL</kbd> + <kbd>W</kbd> + <kbd>J</kbd>  | Move to the window below.        |
| <kbd>CTRL</kbd> + <kbd>W</kbd> + <kbd>K</kbd>  | Move to the window above.        |
| <kbd>CTRL</kbd> + <kbd>W</kbd> + <kbd>L</kbd>  | Move to the window to the right. |

##### Tabs
| Keybinding / Command                           | Description                      |
|------------------------------------------------|----------------------------------|
| <kbd>G</kbd> + <kbd>T</kbd>                    | Move to the next tab.            |
| <kbd>G</kbd> + <kbd>SHIFT</kbd> + <kbd>T</kbd> | Move to the previous tab.        |
| <kbd>:tabs</kbd>                               | List all tabs.                   |
| <kbd>:tabedit `FILE`</kbd>                     | Open `FILE` in a new tab.        |
| <kbd>:tabfind `FILE`</kbd>                     | Find the tab which holds `FILE`. |
| <kbd>:tabclose</kbd>                           | Close the current tab.           |


##### Splits

| Command                         | Description                                   |
|---------------------------------|-----------------------------------------------|
| <kbd>:res `[+\|-] HEIGHT`</kbd> | Changes the split height to the given `HEIGHT`. If `+` or `-` is given increase / reduce it by height|
| <kbd>:vertical `SPLIT_COMMAND`  | Prefix a `SPLIT_COMMAND` and so it applies to a vertical split. |

### Text
#### Navigation

| Keybinding             | Description                                   |
|------------------------|-----------------------------------------------|
| <kbd>H</kbd>           | Move the cursor to the left.                  |
| <kbd>J</kbd>           | Move the cursor down.                         |
| <kbd>K</kbd>           | Move the cursor up.                           |
| <kbd>L</kbd>           | Move the cursor to the right.                 |
| <kbd>$</kbd>           | Move the cursor to the end of the line.       |  


#### Manipulation

| Command / Keybinding       | Description                                   |
|----------------------------|-----------------------------------------------|
| <kbd>:m `TARGETLINE`</kbd> | Moves the current line below the `TARGETLINE`.  |
| <kbd>X</kbd>               | Delete character under the cursor.            |


## Nerd-Tree

| Keybinding                      | Description                    |
|---------------------------------|--------------------------------|
|  <kbd>O</kbd>                   | open in prev window            |
| <kbd>G</kbd> + <kbd>O</kbd>     | preview                        |
| <kbd>T</kbd>                    | open in new tab                |
| <kbd>SHIFT</kbd> + <kbd>T</kbd> | open in new tab silently       |
| <kbd>I</kbd>                    | open split                     |
| <kbd>G</kbd> + <kbd>I</kbd>     | preview split                  |
| <kbd>S</kbd>                    | open vsplit                    |
| <kbd>G</kbd> + <kbd>S</kbd>     | preview vsplit                 |
