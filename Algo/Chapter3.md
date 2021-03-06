## Nine Chapter Class 3

#### 二叉树（BST）/ 排序

BST 可以重复。定义上 左 < 父， 右 >= 父
### 模板
### 1. DFS/ Divide & Conquer /Morris
```java
Template 1: Traverse

public class Solution {
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        // do something with root
        traverse(root.left);
        // do something with root
        traverse(root.right);
        // do something with root
    }
}


Tempate 2: Divide & Conquer

public class Solution {
    public ResultType traversal(TreeNode root) {
        // null or leaf
        if (root == null) {
            // do something and return;
        }
        
        // Divide
        ResultType left = traversal(root.left);
        ResultType right = traversal(root.right);
        
        // Conquer
        ResultType result = Merge from left and right.
        return result;
    }
}

Template 3: Morris

void morris_inOrder(BiTree T) {
    BNode *p = T, *temp;
    while(p != NULL) {
        if(p->left == NULL) {
            printf("%4c",p->ch);
            p = p->right;
        } else {
            temp = p->left;
            while(temp->right != NULL && temp->right != p) {
                temp = temp->right;
            }
            if(temp->right == NULL) {
                temp->right = p;
                // 前序 printf("%4c",p->ch);
				p = p->left;
            } else {
                temp->right = NULL;
				printf("%4c",p->ch);
                p = p->right;
            }
        }
    }
	
Template 4: While Loop (in/post order 比较难, preorder 直接可以写)
 public List<Integer> postorderTraversal(TreeNode root) {
        // write your code here
        List<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        
        if (root == null) {
            return result;
        }
        TreeNode node = root;
        // push all left nodes
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
        while (!stack.empty()) {
            node = stack.peek();
            if (node.right != null) {
                node = node.right;
                stack.push(node);
                while (node.left != null) {
                    stack.push(node.left);
                    node = node.left;
                }
            } else {
                node = stack.pop();
                result.add(node.val);
                while (!stack.empty() && stack.peek().right == node) {
                    node = stack.pop();
                    result.add(node.val);
                }
            }
        }
        return result;
    }
```
[Morris Traversal遍历二叉树 ](https://www.jianshu.com/p/d2059062efac)

### 2. while 循环的 inorder, postorder traversal。
见Problem中 Binary Tree 的第二题。

### 2. BFS
while 队列循环 + for循环。见Problem 中 BFS，  Binary Tree Level Order Traversal


### 3. Quick Sort
```java


/*
* Quick Select/ 
* （1）
* （2）全部都加等号。然后用一个if来判断是否交换。
*/
private void quickSort(int[] A, int start, int end) {
      if (start >= end) {
          return;
      }

      int left = start;
      int right = end;

      int pivot = A[(start + end) / 2];
      while(left <= right) {
          while(left <= right && A[left] < pivot) {
              left++;
          }
          while(left <= right && A[right] > pivot) {
              right--;
          }

          if (left <= right) {
              int temp = A[left];
              A[left] = A[right];
              A[right] = temp;
              left++;
              right--;
          }

      }
      quickSort(A, start, right);
      quickSort(A, left, end);
  }
```

### 4. Merge Sort
- [ ] [Sort LinkedList](https://www.lintcode.com/problem/sort-integers-ii/description)
- [ ] [Merge Sort来写数组排序](https://www.lintcode.com/problem/sort-integers-ii/description)
### 5. Heap Sort
- [ ] [Heap Sort写数组排序](https://www.lintcode.com/problem/sort-integers-ii/description)
### 6. 排序总结
桶排序：先划分成若干个桶(比如用map，0-9/10-19/.../)， 桶内排序以后再合并。
稳定的排序: 
稳定性得好处：从一个键上排序，然后再从另一个键上排序，第一个键排序的结果可以为第二个键排序所用。

各排序算法的稳定性：

1、堆排序、快速排序、希尔排序、直接选择排序不是稳定的排序算法；

2、基数（桶）排序、冒泡排序、直接插入排序、折半插入排序、归并排序是稳定的排序算法。

冒泡：
```java
void bubbleSort(int[] A) {
	for (int i = 0; i < A.length; i++) {
		for(int j = A.length - 1; j >= i; j--) {
			if (A[j] < A[j - 1]) {
				swithch(A[j], A[j - 1]);
			}
		}
	}	
}

```

选择：
```java
void selectSort(int[] A) {
	for (int i = 0; i < A.length; i++) {
		for (int j = i; j < A.length; j++) {
			if (A[j] < A[i]) {
				swithch(A[j], A[i]);
			}
		}
	}
}

```

插入：
```java
void insertSort(int[] A) {
	for (int i = 1; i < A.length; i++) {
		int key = A[i];
		j = i - 1;
		while (j >= 0 && A[j] > key) {
			A[j + 1] = A[j];
			j--;
		}
		A[j + 1] = key;
	}
}
// 折半插入法，用二分来找最后一个插入点。

```

---
### Problems 

- Binary Tree
- [x] [Binary Tree Preorder Traversal (recursion/ divide & conquer/ no recursion)](https://www.lintcode.com/problem/binary-tree-preorder-traversal/description)
- [ ] :carrot: inorder by loop
- [x] :carrot: postorder by loop
- [ ] :carrot: Morris inorder
- [x] [Binary Tree Inorder/Preorder/Postorder Traversal (while loop)](https://www.lintcode.com/problem/binary-tree-inorder-traversal/description)
- divide & conquer （两种传值方式。这里主要是子节点传给父节点。而BST的第一题就用了父节点的传给子节点）
- [x]  [Maximum Depth of Binary Tree](https://lintcode.com/problem/maximum-depth-of-binary-tree/)
- [ ]  [Balanced Binary Tree](https://www.lintcode.com/problem/balanced-binary-tree/)
- [x] [*Binary Tree Maximum Path Sum](https://www.lintcode.com/problem/binary-tree-maximum-path-sum/description) (对非法情况，求最大返回最小，求最小返回最大，求方案数返回0)
- [x] [*Lowest Common Ancestor (包含parent指针 用List，或者不包含 用分治)](https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-tree/description/)

- Sort
- [x] [Partition Array](https://www.lintcode.com/problem/partition-array/description)

- BFS
- [x] [Binary Tree Level Order Traversal](http://www.lintcode.com/problem/binary-tree-level-order-traversal/)
- Binary Search Tree
- [x] [Validate Binary Search Tree](http://www.lintcode.com/problem/validate-binary-search-tree/) 这用前序遍历的思路，把父节点的参数传给子节点。然后再把子节点的结果来分治。写起来更简洁。可以当作另一种思路的模板。
- [x] :carrot: 还有一个性质是，后序遍历时得到最小值排序。 

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        // write your code here
        return divConq(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    private boolean divConq(TreeNode root, long min, long max){
        if (root == null){
            return true;
        }
        if (root.val <= min || root.val >= max){
            return false;
        }
        return divConq(root.left, min, Math.min(max, root.val)) && 
                divConq(root.right, Math.max(min, root.val), max);
    }
}
```
- [x] [Insert Node in a Binary Search Tree](https://www.lintcode.com/problem/insert-node-in-a-binary-search-tree/description) 单独写函数的方法失败了。因为TreeNode没有提供改变自身的赋值。分治法的传值方式，可以把底层的结果慢慢传到最上层。用 root.left = // root.right = // return root. 也是分治法。但是和模板的后序遍历分治法不一样。
- [x] [Search Range in a Binary Search Tree](http://www.lintcode.com/problem/search-range-in-binary-search-tree/)
- [x] :memo: [*Remove Node in Binary Search Tree](http://www.lintcode.com/problem/remove-node-in-binary-search-tree/)第一道hard难度的题。和 Insert 一样，通过分治返回TreeNode的方式来改变BST的结构。  而且也是前序的思路完成的分治。
- [x] [*Binary Search Tree Iterator](https://www.lintcode.com/problem/binary-search-tree-iterator/description) 


---

## 二刷

- [x] [inorder-predecessor-in-bst](https://www.lintcode.com/problem/inorder-predecessor-in-bst/description)
一般的找前驱/后驱，用while+stack容易能看清楚访问的逻辑。
BST找，并且一定存在这个点，那么问题就转换成找最后一个比p.val小的点。可以直接递归搜索。
BST的前序搜索可以用while来模拟。因为每次只走一边，if以后的所搜某一边换成root = root.left/root.right 就可以了。


