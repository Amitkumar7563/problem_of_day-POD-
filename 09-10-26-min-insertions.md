# Minimum Insertions to Balance a Parentheses String

**LeetCode:** [1541. Minimum Insertions to Balance a Parentheses String](https://leetcode.com/problems/minimum-insertions-to-balance-a-parentheses-string/)

**Date:** 09/10/2026

## Intuition

Every `(` must be matched with **two consecutive `))`**.

We use two variables:

- `cnt` → Number of unmatched opening brackets `(`.
- `result` → Number of insertions required so far.

Instead of using a stack, we greedily process the string from left to right and fix imbalances immediately.

## Approach (Greedy)

1. If the current character is `(`, increment `cnt` because it needs two closing brackets.
2. If the current character is `)`:
   - If the next character is also `)`, consume both as a pair.
   - Otherwise, insert one `)` to complete the required pair.
3. Before processing a closing pair, if `cnt == 0`, insert one `(` because there is no opening bracket available to match it.
4. At the end, every unmatched `(` needs two `)` insertions, so add `cnt * 2` to `result`.

## C++ Solution

```cpp
class Solution {
public:
    int minInsertions(string s) {
        int n = s.length();
        int cnt = 0;
        int result = 0;
        int i = 0;

        while (i < n) {
            if (s[i] == '(') {
                cnt++;
                i++;
            } else {
                if (cnt > 0) {
                    cnt--;
                } else {
                    result++;
                }

                if (i + 1 < n && s[i + 1] == ')') {
                    i += 2;
                } else {
                    result++;
                    i++;
                }
            }
        }

        return result + cnt * 2;
    }
};
```

## Dry Run

Input: `s = "(()))"`

| Character(s) | `cnt` | `result` | Explanation |
|---|---:|---:|---|
| `(` | 1 | 0 | One opening bracket needs a pair |
| `(` | 2 | 0 | Another opening bracket |
| `))` | 1 | 0 | Match one opening bracket |
| `)` | 0 | 0 | Match the remaining opening bracket |

Output: `0`

The string is already balanced because each `(` has exactly two corresponding consecutive `)` characters.

## Why This Approach?

- **Greedy:** We fix each imbalance as soon as we encounter it instead of making unnecessary insertions later.
- **No stack required:** We only need to track the number of unmatched opening brackets.
- **Lookahead:** Checking `s[i + 1]` tells us whether the current `)` can form a consecutive `))` pair.
- **Count remaining openings:** Each unmatched `(` requires exactly two closing brackets.

## Complexity Analysis

- **Time:** `O(n)` — Each character is processed at most once.
- **Space:** `O(1)` — Only a few integer variables are used.

## Key Takeaway

For this problem, remember that **every opening bracket requires two consecutive closing brackets**. Greedily match available brackets, insert missing ones immediately, and finally add two insertions for every unmatched opening bracket.
