# Tree Traversals

#### Example Problems
- [Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)
- [Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
- [Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)
- [Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

The most common way of going about traversing (pre, in, or post) a binary search tree is using DFS. We can go about this iteratively using a stack (remember, stack for DFS, Queue for BFS).

### Preorder Traversal (DFS)

*Root -> Left -> Right*

Preorder traversal lends itself to an iterative stack-based DFS solution. The idea is to push our root to the stack, and while this is not null, add it's value to our result array, then push the right and left children, respectively. Take a look at the solution below:

```JavaScript
function preorderTraversal(root) {
    let result = [];
    let stack = [];

    stack.push(root);

    while (stack.length > 0) {
        const currentNode = stack.pop();

        if (currentNode !== null) {
            result.push(currentNode.val);
            
            // Remember: we push the right in first due to LIFO property
            stack.push(currentNode.right);
            stack.push(currentNode.left);
        }
    }

    return result;
}
```

### Inorder Traversal (DFS)

*Left -> Root -> Right*

In order (ha) to accomplish this, we need to go as far as we can left as possible for each node in our tree. When we can't go left any further, we pop the latest node from the stack, push it to some result array, and set our current node to the current nodes right. Take a look at the solution below:

```JavaScript
function inorderTraversal(root) {
    let result = [];
    let stack = [];
    let runner = root;

    while (runner !== null || stack.length > 0) {
        while (runner !== null) {
            stack.push(runner);
            runner = runner.left;
        }

        runner = stack.pop();
        result.push(runner.val);
        runner = runner.right;
    }
    return result;
}
```

### Postorder Traversal (DFS)

Postorder traversal is a little bit less intuitive at first than the other traversals. The general idea is that we will push our root to the stack, *enqueue* the root (remember, order is essentially reversed) and set root to be root.right. Once null is reached, we will pop from the stack and set root (a runner) to the poppedNode.left. This will allow us to appropriately fill in the left nodes in out left -> right -> root queue. Take a look at the JS solution below:

```JavaScript
function postOrderTraversal(root) {
    let result = [];
    let stack = [];
    let runner = root;

    while (stack.length > 0 || runner !== null) {
        if (runner !== null) {
            stack.push(runner);
            result.unshift(runner.val);
            runner = runner.right;
        } else {
            const node = stack.pop();
            runner = node.left;
        }
    }

    return result;
}
```

### Level Order Traversal (BFS)

Level-Order traversal is a bit different, in that we will take a BFS approach to solving the problem (using a Queue). To go about this algorithm, we first enqueue our root, similar to the other traversals, and while our queue has elements, we loop through each element of the queue, enqueuing their left and right child (if available). On each iteration, we dequeue and add the current node we're on to the sublist that we're making along the way (which will be added to our solution list). Take a look at the Java solution below:

```Java
public List<List<Integer>> levelOrder(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    List<List<Integer>> wrapList = new LinkedList<List<Integer>>();
    
    if (root == null) return wrapList;
    
    queue.offer(root);
    while (!queue.isEmpty()){
        int levelNum = queue.size();
        List<Integer> subList = new LinkedList<Integer>();

        for (int i = 0; i < levelNum; i++) {
            if(queue.peek().left != null) queue.offer(queue.peek().left);
            if(queue.peek().right != null) queue.offer(queue.peek().right);
            subList.add(queue.poll().val);
        }

        wrapList.add(subList);
    }
    return wrapList;
}
```