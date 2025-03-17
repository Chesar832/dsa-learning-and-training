# 349. Intersection of Two Arrays

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        
        intersection = []

        for i in nums1: # O(n)
            if i in nums2 and i not in intersection: # O(m) and O(p)
                intersection.append(i)
        
        return intersection
```

- State: Accepted
- Time Complexity: $O(n * (m + p))$