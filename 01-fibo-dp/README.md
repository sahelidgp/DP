# Recursive Fibonacci Code🫠

```c++
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n <= 1)
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    cout << "Enter the position: ";
    cin >> n;

    cout << "Fibonacci number at position " << n << " is " << fibonacci(n) << endl;
    return 0;
}

```

Time Complexity (TC)
T(n) = T(n - 1) + T(n - 2) + O(1)

This recurrence solves to O(2ⁿ).

👉 The recursive solution is exponential time because it recomputes the same subproblems multiple times.

Space Complexity (SC)
The maximum depth of the recursion tree is O(n) (due to the call stack).

So, the space complexity is O(n).

🔹 Summary:
Metric	Complexity
Time	O(2ⁿ)

Space	O(n)

# 1. Optimized Recursive Fibonacci (Memoization / Top-Down DP)😉

```c++
#include <iostream>
#include <vector>
using namespace std;

int fibonacci(int n, vector<int>& dp) {
    if (n <= 1)
        return n;

    if (dp[n] != -1) // already computed
        return dp[n];

    return dp[n] = fibonacci(n - 1, dp) + fibonacci(n - 2, dp);
}

int main() {
    int n;
    cout << "Enter the position: ";
    cin >> n;

    vector<int> dp(n + 1, -1); // initialize with -1
    cout << "Fibonacci number at position " << n << " is " << fibonacci(n, dp) << endl;

    return 0;
}

```

✅ Time Complexity:
O(n) → each subproblem is solved only once.

✅ Space Complexity:
O(n) for the recursion stack.

O(n) for the dp array.

Total: O(n) space.

# 2. Iterative Fibonacci (Bottom-Up DP with O(n) Space)🧟

```c++
#include <iostream>
#include <vector>
using namespace std;

int fibonacci(int n) {
    if (n <= 1)
        return n;

    vector<int> dp(n + 1);
    dp[0] = 0;
    dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}

int main() {
    int n;
    cout << "Enter the position: ";
    cin >> n;

    cout << "Fibonacci number at position " << n << " is " << fibonacci(n) << endl;

    return 0;
}

```
✅ Time Complexity: O(n) 

✅ Space Complexity: O(n) for dp array no recursion stack space 

# 3. Most Optimized Fibonacci (Iterative with O(1) Space)👻


```c++
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n <= 1)
        return n;

    int prev2 = 0, prev1 = 1, curr;

    for (int i = 2; i <= n; i++) {
        curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    return curr;
}

int main() {
    int n;
    cout << "Enter the position: ";
    cin >> n;

    cout << "Fibonacci number at position " << n << " is " << fibonacci(n) << endl;

    return 0;
}

```

✅ Time Complexity: O(n)

✅ Space Complexity: O(1) (Only using 3 variables)


# 📌 Final Comparison Table:

| Approach                      | Time Complexity | Space Complexity |
| ----------------------------- | --------------- | ---------------- |
| Recursive (Naive)             | O(2ⁿ)           | O(n)             |
| Recursive + Memoization (DP)  | O(n)            | O(n)             |
| Iterative (DP with array)     | O(n)            | O(n)             |
| Iterative (Optimized, 3 vars) | O(n)            | O(1)             |
