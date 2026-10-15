
在示例中，我们创建了一种名为二叉搜索树的特殊二叉树。二叉搜索树（无值）具有特性：任何左子树中的值小于其父节点的值，而任何右子树中的值大于其父节点的值。图 17.16 描述了一个包含 12 个整数值的二叉搜索树。注意，对应一组数据的二叉搜索树的形状取决于值插入树的顺序。

图 17.17 和图 17.18 的应用创建了一个整数二叉搜索树，并使用递归的中序、前序和后序遍历对其遍历（即遍历其所有节点）。程序生成 10 个随机数并将每个插入树中。类 `Tree` 定义在包 `com.deitel.jhtp7.ch17` 中以便复用。

![](img/1df0d1e8ac600795647eb8ea38390af_864_0.png)

图 17.15 | 二叉树的图形化表示。

![](img/1df0d1e8ac600795647eb8ea38390af_864_1.png)

图 17.16 | 包含 12 个值的二叉搜索树。

# 第17章 数据结构

```java
// 图 17.17: Tree.java
// TreeNode 类和 Tree类的定义
package com.deitel.jhtp7.ch17;
// TreeNode 类定义
class TreeNode
{
    // 包访问成员
    TreeNode leftNode; // 左节点
    int data; //节点值
    TreeNode rightNode; // 右节点

    // 构造函数初始化数据并使其成为叶节点
    public TreeNode(int data) {
        this.data = data;
        leftNode = rightNode = null; // 节点没有孩子
    } // TreeNode 构造函数

// Tree 类定义
public class Tree
{
    private root;

    // 构造函数初始化一个空 Tree
    public Tree() {
        root = null;
    } // 结束参数构造函数

    // 在二叉搜索树中插入新节点
    public void insert(int insertValue) {
        if (root == null) {
            root = new TreeNode(insertValue); // 创建根节点
        } else if (insertValue < root.data) { // 插入左子树
            if (root.leftNode == null) {
                root.leftNode = new TreeNode(insertValue);
            } else {
                root.leftNode.insert(insertValue); // 调用 insert 方法
            }
        } else if (insertValue > root.data) { // 插入右子树
            if (root.rightNode == null) {
                root.rightNode = new TreeNode(insertValue);
            } else {
                root.rightNode.insert(insertValue); // 调用 insert 方法
            }
        } else { // 忽略重复值
            System.out.println("Duplicate value ignored");
        }
    } // 结束 insert 方法

    // 开始前序遍历
    public void preorderTraversal() {
        preorderHelper(root);
    } // 结束 preorderTraversal 方法

    // 执行前序遍历的递归方法
    private void preorderHelper(TreeNode node) {
        if (node == null) {
            return;
        }
        System.out.printf("%d ", node.data); // 输出节点数据
        preorderHelper(node.leftNode); // 遍历左子树
        preorderHelper(node.rightNode); // 遍历右子树
    } // 结束 preorderHelper 方法

    // 开始中序遍历
    public void inorderTraversal() {
        inorderHelper(root);
    } // 结束 inorderTraversal 方法

    // 执行中序遍历的递归方法
    private void inorderHelper(TreeNode node) {
        if (node == null) {
            return;
        }
        inorderHelper(node.leftNode); // 遍历左子树
        System.out.printf("%d ", node.data); // 输出节点数据
        inorderHelper(node.rightNode); // 遍历右子树
    } // 结束 inorderHelper 方法

    // 开始后序遍历
    public void postorderTraversal() {
        postorderHelper(root);
    } // 结束 postorderTraversal 方法

    // 执行后序遍历的递归方法
    private void postorderHelper(TreeNode node) {
        if (node == null) {
            return;
        }
        postorderHelper(node.leftNode); // 遍历左子树
        postorderHelper(node.rightNode); // 遍历右子树
        System.out.printf("%d \n", node.data); // 输出节点数据
    } // 结束 postorderHelper 方法
}
```

图 17.17 | 二叉搜索树的 `TreeNode` 和 `Tree` 类声明。（2/3。）
