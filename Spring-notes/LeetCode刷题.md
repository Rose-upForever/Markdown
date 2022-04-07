# 741、二分查找

对数组使用二分查找的前提是数组有序并且数组中没有重复的元素。

在本题中，首先进行的时边界判断，因为数组是 有序的，所以只需要将目标值与开头结尾的两个元素进行比较就可以判断数组中是否可能存在目标值。循环执行的终止条件是当left<=right时，并且代码每次执行一次就需要重新计算mid的值。mid值的计算方法为 ***   int mid = left + ((right-left) >> 1)***; 若target的值小于mid 则更新right的值，令其为mid-1；若target的值大于mid，则更新left的值令其为mid + 1；

* **题目描述:**

<img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\1.png" style="zoom:50%;" />

* **代码编写：**

``` java
class Solution {
    public int search(int[] nums, int target) {
        int mark;
        int left = 0;
        int right = nums.length - 1;
        if (target < nums[0] || target > nums[right]){
            return -1;
        }
    while(left <= right){
                int mid = left + ((right-left) >> 1);
                if(target < nums[mid]){
                    right = mid - 1;
                }
                else if(target > nums[mid]){
                    left = mid + 1;
                }
                else if(target == nums[mid]) 
                    return mid;
            }
        return -1;
```

* 二分的两种写法：

while循环的终止判断条件是left<= right.在这种情况下，***若target< nums[mid],则right = mid -1***；若target> nums[mid] 则left = mid +1;

while循环的终止条件是left< right。在这情况下，***若target< nums[mid],则right = mid **；这是两种写法的主要区别。

# 深度优先搜索

## 判断数是否对称

题目描述：

给你一个二叉树的根节点 `root` ， 检查它是否轴对称。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

实际上就是对这颗树的左右子树进行操作。对于左子树，向左执行深度优先比遍历，对于右子树享有执行深度优先遍历，只有上述过程中遍历的每个节点的数值相等，才能判断这棵树是对称的。

~~~ java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root.left,root.right);
    }
    public boolean check(TreeNode p, TreeNode q){
        if(p == null && q == null) return true;
        if(p == null || q == null) return false;
        if(q.val != p.val) return false;
        //左子树向左遍历，右子树向右遍历
        return check(p.left,q.right) && check(p.right,q.left);
    }
}
~~~

# 二进制实现加减乘除操作

## 1、加法操作 

xor:xor表示不考虑进位情况的下的值

forward:forward表示仅考虑进位下的值

加法操作的结果就等于上述两个值的和

~~~java
public class Byte_add{
	public static int add (int a, int b){
		int xor = a ^ b;
		int forward = (a & b) << 1;
		return forward == 0 ? xor : add(xor, forward);
	}
	public static void main(String [] args){
		int a = 115;
		int b = 1;
		int res = add (a,b);
		System.out.println(res);
	}
}
~~~

## 2、实现负数操作

~~~ java
public static int negative(int a ){
    //一个数的负数按照二进制来求的话就是各位取反末尾加一
		return add(~a, 1);
	}
~~~

## 3、实现减法操作

~~~ java
	//加法操作
	public static int add (int a, int b){
		int xor = a ^ b;
		int forward = (a & b) << 1;
	    return forward == 0 ? xor : add(xor, forward) ;
	}

	// 实现负数操作
	public static int negative(int a ){
		return add(~a, 1);
	}
	
	public static int sub(int a, int b){
		return add (a, negative(b));
	}
~~~

## 3、实现乘法操作

乘法的二进制实现主要是让被乘数循环右移。在右移过程中遇到1的时候，则执行加法操作。让当前结果与被乘数左移i位相加，i的值就是代表遇到的1在被乘数二进制字符串中的位置。

~~~ java
public static int multi (int a, int b){
		int i =0;
		int res = 0；
         // 符号判断
		int sign = (a > 0) ^ (b > 0) ? -1 : 1;
		if(b == 0) return 0;
		while(b != 0){
            //如果乘数的最后一位是一的话，则执行加法操作
			if ((b & 1) == 1){
				res = add(res,a << i);
			}
            //乘数右移
			b = b >> 1;
            // i加一
			i = add(i,1);
		}
		return sign == 1 ? res : -res;
	}
