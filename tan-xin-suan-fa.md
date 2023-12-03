---
description: 贪心算法
---

# 贪心算法

## [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)

思路：

* 贪心求解，
* i 每次移动只能在 cover 的范围内移动，每移动一个元素，cover 就会得到当前元素数值（`nums[i]`），然后继续移动 i。
* 如果 cover 大于等于 终点下标 `len(nums)-1`，那就可以返回 True。

```go
func canJump(nums []int) bool {
    cov := 0
    if len(nums) == 1 {
        return true
    }

    for i := 0; i <= cov; i++ {
        cov = max(cov, i + nums[i])
        if cov >= len(nums)-1 {
            return true
        }
    }

    return false
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

## [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)

思路：

* 贪心求解
* 记录两个范围，一个当前的最大覆盖范围，一个是下一步的最大覆盖范围。
  * 如果下标到了当前这一步最大覆盖范围但是还没有到终点，那就再加一步。

```go
func jump(nums []int) int {
    n := len(nums)
    if n == 1 {
        return 0
    }

    curr, next := 0, 0 // curr 当前覆盖的最远距离下标；next 下一步覆盖的最远距离下标
    step := 0          // 记录走的最大步数
    for i := 0; i < n - 1; i++ {
        next = max(nums[i]+i, next)
        if i == curr { // 遇到当前覆盖的最远距离下标
            curr = next
            step++
        }
    }
    return step
}
```



## [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

思路：

* 要想利润最大，最好就是在最低点买入（min 记录最小价格），然后在第 i 填卖出，
  * `利润 = nums[i]- min`
* 遍历数组找到最低点买入价格。

```go
func maxProfit(prices []int) int {
    // 时间复杂度：O(n)
    // 空间复杂度：O(1)
    min := prices[0]
    maxprofit := 0
    for i := 0; i < len(prices); i++ {
        if prices[i] < min {
            min = prices[i]
        } else if prices[i] - min > maxprofit {
            maxprofit = prices[i] - min
        }
    }
    return maxprofit
}
```

## [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

思路：

* 将利润分解为每天为单位的维度，
  * 股票价格  7, 1, 5, 10, 3, 6, 4
  * 每天利润  0, -6, 4, 5, -7, 3, -2
  * 贪心的思路：只保留正收入，4+5+3=12

```go
func maxProfit(prices []int) int {
    res := 0
    for i := 1; i < len(prices); i++ {
        res += max(prices[i]-prices[i-1],  0) // 只去正的利润
    }
    return res
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

## [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

```go
func maxSubArray(nums []int) int {
    ans := -1 << 32
    minPreSum := 0
    preSum := 0
    for _, num := range nums {
        preSum += num                      // 当前前缀和
        ans = max(ans, preSum - minPreSum) // 当前点缀和 - 最小前缀和
        minPreSum = min(minPreSum, preSum) // 更新最小前缀和
    }
    return ans
}

// https://leetcode.cn/problems/maximum-subarray/?envType=study-plan-v2&envId=top-100-liked
```





