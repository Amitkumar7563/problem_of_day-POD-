# Minimum Operations to Sort a String

**Problem:** [LeetCode — Minimum Operations to Sort a String](https://leetcode.com/problems/minimum-operations-to-sort-a-string/description/)  
**Topic:** Greedy / String  


## 1. Core Intuition 💡

Humein string ko ascending order mein sort karna hai using the allowed operations.

**Key idea:** Har character ki exact position check karne ke bajay, first aur last character ko analyze karo.

- Agar string already sorted hai → `0` operations.
- Agar length `2` hai aur sorted nahi hai → `-1`.
- Agar first character minimum hai ya last character maximum hai → `1` operation.
- Agar first character middle ke maximum se bada aur last character middle ke minimum se chhota hai → `3` operations.
- Otherwise → `2` operations.

## 2. Implementation Way

### Step 1: Already sorted check
`is_sorted()` check karta hai ki string ascending order mein hai ya nahi.

### Step 2: Impossible case
Length `2` ki unsorted string ko allowed operations se sort nahi kar sakte.

### Step 3: Global minimum and maximum
- `min_element()` → smallest character.
- `max_element()` → largest character.

Agar `s[0] == min_char` ya `s[l-1] == max_char`, answer `1` hai.

### Step 4: Middle characters check
```cpp
char max_mid = *max_element(s.begin() + 1, s.end() - 1);
char min_mid = *min_element(s.begin() + 1, s.end() - 1);
```

Ye first aur last character ko exclude karke middle ka maximum aur minimum find karta hai.

Agar first character middle ke maximum se bada hai aur last character middle ke minimum se chhota hai, answer `3`; otherwise `2`.

## 3. Important C++ Details

- `*max_element(...)`: iterator ko dereference karke actual character milta hai.
- `s[0]`: first character.
- `s[l-1]`: last character.
- `s.begin()+1`: second character se start.
- `s.end()-1`: last character se pehle tak.
- `is_sorted()` ascending order check karta hai.

## 4. Complexity

- **Time:** \(O(n)\)
- **Auxiliary Space:** \(O(1)\)

String par kuch constant-count linear scans hote hain; extra space constant hai.

## 5. Key Takeaway

**Greedy observation:** Puri string ko sort karne ke bajay, uske extreme characters aur middle range ki properties se minimum operations determine kar sakte hain.
