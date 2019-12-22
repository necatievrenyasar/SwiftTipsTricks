#  Swift tips & tricks 🚀

Here's some Swift tips & tricks. 


## Table of contents
[#14 Email Validation](https://github.com/necatievrenyasar/SwiftTipsTricks#15-email-validation)   
[#14 Variadic Functions](https://github.com/necatievrenyasar/SwiftTipsTricks#14-variadic-functions)   
[#13 Failable init](https://github.com/necatievrenyasar/SwiftTipsTricks#13-failable-init)   
[#12 Convenience init](https://github.com/necatievrenyasar/SwiftTipsTricks#12-convenience-init)   
[#11 Generic with Where Clause](https://github.com/necatievrenyasar/SwiftTipsTricks#11-generic-with-where-clause)   
[#10 deinit](https://github.com/necatievrenyasar/SwiftTipsTricks#10-deinit)   
[#9 compactMap](https://github.com/necatievrenyasar/SwiftTipsTricks#9-compactmap)   
[#8 CustomStringConvertible](https://github.com/necatievrenyasar/SwiftTipsTricks#8-customstringconvertible)   
[#7 Optional Protocol](https://github.com/necatievrenyasar/SwiftTipsTricks#7-optional-protocol)   
[#6 Unique Array](https://github.com/necatievrenyasar/SwiftTipsTricks#6-unique-array)   
[#5 Defer](https://github.com/necatievrenyasar/SwiftTipsTricks#5-defer)   
[#4 Enum rawValues](https://github.com/necatievrenyasar/SwiftTipsTricks#4-enum-rawvalues)   
[#3 Enum allCases](https://github.com/necatievrenyasar/SwiftTipsTricks#3-enum-allcases)   
[#2 For with Where](https://github.com/necatievrenyasar/SwiftTipsTricks#2-for-with-where)   
[#1 Optional Chaining](https://github.com/necatievrenyasar/SwiftTipsTricks#1-optional-chaining)   


## [#15 Email Validation](http://swiftevreni.com)
🌜 To check email validation, regex is best way.

```swift
extension String {
    var isValidEmail: Bool {
        if self.isEmpty {
            return false
        }
        let emailRegEx = "[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,64}"
        let emailPred = NSPredicate(format:"SELF MATCHES %@", emailRegEx)
        return emailPred.evaluate(with: self)
    }
}


print("evren@necatievren.com".isValidEmail)
```


## [#14 Variadic Functions](http://swiftevreni.com)

👾 Variadic functions takes zero or more input values of a specified type. To work with a variadic function, you just add … after any parameter.

```swift
func sum(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total
}

print(sum(1, 2, 3, 4, 5))
//15
```




## [#13 Failable init](http://swiftevreni.com)

 🐸You can prefer `failable initializer` for avoid to create object with invalid parameters.

```swift
enum AppState{
    case login, register
    
    init?(rawValue:Int) {
        switch rawValue {
        case 0:
            self = .login
        case 1:
            self = .register
        default:
            return nil
        }
    }
}

print(AppState(rawValue: 3))
//nil
```





## [#12 convenience init](http://swiftevreni.com)

🦋 `convenience init` calles designated initializers with pre-set parameters.

```swift
class Person {
    var name: String
    var id:Int
    var photo: UIImage
    
    init(name:String, id: Int, photo: UIImage) {
        self.name = name
        self.id = id
        self.photo = photo
    }
    
    convenience init(id: Int) {
        self.init(name: "[Unnamed]", id: id, photo: UIImage(named: "default_photo")!)
    }    
}
```





## [#11 Generic with Where Clause](http://swiftevreni.com)

🥽 `Where` clause help you to filter in values of generic type. 

```swift
struct Location {
    let lat: Double
    let lon: Double
}
extension Location: CustomDebugStringConvertible {
    var description: String {
        return "Location: \(lat),\(lon)"
    }
}

//Logger is work only class/struct that is extended CustomDebugStringConvertible
struct Logger<T> where T: CustomDebugStringConvertible {
    func debug(ref: T) {
        print(ref)
    }
}
```



## [#10 deinit](http://swiftevreni.com)

👓 `deinit` function is called before your class is deallocated the memory spaces.`deinit` function is avaliable only in class type.

```swift
class DetailViewController: UIViewController {
  ....

  deinit {
      NotificationCenter.default.removeObserver(self)
   }
}
```





## [#9 compactMap](http://swiftevreni.com)

🐝 `compactMap` is function like `map` . That functions applies a transformation to each of elements in a array. However  `compactMap` is automatically removes `nil` elements from the returned array.


```swift
let stringsArray = ["4","5","six","7","ten"]
let intsArray = stringsArray.compactMap {Int($0)}
print(intsArray)
//[4, 5, 7]
```





## [#8 CustomStringConvertibel](http://swiftevreni.com)

🐊 `CustomStringConvertible` is a protocol that can be implemented on Class and Struct to readable print. 

**Before**

```swift
struct Person {
    let firstName: String
    let lastName: String
    let id: Int
    let age: Int
    var fullName: String? = nil
}
let person = Person(firstName: "Ali", lastName: "Tekin", id: 987, age: 20)
print(person)
//Person(firstName: "Ali", lastName: "Tekin", id: 987, age: 20, fullName: nil)
```

**After**

```swift
struct Person {
    let firstName: String
    let lastName: String
    let id: Int
    let age: Int
    var fullName: String? = nil
}

extension Person: CustomStringConvertible {
    var description: String {
        return "Person: \(firstName) \(lastName) id: \(id)"
    }
}
let person = Person(firstName: "Ali", lastName: "Tekin", id: 987, age: 20)
print(person)
//Person: Ali Tekin id: 987
```





## [#7 Optional Protocol](http://swiftevreni.com)

🦁 Swift does not allow us to perform optional functions. We can do it through `extension`

```swift
protocol DetailVMDelegate:class {
    func detailVM(_ viewModel: DetailVM, data: [String])
    func detailVMShowPreloader(_ viewModel: DetailVM, status: Bool)
}

extension DetailVMDelegate {
    func detailVMShowPreloader(_ viewModel: DetailVM, status: Bool) {}
}
```





## [#6 Unique Array](http://swiftevreni.com)

🦿 If you want removing duplicate item from an array, there are several ways but I prefer to use  `set`  

```swift
let values = [1,2,3,4,4,4,5,6,7]
let valuesSet = Set(values)
let uniqueValues = Array(valuesSet)
```





## [#5 Defer](http://swiftevreni.com)

🦿 `defer` statement is the last block of code that will be executed in function. 

```swift
func doSometing() {
  defer {print ("First")}
  defer {print ("Second")}
  print("End of function")
}
//End of function
//First
//Second
```

Most common usage:

```swift
func readFile(_ name:String) {
  	let manager: FileManager? = FileManager(with: name) 
  	defer {
      	manager.?closeFile()
    }
  	....
}
```






## [#4 Enum rawValues](http://swiftevreni.com)

🎃 You can access cases of enum directly by use a `rawValue`

```swift
enum City:Int {
    case adana
    case adiyaman
    case afyon
    case agri
    case amasya
    case ankara
}
//Index start by 0.
let city06 = City.init(rawValue: 06 - 1)
```





## [#3 Enum allCases](http://swiftevreni.com)

🧣 If you want to access all cases of enum, you must enable CaseIterable protocol.

```swift
enum Direction: CaseIterable {
    case north, south, east, west
}

for item in Direction.allCases {
  	...
}
```





## [#2 For with Where](http://swiftevreni.com)

🐨 More safety and fast then 'if break'

**Before**

```swift
for player in game.players {
    if player.id == currentId {
        ...
        break
    }
}
```
**After**
```swift
for player in game.players where player.id == currentId {
    ...
}
```





## [#1 Optional Chaining](http://swiftevreni.com)

❓ Optional Chaining that is really cool property in Swift, is help you to avoid 'If blogs'

**Before**
```swift
if let place = placeModel {
    if let reviews = place.reviews {
        if let firstReview = reviews.first? {
            ...
        }
    }
}
```
**After**
```swift
guard let firstReview = placeModel?.reviews?.first? else {return}
...
```
