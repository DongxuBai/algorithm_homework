```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        // sum[l, r] = s[r] - s[l - 1]; (l <= r)
        // => s[i] - s[j] == k (j < i);
        int n = nums.length;
        int[] s = new int[n + 1];
        for (int i = 1; i <= n; i++) s[i] = s[i - 1] + nums[i - 1];
        
        Map<Integer, Integer> map = new HashMap<>();
        map.put(s[0], 1);

        int ans = 0;
        for (int i = 1; i <= n; i++) {
            // s[j] = s[i] - k
            Integer times = map.get(s[i] - k);
            if (times != null) {
                ans += times;
            }
            map.put(s[i], (map.get(s[i]) == null ? 1 : (map.get(s[i]) + 1)));
        }
        return ans;
    }
}
```