## 二叉树遍历

### 144.前序遍历

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traversal(root,list);
        return list;
    }

    private void traversal(TreeNode node,List<Integer> list){
        if(node == null) return;
        list.add(node.val);
        traversal(node.left,list);
        traversal(node.right,list);
    }
}
```



### 145.后序遍历

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traversal(root,list);
        return list;
    }

    private void traversal(TreeNode node,List<Integer> list){
        if(node == null) return;
        traversal(node.left,list);
        traversal(node.right,list);
        list.add(node.val);
    }
}
```



### 94.中序遍历

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traversal(root,list);
        return list;
    }

    private void traversal(TreeNode node,List<Integer> list) {
        if(node == null) return;
        traversal(node.left,list);
        list.add(node.val);
        traversal(node.right,list);
    }
}
```



### 102.二叉树层序遍历

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if(root != null) queue.add(root);
        List<List<Integer>> result = new ArrayList<>();
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i = 0;i < size;i++){
                TreeNode node = queue.peek();
                queue.poll();
                list.add(node.val);
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            result.add(list);
        }  
        return result;
    }
}
```



### 107.二叉树层序遍历 Ⅱ

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if(root != null) queue.add(root);
        LinkedList<List<Integer>> result = new LinkedList<>();
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i = 0;i < size;i++) {
                TreeNode node = queue.peek();
                queue.poll();
                list.add(node.val);
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right); 
            }
            result.addFirst(list);
        }
        return result;
    }
}
```



### 109. 有序链表转换二叉搜索树

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if(head == null) return null;
        else if(head.next == null) return new TreeNode(head.val);
        ListNode pre = head;
        ListNode p = pre.next;
        ListNode q = p.next;
        while(q != null && q.next != null){
            pre = pre.next;
            p = pre.next;
            q = q.next.next;
        }
        pre.next = null;
        TreeNode root = new TreeNode(p.val);
        root.left = sortedListToBST(head);
        root.right = sortedListToBST(p.next);
        return root;
    }
}
```

### 637. 二叉树的层平均值

```java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if(root != null) queue.add(root);
        List<Double> result = new ArrayList<>();
        while(!queue.isEmpty()){
            int size = queue.size();
            double sum = 0;
            for(int i = 0;i < size;i++){
                TreeNode node = queue.peek();
                queue.poll();
                sum += node.val;
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            result.add(sum / size);
        }
        return result;
    }
}
```


### 429. N 叉树的层序遍历

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        Queue<Node> queue = new LinkedList<Node>();
        if(root != null) queue.add(root);
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i = 0;i < size;i++){
                Node node = queue.peek();
                queue.poll();
                list.add(node.val);
                for(Node n : node.children){
                    queue.offer(n);
                }
            }
            result.add(list);
        }
        return result;
    }
}
```



### 226.翻转二叉树

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return null;
        TreeNode rtree = root.right;
        root.right = invertTree(root.left);
        root.left = invertTree(rtree);
        return root;
    }
}
```



### 101.对称二叉树

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return compare(root.left,root.right);
    }

    public boolean compare(TreeNode left,TreeNode right) {
        if (left == null && right != null) return false;
        else if (left != null && right == null) return false;
        else if (left == null && right == null) return true;
        else if (left.val != right.val) return false;
        else return compare(left.left,right.right) && compare(left.right,right.left);
    }
}
```



### 104.二叉树的最大深度

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return 1 + Math.max(maxDepth(root.left),maxDepth(root.right));
    }
}
```



### 559.N叉树的最大深度

```java
class Solution {
    public int maxDepth(Node root) {
        if(root == null) return 0;
        int depth = 0;
        for(int i = 0; i < root.children.size();i++) {
            depth = Math.max(depth,maxDepth(root.children.get(i)));
        }
        return depth + 1;
    }
}
```



### 111.二叉树的最小深度

```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        if(root.left == null && root.right != null){
            return 1 + minDepth(root.right);
        }
        if(root.left != null && root.right == null){
            return 1 + minDepth(root.left);
        }
        return 1 + Math.min(minDepth(root.left),minDepth(root.right));
    }
}
```



