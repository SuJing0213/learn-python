## twoSum

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

> 给定 nums = [2, 7, 11, 15], target = 9
  因为 nums[0] + nums[1] = 2 + 7 = 9
  所以返回 [0, 1]

```python
class Solution:

  def twoSum(self, nums: List[int], target: int) -> List[int]:
     for i in range(0,len(nums)) :
      	for j in range(i+1,len(nums)):
         	if nums[i] + nums[j] == target:
           	return [i,j]

```

![01](01.png)


```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
	d = {}
	for i, n in enumerate(nums): 
	    if n in d: return [d[n], i]
      d[target-n] = i
```