# CombineNetworkOperationPackage

CombineNetworkOperationPackage is a robust and easy-to-use network package designed for iOS apps created with the Combine Framework. It provides a clean interface for making network requests and parsing JSON responses.

## Features

- Simple and intuitive API for making network requests
- Uses Combine to provide a reactive programming interface
- Supports GET, POST, PUT, DELETE and PATCH request methods
- Easily configurable request parameters, headers and body
- Automatically parses JSON responses into custom Codable models
- Supports HTTP and HTTPS protocols
- Built-in error handling and customizable error messages
- Tested and ready for production use

## Installation

You can install CombineNetworkOperationPackage using CocoaPods or Swift Package Manager.

### CocoaPods

Add the following line to your Podfile:

```
pod 'CombineNetworkOperationPackage'
```

Then run `pod install` command.

### Swift Package Manager

In Xcode, go to File -> Swift Packages -> Add Package Dependency and enter the following URL:

```
https://github.com/<username>/CombineNetworkOperationPackage.git
```

## Usage

To make a GET request to a URL with CombineNetworkOperationPackage, simply call the `get` method and pass in the URL as a string. You can chain additional methods to configure your request, such as adding query parameters or headers:

``` swift
import CombineNetworkOperationPackage
import Combine

let url = "https://jsonplaceholder.typicode.com/todos/1"
let cancellable = URLSession.shared

  .get(url)
  .map(\.data)
  .decode(type: Todo.self, decoder: JSONDecoder())
  .sink(receiveCompletion: { result in
    switch result {
    case .finished:
      print("Request finished successfully.")
    case .failure(let error):
      print("Request failed with error: \(error.localizedDescription)")
    }
  }, receiveValue: { todos in
    print("Todo: \(todos)")
  })
```

You can also specify a request body for POST, PUT, DELETE and PATCH requests:

``` swift
let url = "https://jsonplaceholder.typicode.com/posts"
let requestBody = ["title": "foo", "body": "bar", "userId": 1] as [String: Any]
let cancellable = URLSession.shared

  .post(url)
  .body(requestBody)
  .map(\.data)
  .decode(type: Post.self, decoder: JSONDecoder())
  .sink(receiveCompletion: { result in
    switch result {
    case .finished:
      print("Request finished successfully.")
    case .failure(let error):
      print("Request failed with error: \(error.localizedDescription)")
    }
  }, receiveValue: { post in
    print("Post: \(post)")
  })
```

CombineNetworkOperationPackage automatically parses JSON responses into custom Codable models. Make sure your models conform to the `Codable` protocol:

``` swift
struct Todo: Codable {
  let id: Int
  let userId: Int
  let title: String
  let completed: Bool
}

struct Post: Codable {
  let id: Int
  let title: String
  let body: String
  let userId: Int
}
```

For additional configuration options and examples, please see the [documentation](https://github.com/<username>/CombineNetworkOperationPackage).

## Contributions

Contributions are welcome! Please feel free to fork the repository and submit a pull request with your changes.

## License

CombineNetworkOperationPackage is available under the MIT license. See the [LICENSE](./LICENSE) file for more information.