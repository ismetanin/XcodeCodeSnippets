[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

# XcodeCodeSnippets

A set of snippets for Xcode.

## Requirements

Xcode 7.3.1 or later.

## Installation

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

## List of snippets

### MARKs

* **Snippet:** `// MARK: -`, **shortcut:** `mark`
* **Snippet:** `// MARK: - Public methods`, **shortcut:** `Public methods`
* **Snippet:** `// MARK: - Internal methods`, **shortcut:** `Internal methods`
* **Snippet:** `// MARK: - Private methods`, **shortcut:** `Private methods`
* **Snippet:** `// MARK: - Constants`, **shortcut:** `ConstantsMARK`
* **Snippet:** `// MARK: - IBOutlets`, **shortcut:** `IBOutletsMARK`
* **Snippet:** `// MARK: - IBActions`, **shortcut:** `IBActionsMARK`
* **Snippet:** `// MARK: - Initialization and deinitialization`, **shortcut:** `Initialization and deinitialization`
* **Snippet:** `// MARK: - Properties`, **shortcut:** `Properties`
* **Snippet:** `// MARK: - Public properties`, **shortcut:** `Public properties mark`
* **Snippet:** `// MARK: - NSLayoutConstraints`, **shortcut:** `NSLayoutConstraintsMARK`
* **Snippet:** `// MARK: - Nested types`, **shortcut:** `Nested types`
* **Snippet:** `// MARK: - UITableViewCell`, **shortcut:** `UITableViewCellMARK`
* **Snippet:** `// MARK: - UIViewController`, **shortcut:** `UIViewControllerMARK`
* **Snippet:** `// MARK: - Subviews`, **shortcut:** `Subviews mark`
* **Snippet:** `// MARK: - Actions`, **shortcut:** `Actions mark`
* **Snippet:** `// MARK: - Readonly properties`, **shortcut:** `Readonly properties`

### Code

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

       private let output: <#Your#>ViewAdapterOutput

       // MARK: - Properties

       private var items: [<#ItemsType#>]
       private (set) var tableView: UITableView {
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
  
* A code block for creating user property in NSNotification.Name extension, **shortcut:** `NSNotification Name`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
  static let <#notificationName#> = NSNotification.Name("<#projectName#>.notifications.<#notificationName#>")
   ```

  </details>
  
* A code block for creating template comments for unit test, **shortcut:** `testtemplate`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
  // given

  // when

  // then

   ```

  </details>
  
* A code block for creating template constants enum, **shortcut:** `Constants enum`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
    // MARK: - Nested types

    private enum Constants {

    }
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
