# 349. Intersection of Two Arrays

## My solution

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        
        intersection = []

        for i in nums1: # O(n)
            if i in nums2 and i not in intersection: # O(m) and O(p)
                intersection.append(i)
        
        return intersection
```
- Time complexity: $O(n * (m + p))$


## Another Solution (using hashmap)
```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        
        # Creation of hashmap
        hashmap = {}

        for num in nums1: # O(n)
            hashmap[num] = hashmap.get(num, 0) + 1
        
        result = []

        for num in nums2: # O(m)
            if num in hashmap: # O(1)
                result.append(num) # O(1) 
                del hashmap[num] # O(1)

        return result
```
- Time complexity: $O(m + n)$

