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
## 方法1 深度遍历
    深度遍历（递归） 将相邻的变为 ‘0’
```
class Solution {
    public int lr,lc;
    public int numIslands(char[][] grid) {
        lr = grid.length;
        lc = grid[0].length;
        int count = 0;
        for(int i=0;i<lr;i++){
            for(int j=0;j<lc;j++){
                if(grid[i][j]=='1'){
                    count++;
                    dfs(grid,i,j);
                }
            }
        }
        return count;
    }
    private void dfs(char[][] grid, int i,int j){
        if(i<0 || j<0 || i>=lr || j>=lc){
            return;
        }
        if(grid[i][j]=='1'){
            grid[i][j]='0';
            dfs(grid,i+1,j);
            dfs(grid,i-1,j);
            dfs(grid,i,j+1);
            dfs(grid,i,j-1);
        }
    }

}
```
注意边界情况
```
if (grid == null || grid.length == 0) {
            return 0;
        }
```
## 方法2 广度遍历
```
class Solution {
    public int lr,lc;
    public int numIslands(char[][] grid) {
        lr = grid.length;
        lc = grid[0].length;
        int count = 0;
        for(int i=0;i<lr;i++){
            for(int j=0;j<lc;j++){
                if(grid[i][j]=='1'){
                    count++;
                    Deque<Integer> neighbor = new ArrayDeque<>();
                    neighbor.addLast(lc*i+j);
                    while(!neighbor.isEmpty()){
                        int e = neighbor.removeLast();
                        int r=e/lc;
                        int c =e%lc;
                        if(r+1<lr && grid[r+1][c]=='1'){
                            grid[r+1][c]='0';
                            neighbor.addLast(e+lc);
                        }
                        if(r-1>=0 && grid[r-1][c]=='1'){
                            grid[r-1][c]='0';
                            neighbor.addLast(e-lc);
                        }
                        if(c+1<lc && grid[r][c+1]=='1'){
                            grid[r][c+1]='0';
                            neighbor.addLast(e+1);
                        }
                        if(c-1>=0 && grid[r][c-1]=='1'){
                            grid[r][c-1]='0';
                            neighbor.addLast(e-1);
                        }
                    }
                }

            }
        }
        return count;
    }
}
```
广度优先 需要注意维护栈
## 方法3 
    并查集 https://leetcode-cn.com/problems/number-of-islands/solution/dao-yu-shu-liang-by-leetcode/
11. 盛最多水
## 方法1
    双指针+贪心算法
```
class Solution {
    public int maxArea(int[] height) {
    int max = 0;
    int length = height.length;
    int l=0;
    int r=length-1;
    while(l<r){
        max=Math.max(max,Math.min(height[l],height[r])*(r-l));
        if(height[l]<height[r]){
            l++;         
        }else{
            r--;
        }
    }
    return max;
    }
}
```
54. 螺旋矩阵
## 方法 
    模拟

```
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> order = new ArrayList<Integer>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return order;
        }
        int rows = matrix.length, columns = matrix[0].length;
        int total = rows * columns;
        int row = 0, column = 0;
        int[][] directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int directionIndex = 0;
        for (int i = 0; i < total; i++) {
            order.add(matrix[row][column]);
            matrix[row][column]=101;
            int nextRow = row + directions[directionIndex][0], nextColumn = column + directions[directionIndex][1];
            if (nextRow < 0 || nextRow >= rows || nextColumn < 0 || nextColumn >= columns || matrix[nextRow][nextColumn]==101) {
                directionIndex = (directionIndex + 1) % 4;
            }
            row += directions[directionIndex][0];
            column += directions[directionIndex][1];
        }
        return order;
    }
}
```
56. 合并区间

912. 排序数组
## 方法1： 快速排序
```
class Solution {
    Random r = new Random();
    public int[] sortArray(int[] nums) {
        int length = nums.length;
        int first = 0;
        int last = length-1;
        fastSort(nums,first,last);
        return nums;
    }
    private void fastSort(int[] nums, int first, int last){
        if(first<last){
            int pivot = position(nums,first,last);
            fastSort(nums,first,pivot-1);
            fastSort(nums,pivot+1,last);
        }
    }
    private int position(int[] nums,int first, int last){
        int pivot = r.nextInt((last-first)+1)+first;
        swap(nums,first,pivot);
        int index = first+1;
        for(int i=index;i<=last;i++){
            if(nums[i]<nums[first]){
                swap(nums,i,index);
                index++;
            }
        }
        index=index-1;
        swap(nums,first,index);
        return index;
    }
    
    private void swap(int[] nums, int first,int last){
        int temp = nums[first];
        nums[first] = nums[last];
        nums[last] = temp;
    }
}
```
## 方法2
    堆排序
## 方法3
    归并排序
56. 合并区间
##  方法1 排序+合并
- Java sort用法comparator
    可以实现comparator接口 来实现排序方法       comparator返回 正负
    ```
    Arrays.sort(intervals, new Comparator<T>() {
            public int compare(T interval1, T interval2) {
                return interval1[0] - interval2[0];
            }
        });
    ```
- 还可以用Lamda写
```
   Arrays.sort(intervals, (v1, v2) -> v1[0] - v2[0]);
```
```
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals,new Comparator<int[]>(){
            public int compare(int[] t1,int[] t2){
                return t1[0]-t2[0];
            }
        });
    List<int[]> res = new ArrayList<>();
    for(int[] interval: intervals){
        if(res.isEmpty() || res.get(res.size()-1)[1]<interval[0]){
            res.add(interval);
        }else{
            int[] temp = res.get(res.size()-1);
            temp[1]=Math.max(temp[1],interval[1]);
        }
    }
    return res.toArray(new int[res.size()][]);    
    }
}
```
注意事项:
List变为数组 可以用 toArray();
但元素会变为object
因此 需要指明list结构 
``
return res.toArray(new int[res.size()][]);   
``

739. 每日温度
     
740. 最接近的三个数之和
     