# Data-Structures-and-Algorithms
> This is the study record of - "A Common-Sense Guide to Data Structures and Algorithms Level Up Your Core Programming Skills by Jay Wengrow"
I used my knowledge of Swift language to read and explain the example of this book.

### Table of contents
8. [Blazing Fast Lookup with Hash Tables](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#8-blazing-fast-lookup-with-hash-tables)
9. [Crafting Elegant Code with Stacks and Queues](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#9-crafting-elegant-code-with-stacks-and-queues)
10. [Recursively Recurse with Recursion](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#9-recursively-recurse-with-recursion)
12. [Dynamic Programming](https://github.com/KaoWenChung/Data-Structures-and-Algorithms#12-dynamic-programming)

# 8. Blazing Fast Lookup with Hash Tables
## Hash Tables for Organization
As I know the Hash table in Swift is Dictionary Type. It's a key value pairs data type which is useful for many scenarios. We can use key to find the specific value. For example the political candidates and the number of votes each receives.<br/>
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
In this case the big O will be O(N * M).<br/>
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
If we say that the N is total number of items of both arrays combined. Then we can say the big O is O(N)<br/>
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
# 10. Recursively Recurse with Recursion
Recursion is the term for a function calling itself. We need a base case to stop the recursive function in case it infinitely repeats itself.
```
var blahTime: Int = 10

func blah() {
  guard blahTime != 0 else { return }
  blahTime -= 1
  blah()
}
```
## Reading Recursive Code
Take calculating factorials as an example, factorials is like:<br/>
factorial of 3 is:<br/>
3 * 2 * 1 = 6<br/>
factorial of 4 is:<br/>
4 * 3 * 2 * 1 = 24<br/>
So we can write the function as below:
```
func factorial(_ number: Int) {
  if nubmer == 1 {
    return 1
  } else {
    return number * factorial(number - 1)
  }
}
```
# 12. Dynamic Programming
When we use the recursive function, we should be careful about the unnecessary call. A recursive function is a function that calls itself. If we call itself many times in itself, when we analyze its time complexity. We will find there is a big problem with it.

## The Little Fix for Big O
We should try our best to minimize the times a recursive function calls itself. For example, we can declare a property to store the value of the function instead of duplicate calling itself.

> :+1: When a problem is solved by solving smaller versions of the same problem,
the smaller problem is called a subproblem.

## Overlapping Subproblems
The Fibonacci sequence is a list of numbers like: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55???infinity<br/>
it begins with 0, and 1, then each number is the sum of the previous two numbers. The function will be as follows:
```
func fib(_ number: Int) -> Int {
  if number == 0 || number == 1 {
    return number
  } else {
    return fib(number - 2) + fib(number - 1)
  }
}
```
Let say we pass 6 as fib(6), it will call fib(4) and fib(5), Then fib(5) will call fib(3) and fib(4). With the number increase, the time of square increase as well. The time complexity will be O(2<sup>N</sup>)

## Dynamic Programming through Memoization
There is a solution for the previous section, we can pass the second parameter as memorization data which is going to store the result in a dictionary.
```
func fib2(_ number: Int, memo: inout [Int: Int]) -> Int {
  if number == 0 || number == 1 {
    return number
  }
  if memo[number] == nil {
    memo[number] = fib2(number - 2, memo: &memo) + fib2(number - 1, memo: &memo)
  }
  return memo[number]!
}
```
## Bottom-Up Fibonacci
Besides the recursive function, we can also use a bottom-up approach to solve the previous problem.
```
func fib(_ number: Int) -> Int {
  if number == 0 {
    return 0
  }
  var a = 0
  var b = 1
  for _ in 1 ..< number {
    var tempSum = a + b
    a = b
    b = tempSum
  }
  return b
}
```
In this function, we loop once the range of number. The time complexity is O(N).
## Memoization vs. Bottom-Up
Even though the time complexity of both Memoization and Bottom-Up are the same, we should know about recursive function, the computer needs to keep track of all the calls in a call stack, which consume memory. The memorization also requires the usage of a hash table which takes up additional space.<br/>
Generally speaking, going bottom-up is often the better choice unless the recursive function is more intuitive.

## Exercises
1. Improve the function below:
```
func add_until_100(_ array: [Int]) -> Int {
  guard !array.isEmpty else { return 0 }
  if array.first! + add_until_100(Array(array[1...array.count - 1])) > 100 {
    return add_until_100(Array(array[1...array.count - 1]))
  }
  return array.first! + add_until_100(Array(array[1...array.count - 1]))
}
```
Answer:
```
func add2_until_100(_ array: [Int]) -> Int {
  guard !array.isEmpty else { return 0 }
  let tempValue = add_until_100(Array(array[1...array.count - 1]))
  if array.first! + tempValue > 100 {
    return tempValue
  }
  return array.first! + tempValue
}
```
2. Use memoization to optimize
```
func golomb(_ number: Int) -> Int {
  if number == 1 { return 1 }
  return 1 + golomb(number - golomb(golomb(number - 1)))
}
```
Answer:
```
func golomb2(_ number: Int, memo: inout [Int: Int]) -> Int {
  if number == 1 { return 1 }
  if memo[number] == nil {
    memo[number] = 1 + golomb2(number - golomb2(golomb2(number - 1, memo: &memo), memo: &memo), memo: &memo)
  }
  return memo[number]!
}
```
3. Use memoization to improve its efficiency
```
func unique_paths(_ rows: Int, _ columns: Int) -> Int {
  if rows == 1 || columns == 1 { return 1 }
  return unique_paths(rows - 1, columns) + unique_paths(rows, columns - 1)
}
```
Answer:
```
func unique_paths2(_ rows: Int, _ columns: Int, memo: inout [[Int]: Int]) -> Int {
  if rows == 1 || columns == 1 { return 1 }
  if memo[[rows, columns]] == nil {
    memo[[rows, columns]] = unique_paths2(rows - 1, columns, memo: &memo) + unique_paths2(rows, columns - 1, memo: &memo)
  }
  return memo[[rows, columns]]!
}
```
# 13. Recursive Algorithms for Speed
## Partitioning
To partition is to take a random value from an array, which is called "pivot", and then let every number that is less than the pivot ends up on the left, every number that is greater than the pivot ends up to the right.
Step1. pick the rightmost one in the array as the pivot.
Step2. We then assign "pointers", one is the leftmost, and one is the rightmost excluding the pivot itself.
Step3. The left pointer continuously moves one cell to the right until it reaches the value which is greater than or equal to the pivot, and then stops.
Step4. The right pointer continuously moves the cell to the left until it reaches a value that is less than or equal to the pivot, and then stops. It will also stop when it reaches the beginning of the array.
Step5. Once the right pointer stops. If the left pointer reaches the right pointer. We go to step 6. Otherwise, we swap the values that the left and right pointers are pointing to and then go back to stap 3, 4, 5.
Step6. Finally, we swap the pivot with the value that the left pointer is pointing to.
```
SortableArray {
    private(set) var attrArray: [Int]
    init(_ array: [Int]) {
        attrArray = array
    }
    func partition(leftPointer: inout Int, rightPointer: inout Int) {
        var pivotIndex = rightPointer
        var pivot = attrArray[pivotIndex]
        rightPointer -= 1
        while true {
            while attrArray[leftPointer] < pivot {
                leftPointer += 1
            }
            while attrArray[rightPointer] > pivot {
                rightPointer -= 1
            }
            if leftPointer >= rightPointer {
                break
            } else {
                (attrArray[leftPointer], attrArray[rightPointer]) = (attrArray[rightPointer], attrArray[leftPointer])
                leftPointer += 1
            }
        }
        (attrArray[leftPointer], attrArray[pivotIndex]) = (attrArray[pivotIndex], attrArray[leftPointer])
    }
}
```
# 14. Node-Based Data Structures
## Linked Lists
Like an array, a linked list is a data structure that represents a list of items. While on surface, arrays and linked lists seems like act quite similarly, there are big differences between them.<br/>
Linked list contains a connected data that is dispersed throughout memory are known as nodes. Each node also comes with a little extra information, namely, the memory address of the next node in the list.<br/>
Implementing a Linked List
```
class Node {
  let data: AnyObject
  var nextNode: Node?
  init(data: AnyObject) {
    self.data = data
  }
}
```