### 110.平衡二叉树

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return getDepth(root) == -1 ? false : true;
    }

    public int getDepth(TreeNode node){
        if(node == null) return 0;
        int leftDepth = getDepth(node.left);
        if(leftDepth == -1) return -1;
        int rightDepth = getDepth(node.right);
        if(rightDepth == -1) return -1;
        return Math.abs(leftDepth - rightDepth) > 1 ? -1 : 1 + Math.max(leftDepth,rightDepth);
    }
}
```



### 257.二叉树的所有路径

```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        String path = "";
        if(root == null) return result;
        traversal(root,path,result);
        return result;
    }

    public void traversal(TreeNode cur,String path,List<String> result){
        path += cur.val;
        if(cur.left == null && cur.right == null){
            result.add(path);
            return;
        }
        if(cur.left != null) traversal(cur.left,path + "->",result);
        if(cur.right != null) traversal(cur.right,path + "->",result);
    }
}
```



### 100.相同的树

```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        String path = "";
        if(root == null) return result;
        traversal(root,path,result);
        return result;
    }

    public void traversal(TreeNode cur,String path,List<String> result){
        path += cur.val;
        if(cur.left == null && cur.right == null){
            result.add(path);
            return;
        }
        if(cur.left != null) traversal(cur.left,path + "->",result);
        if(cur.right != null) traversal(cur.right,path + "->",result);
    }
}
```



### 572.另一颗树的子树

```java
class Solution {
     public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null) return false;
        return subFrom(s, t) || isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    
    public boolean subFrom(TreeNode s, TreeNode t){
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        if (s.val != t.val) return false;
        return subFrom(s.left, t.left) && subFrom(s.right, t.right);
    }
}
```



### 404.左叶子之和

```java
class Solution {
     public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null) return false;
        return subFrom(s, t) || isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    
    public boolean subFrom(TreeNode s, TreeNode t){
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        if (s.val != t.val) return false;
        return subFrom(s.left, t.left) && subFrom(s.right, t.right);
    }
}
```



### 513.找树左下角的值

```java
class Solution {
    int maxLen;
    int maxleftValue;

    public void traversal(TreeNode root,int leftLen){
        if(root.left == null && root.right == null){
            if(leftLen > maxLen){
                maxLen = leftLen;
                maxleftValue = root.val;
            }
            return;
        }
        if(root.left != null){
            traversal(root.left,leftLen + 1);
        }
        if(root.right != null){
            traversal(root.right,leftLen + 1);
        }
        return;
    }

    public int findBottomLeftValue(TreeNode root) {
        if(root.left == null && root.right == null) return root.val;
        traversal(root,0);
        return maxleftValue;
    }
}
```



### 112.路径总和

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null) return false;
        if(root.left == null && root.right == null && targetSum == root.val){
            return true;
        }
        return hasPathSum(root.left,targetSum - root.val) || hasPathSum(root.right,targetSum - root.val);
    }
}
```



### 113.路径总和Ⅱ

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if(root == null) return new ArrayList<>();
        List<List<Integer>> ans = new ArrayList<>();
        if(root.val == targetSum && root.left == null && root.right == null) {
            List<Integer> arr = new ArrayList<>();
            arr.add(root.val);
            ans.add(arr);
            return ans;
        }
        List<List<Integer>> left = pathSum(root.left,targetSum - root.val);
        List<List<Integer>> right = pathSum(root.right,targetSum - root.val);
        for(List<Integer> list : left){
            list.add(0,root.val);
            ans.add(list);
        }
        for(List<Integer> list : right){
            list.add(0,root.val);
            ans.add(list);
        }
        return ans;
    }
}
```


### 106. 从中序与后序遍历序列构造二叉树

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return build(inorder,postorder,0,inorder.length - 1,postorder.length - 1);
    }

    public TreeNode build(int[] inorder,int[] postorder,int left,int right,int root){
        if(left > right) return null;
        TreeNode node = new TreeNode(postorder[root]);
        int index = 0;
        for(int i = left;i <= right;i++){
            if(inorder[i] == postorder[root]){
                index = i;
                break;
            }
        }
        node.left = build(inorder,postorder,left,index - 1,root - 1 - (right - index));
        node.right = build(inorder,postorder,index + 1,right,root - 1);
        return node;
    }
}
```



