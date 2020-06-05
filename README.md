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

There are MARKs for Swift and Objective-C. For Swift there is prefix before each `// MARK: -` and for Objective-C prefix is `#pragma mark -`.

Shortcuts are equal to snippet body for example for `// MARK: - Properties` shortcut is `Properties`.

<details>
  <summary>Available MARKs</summary>
  <br>

|Snippet|
|---|
|Just empty mark (`// MARK: - ` or `#pragma mark - `)     |
|`Nested types`                                           |
|`Constants`                                              |
|`Subviews`                                               |
|`NSLayoutConstraints`                                    |
|`Properties`                                             |
|`Public properties`                                      |
|`Readonly properties`                                    |
|`IBOutlets`                                              |
|`Initialization and deinitialization`                    |
|`UITableViewCell`                                        |
|`UIViewController`                                       |
|`Actions`                                                |
|`IBActions`                                              |
|`Public methods`                                         |
|`Internal methods`                                       |
|`Private methods`                                        |
</details>

### Code

* A template for creating TableViewAdapter, **shortcut:** `Table View Adapter`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
    import UIKit

    protocol <#Your#>TableViewAdapterOutput {
    }

    final class <#Your#>TableViewAdapter: NSObject {
        // MARK: - Properties

        private let output: <#Your#>TableViewAdapterOutput

        private var items: [String]
        private var tableView: UITableView

        // MARK: - Initialization and deinitialization

        init(tableView: UITableView, output: <#Your#>TableViewAdapterOutput) {
            self.output = output
            self.tableView = tableView
            self.items = []
            super.init()
            setupTable()
        }

        // MARK: - Internal methods

        func configure(with items: [String]) {
            self.items = items
            tableView.reloadData()
        }

        // MARK: - Private methods

        private func setupTable() {
            tableView.delegate = self
            tableView.dataSource = self
            tableView.register(
                UINib(nibName: String(describing: <#Your#>TableViewCell.self), bundle: nil),
                forCellReuseIdentifier: String(describing: <#Your#>TableViewCell.self)
            )
        }
    }

    // MARK: - UITableViewDataSource

    extension <#Your#>TableViewAdapter: UITableViewDataSource {
        func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
            return items.count
        }

        func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
            let cell = tableView.dequeueReusableCell(
                withIdentifier: String(describing: <#Your#>TableViewCell.self),
                for: indexPath
            ) as? TableViewCell
            cell?.backgroundColor = .red
            return cell ?? <#Your#>UITableViewCell()
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
* A code block for layouting child view anchors equal to the parent view anchors, **shortcut:** `Constraints - layout child as parent`
  <details>
  <summary>Code</summary>
  <br>

   ```swift
    <#childView#>.translatesAutoresizingMaskIntoConstraints = false

    NSLayoutConstraint.activate([
        <#childView#>.topAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.topAnchor, constant: 0),
        <#childView#>.bottomAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.bottomAnchor, constant: 0),
        <#childView#>.leadingAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.leadingAnchor, constant: 0),
        <#childView#>.trailingAnchor.constraint(equalTo: <#parentView#>.safeAreaLayoutGuide.trailingAnchor, constant: 0)
        ])
   ```

  </details>
  
* A code block for user property creating in NSNotification.Name extension, **shortcut:** `NSNotification Name`
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
