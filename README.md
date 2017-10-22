# XcodeCodeSnippets
A set of snippets for Xcode.

### Requirements
Xcode 7.3.1 or later.

### Installation
To install or update the snippets you need:
  * Quit Xcode
  * On the command line:
  ```
  git clone https://github.com/ismetanin/XcodeCodeSnippets
mkdir -p $HOME/Library/Developer/Xcode/UserData/CodeSnippets
cp XcodeCodeSnippets/CodeSnippets/* $HOME/Library/Developer/Xcode/UserData/CodeSnippets
rm -rf XcodeCodeSnippets
  ```
  Or if you have a cloned repository:
  * On the command line, cd into the directory with snippets and write `sh ./install.sh`

### List of snippets
#### Comments
* MARK: - Internal methods, `shortcut: Internal methods`
* MARK: - Constants, `shortcut: Constants`
* MARK: - IBOutlets, `shortcut: IBOutlets`
* MARK: - IBActions, `shortcut: IBActions`
* MARK: - Private helpers, `shortcut: Private helpers`
* MARK: - Initialization and deinitialization, `shortcut: Initialization and deinitialization`
* MARK: - Properties, `shortcut: Properties`
* MARK: - NSLayoutConstraints, `shortcut: NSLayoutConstraints`
#### Code
* A template for creating TableViewAdapter, `shortcut: Table View Adapter`
* A code block for creating user property in UserDefaults extension, `shortcut: Defaults Key`
* A code block for layouting child view edges equal to a parent view edges, `shortcut: Constraints - layout child as parent`
* A code block for creating object that implement TableCellGenerator and ViewBuilder protocols, `shortcut: implTableCellGenerator`. For more info about TableCellGenerator and ViewBuilder see [ReactiveDataDisplayManager](https://github.com/LastSprint/ReactiveDataDisplayManager).

### Preview
![ezgif-4-770bdfd9ab](https://user-images.githubusercontent.com/11653316/29164667-ea289d52-7dc8-11e7-99f7-462f7837a7d4.gif)

### Author

iSmetanin, smetanin23@yandex.ru

### License

XcodeCodeSnippets is available under the MIT license. See the [LICENSE](https://github.com/ismetanin/XcodeCodeSnippets/blob/master/LICENSE) file for more info.
