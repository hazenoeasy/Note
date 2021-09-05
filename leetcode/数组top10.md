# 15 三数之和
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