### 105. 从前序与中序遍历序列构造二叉树

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length == 0 || inorder.length == 0){
            return null;
        }
        TreeNode root = new TreeNode(preorder[0]);
        for(int i = 0;i < preorder.length;i++){
            if(preorder[0] == inorder[i]){
                root.left = buildTree(Arrays.copyOfRange(preorder,1,i + 1),Arrays.copyOfRange(inorder,0,i));
                root.right = buildTree(Arrays.copyOfRange(preorder,i + 1,preorder.length),Arrays.copyOfRange(inorder,i + 1,inorder.length));
                break;
            }
        }
        return root;
    }
}
```



### 654.最大二叉树

```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return traversal(nums,0,nums.length);
    }

    public TreeNode traversal(int[] nums,int left,int right){
        if(left >= right) return null;

        int maxValueIndex = left;
        for(int i = left + 1;i < right;++i){
            if(nums[i] > nums[maxValueIndex]) maxValueIndex = i;
        }

        TreeNode root = new TreeNode(nums[maxValueIndex]);

        root.left = traversal(nums,left,maxValueIndex);
        root.right = traversal(nums,maxValueIndex + 1,right);

        return root;
    }
}
```



### 617.合并二叉树

```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        root1.val += root2.val;
        root1.left = mergeTrees(root1.left,root2.left);
        root1.right = mergeTrees(root1.right,root2.right);
        return root1;
    }
}
```



### 700.二叉搜索树中的搜索

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if(root == null || root.val == val) return root;
        if(root.val > val) return searchBST(root.left,val);
        if(root.val < val) return searchBST(root.right,val);
        return null;
    }
}
```



### 98.验证二叉搜索树

```java
class Solution {
    TreeNode pre = null;
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        boolean left = isValidBST(root.left);

        if(pre != null && pre.val >= root.val) return false;
        pre = root;

        boolean right = isValidBST(root.right);
        return left && right;
    }
}
```



### 530. 二叉搜索树的最小绝对差

```java
class Solution {
    int result = Integer.MAX_VALUE;
    TreeNode pre;

    public void traserval(TreeNode cur){
        if(cur == null) return;
        traserval(cur.left);
        if(pre != null){
            result = Math.min(result,Math.abs(cur.val - pre.val));
        }
        pre = cur;
        traserval(cur.right);
    }

    public int getMinimumDifference(TreeNode root) {
        traserval(root);
        return result;
    }

}
```



### 501. 二叉搜索树中的众数

```java
class Solution {
    int maxCount;
    int count;
    TreeNode pre = new TreeNode();
    List<Integer> result = new ArrayList<>();

    public int[] findMode(TreeNode root) {
        count = 0;
        maxCount = 0;
        TreeNode pre = null;
        serchBST(root);
        int[] res = new int[result.size()];
        for(int i = 0; i < result.size();i++){
            res[i] = result.get(i);
        }
        return res;
    }

    public void serchBST(TreeNode cur){
        if(cur == null) return;
        serchBST(cur.left);
        if(pre == null){
            count = 1;
        } else if (pre.val == cur.val) {
            count++;
        } else {
            count = 1;
        }
        pre = cur;

        if(count == maxCount){
            result.add(cur.val);
        }

        if(count > maxCount){
            maxCount = count;
            result.clear();
            result.add(cur.val);
        }
        serchBST(cur.right);
        return;
    }
}
```



### 236. 二叉树的最近公共祖先

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == q || root == p || root == null) return root;
        TreeNode left = lowestCommonAncestor(root.left,p,q);
        TreeNode right = lowestCommonAncestor(root.right,p,q);
        if(left != null && right != null) return root;
        if(left == null) return right;
        return left;
    }
}
```

### 235. 二叉搜索树的最近公共祖先

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val){
            return lowestCommonAncestor(root.left,p,q);
        } else if(root.val < p.val && root.val < q.val){
            return lowestCommonAncestor(root.right,p,q);
        } else return root;
    }
}
```




