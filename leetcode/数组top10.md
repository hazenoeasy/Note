15. 三数之和
## 解决方法： 
    先排序 再前后指针 再去重
## 为什么排序？ 
    要找所有的
## 为什么双指针？ 
    一个递增 一个递减 就可以双指针
## 语法注意点：
```
ans.add(Arrays.asList(nums[i],nums[L],nums[R]));
```
为list添加一个list元素 可以选用 Array.asList 将元素转化为list
```
List<List<Integer>> ans = new ArrayList<List<Integer>>();
List<List<Integer>> ans = new ArrayList<>();(自动匹配)
List<List<Integer>> ans = new ArrayList<ArrayList<Integer>>();
ArrayList<ArrayList<Integer>> cannot be converted to List<List<Integer>> ？？
```
二维list的声明方式
ArrayList<T>是List<T>的子类
但T变了 不能算继承了

46. 全排列 https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/
## 解决方法：
    回溯
## 为什么回溯
    需要求所有解

    动态规划只需要求我们评估最优解是多少，最优解对应的具体解是什么并不要求。因此很适合应用于评估一个方案的效果；
    回溯算法可以搜索得到所有的方案（当然包括最优解），但是本质上它是一种遍历算法，时间复杂度很高。
## 语法注意点：
- booleam默认初始化为false
- boolean和Boolean不一样   boolean是基本类型 Boolean是封装类 有属性有方法，可以new； 一般用boolean就足够
- ArrayList初始化 可以在括号中添加一个集合
- Deque

215. 数组中的第k个最大元素
## 方法1：
    随机快速排序+ 快速选择
## 为什么用快速排序？
    因为需要求第k个最大值，不需要让整个数组有序。 快速选择->二分法思想 加速
    随机pivot 可以极快加速算法
## 方法2： 
    堆排序
## 为什么用堆排序？ 
    堆排序可以依次知道最大值 https://www.pdai.tech/md/algorithm/alg-sort-x-heap.html#%E5%A0%86%E6%8E%92%E5%BA%8F%E5%AE%9E%E7%8E%B0

200. 岛屿数量

11. 盛最多水

54. 螺旋矩阵

56. 合并区间

912. 排序数组

739. 最接近的三个数之和
     