~~~



## 4、除法操作

方法一：直接使用减法操作实现：

```java
//使用剑法运算实现除法
	public int divide(int a, int b) {
		// 当a为最小值使，b为-1 此时会产生越界情况;
		int res = 0;
		if (a == 0)
			return res;
		if(b == 0)
			return 0;
        if(a == Integer.MIN_VALUE && b == -1)
        	return Integer.MaxValue;
        int sign = (a > 0) ^ (b > 0) ? -1 : 1;
        // 因为复数的表示范围比正数的表示范围大，所以需要将正数转化为负数，这样统一符号的原因是为了后面的减法运算
        if (a > 0) a = -a;
        if (b > 0) b = -b;
        while(a >= b){
        	a- = b;
       		res++;
       	}
       	res = sign == 1 ? res : -res;
       	return res;
    }
```

方法二：利用左移与右移操作实现



例如计算 22 / 3 ：
22 -  （3 << 2）= 10  1 << 2 = 4

10 -   (3 << 1)  = 4      1 << 1 = 2

4 - (3 << 0) = 1           1 << 0  = 1;

```java
// 使用二进制位运算进行优化
    public divideB(int a, int b){
    	int res = 0;
        int sign = (a > 0) ^ (b > 0) ? -1 : 1;
    	if (a == 0)
    		return 0;
    	if (b == 0)
    		return 0;
        // 当a的值是-2的31次方的时候，如果求其绝对值，则会超越范围，所以要拿出来单独讨论
    	if(a == Integer.MIN_VALUE){
    		if(b == -1) return Integer.MAX_VALUE;
    		if(b == 1)	return Integer.MIN_VALUE;
    	    if (b > 0){
    	    	// >> 算数右移 >>> 逻辑右移 
    	    	for (int i = 31; i >=0; i--) {
    	    		if((a >> i) + b <= 0){
    	    			a += (b << i);
    	    			res += (1 << i); 
    	    		}
    	    	}
    	    	return -res;
            }
    	    else if(b < 0){
    	    	for (int i = 31; i >=0; i--){
    	    		if((a >> i) - b <= 0 ){
    	    			a -= (b << i);
    	    			res += (1 << i);
    	    		}
                }
                return res;
    	    }
        }
        
        
    	a = Math.abs(a);
    	b = Math.abs(b);
        
        // 算法的核心部分；i代表的是b进行左移的位数，当 a > (b << i)的时候，让a减去(b << i). 1 << i 表示减去的了几个b 例如 b = 2 2 << 2 =            8,表示4个2，1 << 2 = 4 ;然后继续让余数进行上述操作。
    	for(int i = 31; i >=0; i--){
    		if ((a >>> i) - b>= 0) {
    			a -= (b << i);
    			res += (1 << i);
    		}
    }
 
    return sign == 1 ? res : -res;
 }
```

# 字符串操作

## 计算二进制字符串的和

算法思想：从后往前遍历两个字符串，然后让两个字符串对应位置的数字和上一次相加的进位进行相加，得到和之后，该和的模位拼接后字符串在该位置上的值，商为进位。

~~~java
public static String addBinary(String a, String b) {
      StringBuilder res = new StringBuilder();
      int l1 = a.length() - 1;
      int l2 = b.length() - 1;
      int add = 0;
      int carry = 0;
      while (l1 >= 0 || l2 >= 0){
      // -'0'表示将一个数字字符转化为整数
         int temp = l1 < 0 ? 0 : a.charAt(l1) - '0';
         int temp1 = l2 < 0 ? 0 :b.charAt(l2) - '0';
         // carry是进位标志位
         add = temp + temp1 + carry;
         // 进行字符串的拼接
         res.append(add % 2);
         carry = add / 2;
         l1 --;
         l2 --;
      }
      if(carry != 0) res.append(carry); 
      // 使用reverse函数可以将字符串逆置
      return res.reverse().toString();
    }
~~~



