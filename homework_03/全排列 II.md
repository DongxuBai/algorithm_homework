# 47. 全排列 II
```java
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<Integer> list = Arrays.stream(nums).boxed().collect(Collectors.toList());
        recur(null, list);
        return ans;
    }

    public void recur(List<Integer> subAns, List<Integer> list) {
        if (list.size() == 0) return;
        if (subAns == null) {
            subAns = new ArrayList<>();
        }
        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < list.size(); i++) {
            // 重复跳过
            int val = list.get(i);
            if (set.contains(val)) continue;
            subAns.add(val);
            set.add(val);
            if (list.size() == 1) {
                ans.add(new ArrayList<>(subAns));
            }
            List<Integer> nextList = new ArrayList<>(list);
            nextList.remove(i);
            recur(new ArrayList<>(subAns), nextList);
            subAns.remove(subAns.size() - 1);
        }
    }
}
```