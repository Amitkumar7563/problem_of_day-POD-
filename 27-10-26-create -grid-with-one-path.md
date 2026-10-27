# LeetCode Notes: Create Grid With Exactly One Path

**Topic:** Constructive Algorithms, Grid, Implementation  
**Goal:** Similar constructive problems ko independently solve karna.

## 1. Meri actual problem kya thi?

Main solution dekhkar code samajh sakta tha, lekin khud se code implement nahi kar paaya.

Iska matlab mujhe sirf syntax nahi, balki ye 3 skills improve karni hain:

1. Problem statement se important conditions identify karna.
2. Conditions ko grid ke pattern mein convert karna.
3. Pattern ko loops aur indexing se implement karna.

**Lesson:** Solution samajhna aur bina help ke solution banana alag skills hain.

---

## 2. Problem ko apni language mein samjho

Humein `m × n` grid banana hai jisme:

- `.` = open cell
- `#` = blocked cell
- Start = top-left `(0,0)`
- Destination = bottom-right `(m-1,n-1)`
- Movement sirf right aur down allowed hai.
- Start se destination tak exactly one valid path hona chahiye.

**Main question:** Grid ko kaise design karein taaki ek path possible ho, lekin doosra path na ho?

Yahan mujhe har possible path count nahi karna. Main grid ko aise construct kar sakta hoon ki alternate paths ban hi na paayein.

---

## 3. Observation kaise nikalein?

### Step 1: Ek simple path imagine karo

Start se destination tak pahunchne ka easiest way:

- Pehle first row mein right move karo.
- Phir last column mein down move karo.

Example, `m = 3, n = 4`:

```text
....
###.
###.
```

Yahan ek continuous path hai:

```text
(0,0) → (0,1) → (0,2) → (0,3)
                                  ↓
                               (1,3)
                                  ↓
                               (2,3)
```

### Step 2: Alternate paths ko roko

Agar hum saare cells open kar dein, toh multiple paths ho sakte hain.

Isliye:
- Required path ke cells ko `.` banao.
- Baaki sab cells ko `#` rakho.

**Core observation:** Pehle ek simple valid path choose karo, phir unnecessary routes block kar do.

### Step 3: Grid ka pattern identify karo

Required open cells:
- First row: `grid[0][j]`
- Last column: `grid[i][n-1]`

C++ mein indexing zero se start hoti hai. Isliye last column ka index `n-1` hoga.

---

## 4. Logic se code tak kaise pahunchein?

Code likhne se pehle implementation ko 3 steps mein divide karo.

### Step A: Initial grid banao

```cpp
vector<string> grid(m, string(n, '#'));
```

Socho:
- Kitni rows? `m`
- Har row mein kitne characters? `n`
- Initial character? `#`

Agar `m = 3, n = 4`:

```text
####
####
####
```

### Step B: First row open karo

```cpp
for (int j = 0; j < n; j++) {
    grid[0][j] = '.';
}
```

**Loop variable `j` kyun?**

Row fixed hai: `0`.

Column change ho raha hai: `0` se `n-1`.

Isliye `j` column index represent karta hai.

### Step C: Last column open karo

```cpp
for (int i = 0; i < m; i++) {
    grid[i][n - 1] = '.';
}
```

**Loop variable `i` kyun?**

Column fixed hai: `n-1`.

Row change ho rahi hai: `0` se `m-1`.

Isliye `i` row index represent karta hai.

---

## 5. Final implementation

```cpp
class Solution {
public:
    vector<string> createGrid(int m, int n) {
        vector<string> grid(m, string(n, '#'));

        for (int j = 0; j < n; j++) {
            grid[0][j] = '.';
        }

        for (int i = 0; i < m; i++) {
            grid[i][n - 1] = '.';
        }

        return grid;
    }
};
```

### Dry run: `m = 3, n = 4`

| Operation | Grid |
|---|---|
| Initialize | `#### / #### / ####` |
| First row open | `..../ #### / ####` |
| Last column open | `..../ ###. / ###.` |

Final grid:

```text
....
###.
###.
```

Time complexity: `O(m × n)` because the grid initialization dominates.

Space complexity: `O(m × n)` for the output grid.

---

## 6. Future mein similar question aaye toh kya karna hai?

Har constructive grid problem mein ye checklist use karna.

### My problem-solving checklist

1. **Requirement:** Exactly kya banana hai?
2. **Rules:** Movement, allowed cells aur restrictions kya hain?
3. **Small example:** `2 × 2` ya `3 × 3` grid draw karo.
4. **Construct:** Sabse simple valid structure imagine karo.
5. **Prevent alternatives:** Unwanted paths ya patterns ko kaise rokenge?
6. **Initialize:** Sab cells ko default value do.
7. **Modify:** Sirf required cells ko change karo.
8. **Verify:** Kya saari conditions satisfy hoti hain?
9. **Test edge cases:** Minimum dimensions aur unusual dimensions check karo.
10. **Implement without help:** Pehle khud code likho, phir solution compare karo.

---

## 7. Similar questions mein observation kaise change hogi?

- **Exactly one path:** Ek route construct karo aur alternate routes prevent karo.
- **At least one path:** Valid route ensure karna important hai; unnecessary restrictions zaroori nahi.
- **No path:** Start aur destination ke beech connectivity break karo.
- **Exactly `k` paths:** Aisa structure design karna hoga jahan valid paths ki count controlled ho. Iske liye naya observation aur proof chahiye.
- **Pattern generation:** Pehle expected pattern paper par draw karo, phir fixed rows/columns ko loops se fill karo.

Yaad rakho: Ye general hints hain, har problem ka solution isi pattern se nahi niklega.

---

## 8. Practice plan: Help se independence tak

**Attempt 1 — Aaj:** Notes padho aur code samjho.

**Attempt 2 — Kuch der baad:** Notes band karke problem dobara solve karo.

**Attempt 3 — Agle din:** Problem statement se start karo. Pehle grid draw karo, phir loops likho.

**Attempt 4 — Kuch din baad:** Ek similar constructive problem solve karo, bina solution dekhe.

Jab tak tum blank editor mein khud se solution nahi likh paate, tab tak problem ko fully mastered mat samajhna.

---

## Final takeaway

Meri biggest learning ye hai:

**"Pehle structure socho, phir us structure ko code mein convert karo."**

Mujhe har baar poora code yaad nahi karna. Mujhe ye seekhna hai ki:
- Kya initialize karna hai?
- Kaunse cells change karne hain?
- Kaunsa index fixed hai?
- Kaunsa index loop mein change hoga?
- Solution ki correctness kaise verify karni hai?

Ye skills improve hongi toh constructive algorithm wale naye questions mein bhi approach develop karna easier hoga.
