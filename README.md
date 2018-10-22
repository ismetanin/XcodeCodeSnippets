[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
# XcodeCodeSnippets
A set of snippets for Xcode.

### Requirements
Xcode 7.3.1 or later.

### Installation
To install or update the snippets you need:
  * Quit Xcode
  * On the command line:
  ```
  cd ~/Downloads
  git clone https://github.com/ismetanin/XcodeCodeSnippets
mkdir -p $HOME/Library/Developer/Xcode/UserData/CodeSnippets
cp XcodeCodeSnippets/CodeSnippets/* $HOME/Library/Developer/Xcode/UserData/CodeSnippets
rm -rf XcodeCodeSnippets
  ```
  Or if you have a cloned repository:
  * On the command line, cd into the directory with snippets and write `sh ./install.sh`

### List of snippets
#### Comments
* **Snippet:** `// MARK: - `, **shortcut:** `mark`
* **Snippet:** `// MARK: - Public methods`, **shortcut:** `Public methods`
* **Snippet:** `// MARK: - Internal methods`, **shortcut:** `Internal methods`
* **Snippet:** `// MARK: - Private methods`, **shortcut:** `Private methods`
* **Snippet:** `// MARK: - Constants`, **shortcut:** `Constants`
* **Snippet:** `// MARK: - IBOutlets`, **shortcut:** `IBOutletsMARK`
* **Snippet:** `// MARK: - IBActions`, **shortcut:** `IBActionsMARK`
* **Snippet:** `// MARK: - Initialization and deinitialization`, **shortcut:** `Initialization and deinitialization`
* **Snippet:** `// MARK: - Properties`, **shortcut:** `Properties`
* **Snippet:** `// MARK: - NSLayoutConstraints`, **shortcut:** `NSLayoutConstraintsMARK`
* **Snippet:** `// MARK: - Nested types`, **shortcut:** `Nested types`
* **Snippet:** `// MARK: - UITableViewCell`, **shortcut:** `UITableViewCellMARK`
* **Snippet:** `// MARK: - UIViewController`, **shortcut:** `UIViewControllerMARK`
#### Code
* A template for creating TableViewAdapter, **shortcut:** `Table View Adapter`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
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
* A code block for creating user property in UserDefaults extension, **shortcut:** `Defaults Key`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
    var <#defaultsKey#>: <#Type#> {
        get { return <#typeof#>(forKey: #function) }
        set { set(newValue, forKey: #function) }
    }
   ```
  </details>
* A code block for layouting child view anchors equal to a parent view anchors, **shortcut:** `Constraints - layout child as parent`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
    <#childView#>.translatesAutoresizingMaskIntoConstraints = false

    if #available(iOS 11.0, *) {
        NSLayoutConstraint.activate([
            <#childView#>.topAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.topAnchor, constant: 0),
            <#childView#>.bottomAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.bottomAnchor, constant: 0),
            <#childView#>.leadingAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.leadingAnchor, constant: 0),
            <#childView#>.trailingAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.trailingAnchor, constant: 0)
            ])
    } else {
        NSLayoutConstraint.activate([
            <#childView#>.topAnchor.constraint(equalTo: <#parentView#>.topAnchor, constant: 0),
            <#childView#>.bottomAnchor.constraint(equalTo: <#parentView#>.bottomAnchor, constant: 0),
            <#childView#>.leadingAnchor.constraint(equalTo: <#parentView#>.leadingAnchor, constant: 0),
            <#childView#>.trailingAnchor.constraint(equalTo: <#parentView#>.trailingAnchor, constant: 0)
            ])
    }
   ```
  </details>
* A code block for creating object that implement TableCellGenerator and ViewBuilder protocols, **shortcut:** `implTableCellGenerator`. For more info about TableCellGenerator and ViewBuilder see [ReactiveDataDisplayManager](https://github.com/LastSprint/ReactiveDataDisplayManager).
  <details>
  <summary>Code</summary>
  <br>

   ```swift
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
  
* A code block for creating user property in NSNotification.Name extension, **shortcut:** `NSNotification Name`
  <details>
  <summary>Code</summary>
  <br>
 
   ```swift
  static let <#notificationName#> = NSNotification.Name("<#projectName#>.notifications.<#notificationName#>")
   ```
  </details>
  
* A code block for creating template comments for unit test, **shortcut:** `Unit test template`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
  // given

  // when

  // then

   ```
  </details>
  
 * A code block for creating keyboard notifications detector, **shortcut:** `Keyboard detector`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
func addKeyboardObservers() {
        NotificationCenter.default.addObserver(self,
                                               selector: #selector(keyboardWillShow),
                                               name: UIResponder.keyboardWillShowNotification,
                                               object: nil)
        NotificationCenter.default.addObserver(self,
                                               selector: #selector(keyboardWillHide),
                                               name: UIResponder.keyboardWillHideNotification,
                                               object: nil)
    }
    
    @objc
    func keyboardWillShow(notification: NSNotification) {
        guard
            let frame = notification.userInfo?[UIResponder.keyboardFrameEndUserInfoKey] as? NSValue
        else {
            return
        }
    }
    
    @objc
    func keyboardWillHide() {
        
    }
   ```
  </details>

### Author

Ivan Smetanin, smetanin23@yandex.ru

### License

XcodeCodeSnippets is available under the MIT license. See the [LICENSE](https://github.com/ismetanin/XcodeCodeSnippets/blob/master/LICENSE) file for more info.
