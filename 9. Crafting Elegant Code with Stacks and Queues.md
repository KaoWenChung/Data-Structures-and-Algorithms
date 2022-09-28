Stacks and Queues are the data types we use to store temporary data
# Stacks
Stacks follow three point:
- Last In First Out (LIFO)
- Can't not be inserted somewhere instead of the end of stack
- Only the last one of the stack can be read

# Abstract Data Types
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
