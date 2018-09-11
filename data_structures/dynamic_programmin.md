# Dynamic Programming

 Keeping track of work that was done already, and using that work to solve problems we already saw in constant time. It's dynamic because the record of the work we already done is being updated in real-time. 
 ## Top-Down
 * Often refered to as **momoization**.
 * typical of recursive implementation that depend on solutions further down the chain.
 * build your stacks and save the work to a cache as you bubble up - subsequent calls to the same function within any given stack can pull the answer out of the cache without incurring more fucntions calls.

 ## Bottom-Up
 * Uses smaller solutions as the basis of later solutions
 * Typical of iterative implementations
 * Can use a cache as well, but builds it from the ground up without incurring additionl stacks.

 ## Top-Down fibonacci
 ```ruby
  class Fiboncci
    def initialize
      @cache = { 1 => 1, 2 => 1 }
    end

    def fibonacci(n)
      # return 1 if n == 1 || n == 2
      # Check our cache instead of the original base case
      return @cache[n] if @cache[n]

      # record the asnwer in our cache before returning it
      ans = fibonacci(n - 1) + fibonacci(n - 2)
      @cache[n] = and
      ans
    end
  end
 ```

 ## Bottom-Up Fibonacci
 ```ruby
  def fib_cache_builder(n)
    #builds the cache, starting at 1 and ending at 1
    cache = { 1 => 1, 2 => 1}
    return cache if n < 3
    (3..n).each do |i|
      cache[i] = cache[i-1] + cache[i-2]
    end
    cache

  end

  def fibonacci(n)
    # calls the helper function
    cache = fib_cache_builder(n)
    # Retunrs the nth entry
    cache[n]

  end
 ```

 ## Longest increasing subsequence
 ```ruby
  def longest_sub(arr)
    # Create an array of length arr.size to       place the longest subsequence which         terminates at each index
    longest = Array.new(arr.size) { Array.new }

    # Base case
    longest[0] << arr[0]

    #Starting at 1 iterate through the longest sequence to that point
    (1...arr.size).each do |i|
      (0...i).each do |j|

    # As we iterate up to i, if arr[i] is less than arr[j] and if what we have stored as the candidate for longest[i] is shorter than what we could make by selecting a new sequence, then we store that as the longest[i] (must dup it)
        if arr[j] < arr[i] && longest[i].size <      longest[j].size
          longest[i] = longest[j].dup
        end
      end
    end
    longest[i] << arr[i]
  end
 ```

 ## Burglar Problem
 given an array [1, 5, 16, 20, 3, 7, 10, 5, 10, 25, 17], each number is a value of house in a neighberhood. If you are a burglar, what is the maximum amount we can get, providing that you don't rob consecutive houses. So can't rob 16 and 20 because they're neighbors.
 ### Similiar to the Knapsack problem

 * keep track of subsolutions
 * each decision relies on relationship with subsolutions

 To solve, keep a record of the max amount in at each iteration in a seperate array as we loop through the array, which will look like this: 
  * [1, 5, 17, 25, 25, 32, 35, 37, 45, 62, 62]

## Max. Sum to leaf
given a tree, find the largest sum possible by taking a direct route from the root downwards. If a node has only one child, assume it is a left child

```javascript
  maxSum(node) {
    if (!node.left && !node.right) {
      return node.val
    }
    if (!node.right) {
      return node.val + maxSum(node.left)
    }

    return Math.max(maxSum(node.left) + node.val, maxSum(node.right) + node.val)
  }
```