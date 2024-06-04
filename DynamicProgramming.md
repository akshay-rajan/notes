# Dynamic Programming

Dynamic Programming is the concept of solving a complex problem by breaking it down into overlapping subproblems.

## Memoization

Memoization is a programming technique of storing the result of expensive function calls and returning the stored result when the same input occurs again.

### Fibonacci

Problem: Find the fibonacci number for a given number.

```java
// Recursive Function
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```
```java
// Memoization
int fib(int n, int[] memo) {
    // Check in the memo
    if (memo[n] != 0) 
        return memo[n];
    
    if (n <= 1) return n;

    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}
```
Memoization cuts down the number of recursive calls.

<img src="image-3.png" alt="alt text" style="height: 200px">
<img src="image-2.png" alt="alt text" style="height: 200px">
<img src="image-4.png" alt="alt text" style="height: 200px">

Memoization simplifies the Time Complexity of `O(n^2)` to `O(n)`. The tree only grows linearly.


### Grid Traveler

Problem: Find the number of ways to travel from the top-right to bottom-down in a 2D grid.

`gridTraveler(1, 1) -> 1`

`gridTraveler(0, k) -> 0 and gridTraveler(k, 0) -> 0`

<img src="image.png" alt="alt text" style="height: 200px">

`gridTraveler(2, 3) -> 3`

<img src="image-1.png" alt="alt text" style="height: 180px">

```java
// Recursive Implementation
int gridTraveler(int m, int n) {
    // Base Case
    if (m == 1 && n == 1) return 1;
    if (m == 0 || n == 0) return 0;
    // Recursive call
    return gridTraveler(m - 1, n) + gridTraveler(m, n - 1);
}
```
The time complexity of the recursive function is `O(2 ^ (m + n))` and the space complexity is `O(m + n)`

We can observe that `gridTraveler(a, b)` is equal to `gridTraveler(b, a)`.

```java
// Memoization
int gridTraveler(int m, int n, int[][] memo) {
    // Check for the value inside the memo
    if (memo[m][n] != 0) return memo[m][n];

    // Base Case
    if (m == 1 && n == 1) return 1;
    if (m == 0 || n == 0) return 0;

    // Recursive Call
    return memo[m][n] = gridTraveler(m - 1, n, memo) + gridTraveler(m, n - 1, memo);
}
```

In the memoized function, the time complexity is `O(m * n)` and the space complexity is `O(m + n)`.

### Steps for Memoization

1. Make it work
    - Visulaize the problem as a tree
    - Implement the tree using recursion
        - Base Case: Leaves of the tree
    - Now you have the brute force solution. Test it

2. Make it efficient
    - Add a memo object 
        - Keys: Arguments
        - Values: Return Values
    - Add a new Base Case which returns memo values
    - Store return values in the memo before returning

### canSum

Problem: Return whether it's possible to generate the `targetSum` using some `numbers` in an array.

`canSum(7, [5, 3, 4, 7]) = true`

<img src="image-5.png" alt="alt text" style="height: 180px">

```java
boolean canSum(int targetSum, int[] nums) {
    // We can generate a sum of 0 by taking NO elements
    if (canSum == 0) return true;
    // If the targetSum is negative, the path is wrong
    if (canSum < 0) return false;

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        if (canSum(remainder, nums)) return true;
    }
    return false;
}
```
This is of `O(n^m)` time complexity and `O(m)` space complexity.

The numbers argument doesn't change, or does not affect the return values, hence we only need the target sum in the memo.

```java
boolean canSum(int targetSum, int[] nums, int[] memo) {
    // We can generate a sum of 0 by taking NO elements
    if (canSum == 0) return true;
    // If the targetSum is negative, the path is wrong
    if (canSum < 0) return false;

    // Check in the memo
    if (memo[targetSum] != -1) 
        return memo[targetSum] == 1 ? true : false;

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        if (canSum(remainder, nums, memo)) {
            memo[targetSum] = 1;
            return true;
        }
    }
    memo[targetSum] = 0;
    return false;
}
```
Now the time complexity has changed to `O(m * n)`.

### howSum

Problem: Return a combination of elements in an array, that adds up to exactly the `targetSum`.

```java
List<Integer> howSum(int targetSum, int[] nums) {
    
    // If the target sum is 0, return an empty array
    if (canSum == 0)
        return new ArrayList<Integer>();
    
    // If the targetSum is negative, the path is wrong
    if (canSum < 0) return null;

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        // If the branch returned a possible solution
        List<Integer> curr = howSum(remainder, nums);
        if (curr != null) {
            // Add the current element to the array
            curr.add(num);
            return curr;
        }
    }
    return null;
}
```

