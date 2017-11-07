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
* // MARK: - Internal methods, `shortcut: Internal methods`
* // MARK: - Constants, `shortcut: Constants`
* // MARK: - IBOutlets, `shortcut: IBOutlets`
* // MARK: - IBActions, `shortcut: IBActions`
* // MARK: - Private helpers, `shortcut: Private helpers`
* // MARK: - Initialization and deinitialization, `shortcut: Initialization and deinitialization`
* // MARK: - Properties, `shortcut: Properties`
* // MARK: - NSLayoutConstraints, `shortcut: NSLayoutConstraints`
#### Code
* A template for creating TableViewAdapter, `shortcut: Table View Adapter`
  <details>
  <summary>Code</summary>
  <br>

   ```
   import UIKit

   protocol <#Your#>ViewAdapterOutput {
   }

   final class <#Your#>TableViewAdapter: NSObject {

       // MARK: - Constants

       fileprivate let output: <#Your#>ViewAdapterOutput

       // MARK: - Properties

       fileprivate var items: [<#ItemsType#>]
       fileprivate (set) var tableView: UITableView {
           didSet {
               tableView.register(UINib(nibName: <#CellName#>, bundle: nil), forCellReuseIdentifier: <#CellName#>)
           }
       }

       // MARK: - Initialization and deinitialization

       init(output: <#Your#>ViewAdapterOutput) {
           self.output = output
       }

       // MARK: - Internal helpers

       func set(tableView: UITableView) {
           self.tableView = tableView
       }

       func configure(with items: <#ItemsType#>) {
           self.items = items
      }

   }


   // MARK: - UITableViewDataSource

   extension <#Your#>TableViewAdapter: UITableViewDataSource {
       func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
           return items.count
       }

       func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
           let cell = UITableViewCell()
           return cell
       }
   }


   // MARK: - UITableViewDelegate

   extension <#Your#>TableViewAdapter: UITableViewDelegate {
       func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
           tableView.deselectRow(at: indexPath, animated: true)
       }
   }
   ```
  </details>
* A code block for creating user property in UserDefaults extension, `shortcut: Defaults Key`
  <details>
  <summary>Code</summary>
  <br>

   ```
    var <#defaultsKey#>: <#Type#> {
        get { return <#typeof#>(forKey: #function) }
        set { set(newValue, forKey: #function) }
    }
   ```
  </details>
* A code block for layouting child view anchors equal to a parent view anchors, `shortcut: Constraints - layout child as parent`
  <details>
  <summary>Code</summary>
  <br>

   ```
    <#childView#>.translatesAutoresizingMaskIntoConstraints = false

        NSLayoutConstraint.activate([
            <#childView#>.topAnchor.constraint(equalTo: <#parentView#>.topAnchor, constant: 0),
            <#childView#>.bottomAnchor.constraint(equalTo: <#parentView#>.bottomAnchor, constant: 0),
            <#childView#>.leadingAnchor.constraint(equalTo: <#parentView#>.leadingAnchor, constant: 0),
            <#childView#>.trailingAnchor.constraint(equalTo: <#parentView#>.trailingAnchor, constant: 0)
            ])
   ```
  </details>
* A code block for creating object that implement TableCellGenerator and ViewBuilder protocols, `shortcut: implTableCellGenerator`. For more info about TableCellGenerator and ViewBuilder see [ReactiveDataDisplayManager](https://github.com/LastSprint/ReactiveDataDisplayManager).
  <details>
  <summary>Code</summary>
  <br>

   ```
    class <#name#>Generator {

        // MARK: - Events

        <#events declarations#>

        // MARK: - Stored properties

        fileprivate let model: <#model type#>

        // MARK: - Initializers

        public init(model: <#model type#>) {
            self.model = model
        }
    }

    // MARK: - TableCellGenerator

    extension <#name#>Generator: TableCellGenerator {

        var identifier: UITableViewCell.Type {
            return <#cell type#>.self
        }

        func generate(tableView: UITableView, for indexPath: IndexPath) -> UITableViewCell {

            guard let cell = tableView.dequeueReusableCell(withIdentifier: self.identifier.nameOfClass, for: indexPath) as? <#cell type#> else { return UITableViewCell() }

            self.build(view: cell)

            return cell
        }
    }

    // MARK: - ViewBuilder

    extension <#name#>Generator: ViewBuilder {

        func build(view: <#cell type#>) {
            <#code for building cell#>
        }
    }
   ```
  </details>

### Preview
![ezgif-4-770bdfd9ab](https://user-images.githubusercontent.com/11653316/29164667-ea289d52-7dc8-11e7-99f7-462f7837a7d4.gif)

### Author

Ivan Smetanin, smetanin23@yandex.ru

### License

XcodeCodeSnippets is available under the MIT license. See the [LICENSE](https://github.com/ismetanin/XcodeCodeSnippets/blob/master/LICENSE) file for more info.
