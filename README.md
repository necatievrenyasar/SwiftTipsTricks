#  Swift tips & tricks 🚀

Here's some Swift tips & tricks. 


## Table of contents


[#8 CustomStringConvertible](https://github.com/necatievrenyasar/SwiftTipsTricks#8-customstringconvertible)   
[#7 Optional Protocol](https://github.com/necatievrenyasar/SwiftTipsTricks#7-optional-protocol)   
[#6 Unique Array](https://github.com/necatievrenyasar/SwiftTipsTricks#6-unique-array)   
[#5 Defer](https://github.com/necatievrenyasar/SwiftTipsTricks#5-defer)   
[#4 Enum rawValues](https://github.com/necatievrenyasar/SwiftTipsTricks#4-enum-rawvalues)   
[#3 Enum allCases](https://github.com/necatievrenyasar/SwiftTipsTricks#3-enum-allcases)   
[#2 For with Where](https://github.com/necatievrenyasar/SwiftTipsTricks#2-for-with-where)   
[#1 Optional Chaining](https://github.com/necatievrenyasar/SwiftTipsTricks#1-optional-chaining)   

## [#8 CustomStringConvertible

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
