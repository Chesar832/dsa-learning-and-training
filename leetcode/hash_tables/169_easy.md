# 169. Majority element

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        
        threshold = len(nums) / 2 # O(1)

        hashmap = {} # O(1)

        for i in nums: # O(n)
            hashmap[i] = hashmap.get(i, 0) + 1 # O(1)

            if hashmap[i] > threshold: # O(1)
                return i
```
- Time complexity: $O(n)$
