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



