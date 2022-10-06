# Data-Structures-and-Algorithms
> This is the study record of - "A Common-Sense Guide to Data Structures and Algorithms Level Up Your Core Programming Skills by Jay Wengrow"
I used my knowledge of Swift language to read and explain the example of this book.

### Table of contents
8. [Blazing Fast Lookup with Hash Tables](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#8-blazing-fast-lookup-with-hash-tables)
9. [Crafting Elegant Code with Stacks and Queues](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#8-Crafting-Elegant-Code-with-Stacks-and-Queues)

# 8. Blazing Fast Lookup with Hash Tables
## Hash Tables for Organization
As I know the Hash table in Swift is Dictionary Type. It's a key value pairs data type which is useful for many scenarios. We can use key to find the specific value. For example the political candidates and the number of votes each receives.
Another example is common HTTP status, we can define a function and return the meaning of the status code.
```
func statusCode(_ code: Int) -> String? {
  switch code {
    case 200:
    return "OK"
    case 301:
    return "Moved Permanently"
    case 401:
    return "Unauthorized"
    case 404:
    return "Not Found"
    case 500:
    return "Internal Server Error"
    default:
    return nil
  }
}
```
We can use Hash Tables aka Dictionary to deal with it
```
let statusCodeDict: [Int: String] = [
  200: "OK",
  301: "Moved Permanently",
  401: "Unauthorized",
  404: "Not Found",
  500: "Internal Server Error"
]
```
## Hash Tables for Speed
If we want to search a number in an unordered Int array, we must use linear search. Therefore, the big O notation would be O(N). Instead of searching a number in an array, we can use dictionary pairs number key with Boolean value true. If we want to search the number in a hash table data. It will only take one step. Big O will be O(1).

## Array Subset
Now we determine wether an array is subset of another array. We can use a nested loop to check the larger array by each smaller array.
```
func isSubset(array1: [String], array2: [String]) -> Bool {
  var largerArray: [String] = []
  var smallerArray: [String] = []

  if array1.count > array2.count {
    largerArray = array1
    smallerArray = array2
  } else {
    largerArray = array2
    smallerArray = array1
  }

  for element1 in smallerArray {
    var isMatch = false
    for element2 in largerArray {
      if element1 == element2 {
        isContains = true
        break
      }
    }
    if isMatch == false {
      return false
    }
  }
  return true
}
```
In this case the big O will be O(N * M).
We can use hash table to improve this function.
```
func isSubset(array1: [String], array2: [String]) -> Bool {
  var largerArray: [String] = []
  var smallerArray: [String] = []

  if array1.count > array2.count {
    largerArray = array1
    smallerArray = array2
  } else {
    largerArray = array2
    smallerArray = array1
  }

  var largeDictionary: [String: Bool] = [:]
  for item in largerArray {
    largeDictionary[item] = true
  }

  for item in smallerArray {
    if largeDictionary[item] == nil {
      return false
    }
  }
  return true
}

```
If we say that the N is total number of items of both arrays combined. Then we can say the big O is O(N)
Stacks and Queues are the data types we use to store temporary data
# 9. Crafting Elegant Code with Stacks and Queues
## Stacks
Stacks follow three point:
- Last In First Out (LIFO)
- Can't not be inserted somewhere instead of the end of stack
- Only the last one of the stack can be read

## Abstract Data Types
Even though we don't have stack type in Swift, we can create one
```
struct Stack<T> {
    private var stackData: [T] = []

    mutating func push(_ element: T) {
        stackData.append(element)
    }

    func read() -> T? {
        return stackData.last
    }

    mutating func pop() {
        stackData.popLast()
    }
}
```