```java
List<Integer> howSum(int targetSum, int[] nums, int[][] memo) {
    
    // If the target sum is 0, return an empty array
    if (howSum == 0)
        return new ArrayList<Integer>();
    
    // If the targetSum is negative, the path is wrong
    if (howSum < 0) return null;

    // Check inside the memo
    if (!memo[targetSum].isEmpty()) return memo[targetSum];

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        // If the branch returned a possible solution
        List<Integer> curr = howSum(remainder, nums);
        if (curr != null) {
            // Add the current element to the array
            curr.add(num);
            return memo[targetSum] = curr;
        }
    }
    memo[targetSum] = -1;
    return null;
}
```

### bestSum

Problem: Return the smallest array that adds up to `targetSum`.

`bestSum(8, [2, 3, 5]) = [3, 5]`

`bestSum(8, [1, 4, 5]) = [4, 4]`

```java 
List<Integer> bestSum(int targetSum, int[] nums) {
    
    // If the target sum is 0, return an empty array
    if (canSum == 0)
        return new ArrayList<Integer>();
    
    // If the targetSum is negative, the path is wrong
    if (canSum < 0) return null;

    // Keep track of the shortest combination
    List<Integer> shortestComb = null;

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        // If the branch returned a possible solution
        List<Integer> remComb = bestSum(remainder, nums);
        if (remComb != null) {
            // Add the current element to the array
            List<Integer> comb = remComb.add(num);
            if (shortestComb == null || comb.size() < shortestComb.size()) {
                shortestComb = comb;
            }
        }
    }
    return shortestComb;
}
```

```java 
List<Integer> bestSum(int targetSum, int[] nums, int[][] memo) {
    
    // If the target sum is 0, return an empty array
    if (canSum == 0)
        return new ArrayList<Integer>();
    
    // If the targetSum is negative, the path is wrong
    if (canSum < 0) return null;

    // Check in the memo
    if (!memo[targetSum].isEmpty()) return memo[targetSum];

    // Keep track of the shortest combination
    List<Integer> shortestComb = null;

    // Try all possibilities of numbers
    for (int num: nums) {
        int remainder = targetSum - num;
        // If the branch returned a possible solution
        List<Integer> remComb = bestSum(remainder, nums, memo);
        if (remComb != null) {
            // Add the current element to the array
            List<Integer> comb = remComb.add(num);
            if (shortestComb == null || comb.size() < shortestComb.size()) {
                shortestComb = comb;
            }
        }
    }
    return memo[targetSum] = shortestComb;
}
```

<div style="color: red">
The `canSum` Problem is a Decision Problem, `howSum` is a Combinatoric Problem and `bestSum` is an Optimization problem.
</div>

### canConstruct

Problem: Return whether the `target` string can be constructed from an array of strings, `wordbank` by concatenation. The elements in `wordbank` can be reused.

<img src="image-6.png" alt="alt text" style="height: 180px">

<img src="image-7.png" alt="alt text" style="height: 280px">

```java 
public boolean canConstruct(String target, List<String> wordbank) {
    if (target.isEmpty()) return true;

    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            if (canConstruct(suffix, wordbank)) return true;
        }
    }
    return false;
}
```
```java 
public boolean canConstruct(String target, List<String> wordbank, Map<String, Boolean> memo) {
    if (target.isEmpty()) return true;

    if (memo.contains(target)) return memo.get(target);

    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            if (canConstruct(suffix, wordbank, memo)) {
                memo.put(target, true);
                return true;
            }
        }
    }
    memo.put(target, false);
    return false;
}
```

### countConstruct

Problem: Return the number of ways in which the target string can be constructed.

```java 
public int countConstruct(String target, List<String> wordbank) {
    if (target.isEmpty()) return 0;

    int value = 0;
    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            value += countConstruct(suffix, wordbank);
        }
    }
    return value;
}
```
```java 
public int countConstruct(String target, List<String> wordbank, Map<String, Integer> memo) {
    if (target.isEmpty()) return 0;

    if (memo.contains(target)) return memo.get(target);

    int value = 0;
    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            value += countConstruct(suffix, wordbank, memo);
        }
    }
    memo.put(target, value);
    return value;
}
```

```java 
```