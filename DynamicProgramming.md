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

### allConstruct

Problem: Return the collection of all ways in which the target string can be constructed.

```java 
public List<List<String>> allConstruct(String target, List<String> wordbank) {
    List<List<String>> result = new ArrayList<>();

    if (target.isEmpty()) return result;

    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            // The function returns a 2D array
            List<List<String>> suffixWays = allConstruct(suffix, wordbank);
            for (List<String> way: suffixWays) {
                suffixWays.insert(0, way);
            }
            result.addAll(suffixWays);
        }
    }
    return result;
}
```
```java 
public List<List<String>> allConstruct(String target, List<String> wordbank, Map<String, List<List<String>>> memo) {
    List<List<String>> result = new ArrayList<>();

    if (target.isEmpty()) return result;
    
    if (memo.contains(target)) return memo.get(target);

    for (String word: wordbank) {
        if (target.indexOf(word) == 0) {
            String suffix = target.substring(0, word.length());
            // The function returns a 2D array
            List<List<String>> suffixWays = allConstruct(suffix, wordbank, memo);
            for (List<String> way: suffixWays) {
                suffixWays.insert(0, way);
            }
            result.addAll(suffixWays);
        }
    }
    memo.put(target, result);
    return result;
}
```

## Tabluation

Tabluation or Pure Dynamic Programming combines storage and iteration, whereas memoization combines storage and recursion.

We store the results of each sub problem in a table.

### fib

```java 
int fib(int n) {
    if (n <= 1) return n;
    // Initialize a table. In Java, this table is filled with 0
    int[] dp = new int[n + 1];
    
    // Base Case: n = 0 or 1
    dp[1] = 1;

    // Iteration
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}
```

This method is of `O(n)` time and space complexities. We may optimize this particular problem by using constant space.

### gridTraveler

```java 
boolean gridTraveler(int m, int n) {
    
    int[][] dp = new int[m + 1][n + 1];

    // Only one way to traverse 1x1 grid    
    dp[1][1] = 1;

    // Iteration
    for (int i = 0; i <= m; i++) {
        for (int j = ; j <= n; j++) {
            int[] curr = dp[i][j]
            if (j + 1 <= n) dp[i][j + 1] += curr; // Update right
            if (i + 1 <= m) dp[i + 1][j] += curr; // Update bottom
        }
    }

}
```
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

### Steps for DP

1. Visualize the problem as a table
2. Create a table based on the input size
3. Initialize the table with default values
4. Seed the base case / trivial values into the table
5. Iterate through the table
6. Fill further positions based on current position

### canSum

<img src="image-8.png" alt="alt text" style="height: 200px">

```java 
boolean canSum(int targetSum, int[] nums) {
    // Create an array of size targetSum + 1
    boolean[] dp = new boolean[targetSum + 1];

    // We can generate a sum of 0 by taking NO elements
    dp[0] = true;
   
    // Iterate through the table
    for (int i = 0; i <= targetSum; i++) {
        // If the current element is false, move on
        if (dp[i] == false) continue;
        // True means, we can generate this number by summing the array
        // For each number in nums,
        for (int num: nums) {
            // If we can generate the current number, we can also generate current + num
            if (i + num <= targetSum) 
                dp[i + num] = true;
        }
    }
    return dp[targetSum];
}
```

### howSum

<img src="image-9.png" alt="alt text" style="height: 200px">

```java 
List<Integer> howSum(int targetSum, int[] nums) {
    // Create an array 
    List<List<Integer>> dp = new ArrayList<>();
    // Fill the array with null, meaning it's impossible to obtain targetSum
    for (int i = 0; i <= targetSum; i++) {
        dp.add(i, null);
    }

    // We can generate a sum of 0 by taking NO elements
    // Hence if targetSum is 0, we should return an empty array
    dp.add(0, new ArrayList<>());
   
    // Iterate through the table
    for (int i = 0; i <= targetSum; i++) {
        if (dp.get(i) == null) continue;
        // For each number in nums,
        for (int num: nums) {
            if (i + num <= targetSum) 
                // Fill that position in the table
                // also including the value at the current pos
                dp.put(i + num, dp.get(i).add(num));
        }
    }
    return dp.get(targetSum);
}
```

### bestSum

```java 
List<Integer> bestSum(int targetSum, int[] nums) {
    List<List<Integer>> dp = new ArrayList<>();
    
    for (int i = 0; i <= targetSum; i++) dp.add(i, null);

    dp.add(0, new ArrayList<>());
   
    // Iterate through the table
    for (int i = 0; i <= targetSum; i++) {
        if (dp.get(i) == null) continue;
        for (int num: nums) {
            if (i + num <= targetSum) {
                List<Integer> present = dp.get(i + num); 
                List<Integer> newArr = dp.get(i).add(num);
                // If the cell was previously filled (!null)
                // Only replace, if the new combination is shorter
                if (present != null && present.size() > newArr.size())
                    dp.put(i + num, newArr);
            }
        }
    }
    return dp.get(targetSum);
}
```

### canConstruct

```java 

```
```java 

```
```java 

```