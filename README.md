# LEETCODE-Array-2191
Let's perform a dry run of the `sortJumbled` method in the `Solution` class using a specific example to understand its functionality.

### Example Input:
- `mapping`: `[8, 9, 4, 0, 2, 1, 3, 5, 7, 6]`
- `nums`: `[990, 332, 981]`

### Step-by-Step Execution:

1. **Initialization:**
   - `ans` is initialized as a new array of length `nums.length` (i.e., 3).
   - `A` is initialized as an empty list.

2. **Populating List `A`:**
   - For each element in `nums`, we calculate its mapped value and store it along with its index and original value in list `A`.

   #### Iteration 1 (i = 0):
   - `num = 990`
   - `getMapped(990, mapping)`:
     - Convert `990` to a string and iterate through its characters:
       - `'9'` → `6` (mapping[9])
       - `'9'` → `6` (mapping[9])
       - `'0'` → `8` (mapping[0])
     - Mapped value: `6668`
   - Add `[6668, 0, 990]` to `A`.

   #### Iteration 2 (i = 1):
   - `num = 332`
   - `getMapped(332, mapping)`:
     - Convert `332` to a string and iterate through its characters:
       - `'3'` → `0` (mapping[3])
       - `'3'` → `0` (mapping[3])
       - `'2'` → `4` (mapping[2])
     - Mapped value: `004`
   - Add `[004, 1, 332]` to `A`.

   #### Iteration 3 (i = 2):
   - `num = 981`
   - `getMapped(981, mapping)`:
     - Convert `981` to a string and iterate through its characters:
       - `'9'` → `6` (mapping[9])
       - `'8'` → `7` (mapping[8])
       - `'1'` → `9` (mapping[1])
     - Mapped value: `679`
   - Add `[679, 2, 981]` to `A`.

   **State of `A` after iteration:**
   ```
   A = [[6668, 0, 990], [004, 1, 332], [679, 2, 981]]
   ```

3. **Sorting List `A`:**
   - Sort `A` by the mapped value (`a[0]`). If mapped values are equal, sort by index (`a[1]`).
   - Sorted `A`:
   ```
   A = [[4, 1, 332], [679, 2, 981], [6668, 0, 990]]
   ```

4. **Extracting Sorted Values:**
   - Map the sorted list `A` to an array containing only the original numbers:
   ```
   ans = [332, 981, 990]
   ```

### Output:
- The sorted array is `[332, 981, 990]`.

### Full Execution with Code:
```java
import java.util.*;

class Solution {
  public int[] sortJumbled(int[] mapping, int[] nums) {
    int[] ans = new int[nums.length];
    List<int[]> A = new ArrayList<>(); // (mapped, index, num)

    for (int i = 0; i < nums.length; ++i)
      A.add(new int[] {getMapped(nums[i], mapping), i, nums[i]});

    Collections.sort(A, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
    return A.stream().mapToInt(a -> a[2]).toArray();
  }

  private int getMapped(int num, int[] mapping) {
    StringBuilder sb = new StringBuilder();
    for (final char c : String.valueOf(num).toCharArray())
      sb.append(mapping[c - '0']);
    return Integer.parseInt(sb.toString());
  }

  public static void main(String[] args) {
    Solution solution = new Solution();
    int[] mapping = {8, 9, 4, 0, 2, 1, 3, 5, 7, 6};
    int[] nums = {990, 332, 981};
    int[] sortedNums = solution.sortJumbled(mapping, nums);
    System.out.println(Arrays.toString(sortedNums)); // Output: [332, 981, 990]
  }
}
```

### Explanation:
- The method maps each number in `nums` according to the `mapping` array, sorts them based on the mapped values, and then returns the sorted original numbers.
