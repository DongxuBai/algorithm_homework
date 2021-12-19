```java
class Solution {
    public int shipWithinDays(int[] weights, int days) {
        // 第一时间看题就能明显发现，判定问题 000111; 然后找 0 1 交界
        int left = 0;
        int right = 0;
        for (int weight : weights) {
            left = Math.max(left, weight);
            right += weight;
        }
        while (left < right) {
            int mid = (left + right) / 2;
            if (can(mid, days, weights)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }

    boolean can(int mid, int days, int[] weights) {
        int box = 0;
        int count = 1;
        for (int weight : weights) {
            if ((box + weight) <= mid) {
                box += weight;
            } else {
                box = weight;
                count++;
            }
        }
        return count <= days;
    }
}
```