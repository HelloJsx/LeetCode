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


