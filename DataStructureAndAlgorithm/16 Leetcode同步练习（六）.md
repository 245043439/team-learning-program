
# Leetcodeͬ����ϰ������
## Ŀ¼
- ��Ŀ01����ͬ����
- ��Ŀ02���Գƶ�����
- ��Ŀ03����������������
- ��Ŀ04�� Pow(x, n)
- ��Ŀ05���Ӽ�
- ��Ŀ06�����ױ���
- ��Ŀ07���������������������
- ��Ŀ08����������ǰ�����
- ��Ŀ09�����������������
- ��Ŀ10���������ĺ������

---
## ��Ŀ01����ͬ����

> - ��ţ�100
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/same-tree/

������������������дһ�����������������Ƿ���ͬ��

����������ڽṹ����ͬ�����ҽڵ������ͬ��ֵ������Ϊ��������ͬ�ġ�

**ʾ�� 1**:

```
����:      1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

���: true
```

**ʾ�� 2**:

```
����:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

���: false
```

**ʾ�� 3**:
```
����:      1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

���: false
```

**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��160 ms, ������ C# �ύ�л����� 5.85% ���û�
- �ڴ����ģ�24 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
 
public class Solution
{
    public bool IsSameTree(TreeNode p, TreeNode q)
    {
        //�ݹ���ֹ����
        if (p == null && q == null)
            return true;

        if (p != null && q != null && p.val == q.val)
        {
            return IsSameTree(p.left, q.left)
                    && IsSameTree(p.right, q.right);
        }
        return false;
    }
}
```

---
## ��Ŀ02���Գƶ�����

> - ��ţ�101
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/symmetric-tree/

����һ����������������Ƿ��Ǿ���ԳƵġ�

���磬������ `[1,2,2,3,4,4,3]` �ǶԳƵġ�

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

����������� `[1,2,2,null,3,null,3]` ���Ǿ���ԳƵ�:

```
    1
   / \
  2   2
   \   \
   3    3
```

**�ο����룺**

**��һ�֣����õݹ�ķ���**

- ִ�н����ͨ��
- ִ����ʱ��132 ms, ������ C# �ύ�л����� 16.67% ���û�
- �ڴ����ģ�25.1 MB, ������ C# �ύ�л����� 5.17% ���û�


```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
 
//����ԳƵĵݹ麯��
public class Solution
{
    public bool IsSymmetric(TreeNode root)
    {
        return IsMirror(root, root);
    }
    private bool IsMirror(TreeNode t1, TreeNode t2)
    {
        if (t1 == null && t2 == null) return true;
        if (t1 == null || t2 == null) return false;
        return (t1.val == t2.val)
            && IsMirror(t1.left, t2.right)
            && IsMirror(t1.right, t2.left);
    }
}
```

**�ڶ��֣����ö��еķ���**

**˼·**�����ö������Ĳ�α����ķ�ʽ��ʵ�֡�

- ִ�н����ͨ��
- ִ����ʱ��112 ms, ������ C# �ύ�л����� 70.93% ���û�
- �ڴ����ģ�24.9 MB, ������ C# �ύ�л����� 5.17% ���û�

```c
public class Solution
{
    public bool IsSymmetric(TreeNode root)
    {
        if (root == null)
            return true;

        Queue<TreeNode> nodes = new Queue<TreeNode>();
        nodes.Enqueue(root.left);
        nodes.Enqueue(root.right);
        while (nodes.Count != 0)
        {
            TreeNode node1 = nodes.Dequeue();
            TreeNode node2 = nodes.Dequeue();

            if (node1 == null && node2 == null)
                continue;
            if (node1 == null || node2 == null)
                return false;
            if (node1.val != node2.val)
                return false;
            nodes.Enqueue(node1.left);
            nodes.Enqueue(node2.right);
            nodes.Enqueue(node1.right);
            nodes.Enqueue(node2.left);
        }
        return true;
    }
}
```

---
## ��Ŀ03����������������

> - ��ţ�104
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/


����һ�����������ҳ��������ȡ�

�����������Ϊ���ڵ㵽��ԶҶ�ӽڵ���·���ϵĽڵ�����

˵��: Ҷ�ӽڵ���ָû���ӽڵ�Ľڵ㡣

**ʾ��**��

���������� [3,9,20,null,null,15,7]

```c
    3
   / \
  9  20
    /  \
   15   7
```

�������������� 3 ��

**�ο����룺**

**��һ�֣����ö���ʵ�ֲ�α�����˼·**

- ִ�н����ͨ��
- ִ����ʱ��108 ms, ������ C# �ύ�л����� 88.13% ���û�
- �ڴ����ģ�25.5 MB, ������ C# �ύ�л����� 5.97% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public int MaxDepth(TreeNode root)
    {
        if (root == null)
            return 0;

        Queue<TreeNode> q = new Queue<TreeNode>();
        int deep = 0;
        q.Enqueue(root);

        while (q.Count != 0)
        {
            deep++;
            int count = 0;
            int size = q.Count;

            while (count < size)
            {
                TreeNode node = q.Dequeue();
                count++;

                if (node.left != null)
                    q.Enqueue(node.left);
                if (node.right != null)
                    q.Enqueue(node.right);
            }
        }
        return deep;
    }
}
```



**�ڶ��֣����õݹ�**

**˼·**���ݹ�ֱ������������������ȣ����ӵ�ԭ�в����ϣ���󷵻������е����ֵ��

- ִ�н����ͨ��
- ִ����ʱ��132 ms, ������ C# �ύ�л����� 16.62% ���û�
- �ڴ����ģ�25.5 MB, ������ C# �ύ�л����� 6.06% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public int MaxDepth(TreeNode root)
    {
        if (root == null)
            return 0;
        int llen = 1;
        int rlen = 1;
        if (root.left != null)
        {
            llen += MaxDepth(root.left);
        }
        if (root.right != null)
        {
            rlen += MaxDepth(root.right);
        }
        return llen > rlen ? llen : rlen;
    }
}
```
---
## ��Ŀ04�� Pow(x, n)

> - ��ţ�50
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/powx-n/


ʵ�� `pow(x, n)` �������� x �� n ���ݺ�����

**ʾ�� 1:**

```c
����: 2.00000, 10
���: 1024.00000
```

**ʾ�� 2:**
```c
����: 2.10000, 3
���: 9.26100
```

**ʾ�� 3:**
```c
����: 2.00000, -2
���: 0.25000
����: 2-2 = 1/22 = 1/4 = 0.25
```

**ʾ�� 4:**
```c
����: 1.00000, -2147483648
���: 1.00000
```

**˵��:**

- -100.0 < x < 100.0
- n �� 32 λ�з�������������ֵ��Χ�� [?2^31, 2^31 ? 1] ��


**˼·**�����ÿ����ݷ���

��������Ҫ��`a^b`����ô`b`���Բ�ɶ����Ʊ�ʾ�����統`b = 5`ʱ��5�Ķ�������0101��`5 = 2^3��0 + 2^2��1 + 2^1��0 + 2^0��1`����ˣ����ǽ�`a^5`ת��Ϊ�� `a^(2^3��0 + 2^2��1 + 2^1��0 + 2^0��1)`����`a^(2^0) �� a^(2^2)`��


![](https://img-blog.csdnimg.cn/20200419235913493.png)

�������������2���ݣ�Ȼ�����������x��2���ݴη����ٰ�n��ɶ����ƣ��Ѷ����Ƶ��ж�Ӧλ����1��ֵ���������͵õ��˽�������׷�����Ϊ **�����ݷ�**��


**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��56 ms, ������ C# �ύ�л����� 51.87% ���û�
- �ڴ����ģ�15.1 MB, ������ C# �ύ�л����� 50.00% ���û�

```c
public class Solution
{
    public double MyPow(double x, int n)
    {
        int neg = n < 0 ? -1 : 1;
        long g = Math.Abs((long)n);

        double[] d = new double[32];
        d[0] = x;
        for (int i = 1; i < 32; i++)
        {
            d[i] = d[i - 1] * d[i - 1];
        }

        double result = 1.0d;
        for (int i = 0; i < 32; i++)
        {
            int mask = 1 << i;
            if ((mask & g) != 0)
            {
                result *= d[i];
            }
        }
        return neg != -1 ? result : 1.0 / result;
    }
}
```
---
## ��Ŀ05���Ӽ�

> - ��ţ�78
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/subsets/


����һ��**�����ظ�Ԫ��**���������� nums�����ظ��������п��ܵ��Ӽ����ݼ�����

<b>˵��</b>���⼯���ܰ����ظ����Ӽ���

<b>ʾ��</b>:
```c
����: nums = [1,2,3]
���:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**�ο�����**��

**��һ�֣����ݷ�**

������nums[i]Ϊ��ʼ������������Һ���������ֵ��Ҫ����ǰһ����ֵ������������ظ�������

![���ݹ���](https://img-blog.csdnimg.cn/20190913152245222.png)

- ״̬��ͨ��
- ����ʱ: 356 ms, ������ C# �ύ�л����� 92.31% ���û�
- �ڴ�����: 29.2 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
public class Solution
{
    private IList<IList<int>> _result;
    
    public IList<IList<int>> Subsets(int[] nums)
    {
        _result = new List<IList<int>>();
        int len = nums.Length;

        if (len == 0)
        {
            return _result;
        }
        IList<int> item = new List<int>();
        Find(nums, 0, item);
        return _result;
    }

    private void Find(int[] nums, int begin, IList<int> item)
    {
        // ע�⣺����Ҫ new һ��
        _result.Add(new List<int>(item)); 

        if (begin == nums.Length)
            return;

        for (int i = begin; i < nums.Length; i++)
        {
            item.Add(nums[i]);
            Find(nums, i + 1, item);

            // ������⣬״̬�ڵݹ���ɺ�Ҫ����
            item.RemoveAt(item.Count - 1); 
        }
    }
}
```

**�ڶ��֣��Ӽ���չ��**

- ״̬��ͨ��
- ִ����ʱ: 352 ms, ������ C# �ύ�л����� 94.51% ���û�
- �ڴ�����: 29.2 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
public class Solution
{
    public IList<IList<int>> Subsets(int[] nums)
    {
        IList<IList<int>> result = new List<IList<int>>();
        IList<int> item = new List<int>();
        result.Add(item);
        for (int i = 0; i < nums.Length; i++)
        {
            for (int j = 0, len = result.Count; j < len; j++)
            {
                item = new List<int>(result[j]);
                item.Add(nums[i]);
                result.Add(item);
            }
        }
        return result;
    }
}
```

**�����֣�λ����**

**˼·��** �����������ϵ�˼·��

��`{1,2,3}`Ϊ��������������`2^3`���Ӽ���

```c
000 -> []
100 -> [1]
101 -> [1,3]
110 -> [1,2]
111 -> [1,2,3]
...
```

- ״̬��ͨ��
- ִ����ʱ: 348 ms, ������ C# �ύ�л����� 97.80% ���û�
- �ڴ�����: 29.5 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
public class Solution
{
    public IList<IList<int>> Subsets(int[] nums)
    {
        IList<IList<int>> result = new List<IList<int>>();
        int count = nums.Length;

        for (int i = 0; i < 1 << count; i++)
        {
            IList<int> item = new List<int>();
            for (int j = 0; j < count; j++)
            {
                int mask = 1 << j;
                if ((mask & i) != 0)
                    item.Add(nums[j]);
            }
            result.Add(item);
        }
        return result;
    }
}
```

---
## ��Ŀ06�����ױ���

> - ��ţ�89
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/gray-code/

���ױ�����һ������������ϵͳ���ڸ�ϵͳ�У�������������ֵ����һ��λ���Ĳ��졣

����һ�����������λ���ķǸ����� n����ӡ����ױ������С����ױ������б����� 0 ��ͷ��

<b>ʾ�� 1</b>:
```c
����: 2
���: [0,1,3,2]
����:
00 - 0
01 - 1
11 - 3
10 - 2

���ڸ����� n������ױ������в���Ψһ��
���磬[0,2,3,1] Ҳ��һ����Ч�ĸ��ױ������С�

00 - 0
10 - 2
11 - 3
01 - 1
```

<b>ʾ�� 2</b>:
```c
����: 0
���: [0]
����: ���Ƕ�����ױ������б����� 0 ��ͷ��
    ����������λ��Ϊ n �ĸ��ױ������У��䳤��Ϊ 2^n��
    �� n = 0 ʱ������Ϊ 2^0 = 1��
    ��ˣ��� n = 0 ʱ������ױ�������Ϊ [0]��
```

**˼·**��


![�׸���](https://img-blog.csdnimg.cn/20190915115931873.png)

�� n λ�Ƶ� n+1 λ���ʱ��n+1 λ������� n λ�����ͬʱ���� n λ������ڸ�λ������һ��λ 1 ���γɵ���һ������������һ������Ҫ��ǰһ�����������С�

**�ο�����**��

- ״̬��ͨ��
- 12 / 12 ��ͨ����������
- ִ����ʱ: 296 ms, ������ C# �ύ�л����� 95.83% ���û�
- �ڴ�����: 24.8 MB, ������ C# �ύ�л����� 16.67% ���û�

```c
public class Solution
{
    public IList<int> GrayCode(int n)
    {
        IList<int> lst = new List<int>();
        lst.Add(0);
        for (int i = 1; i <= n; i++)
        {
            for (int j = lst.Count - 1; j >= 0; j--)
            {
                int item = lst[j] + (1 << i - 1);
                lst.Add(item);
            }
        }
        return lst;
    }
}
```


---
## ��Ŀ07���������������������



> - ��ţ�236
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/

����һ��������, �ҵ�����������ָ���ڵ������������ȡ�

�ٶȰٿ�������������ȵĶ���Ϊ���������и��� T ��������� p��q������������ȱ�ʾΪһ����� x������ x �� p��q �������� x ����Ⱦ����ܴ�<b>һ���ڵ�Ҳ���������Լ�������</b>������

���磬�������¶�����: root = [3,5,1,6,2,0,8,null,null,7,4]

![](https://img-blog.csdnimg.cn/20190922095031349.png)

<b>ʾ�� 1</b>:
```c
����: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
���: 3
����: �ڵ� 5 �ͽڵ� 1 ��������������ǽڵ� 3��
```

<b>ʾ�� 2</b>:
```c
����: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
���: 5
����: �ڵ� 5 �ͽڵ� 4 ��������������ǽڵ� 5����Ϊ���ݶ�������������Ƚڵ����Ϊ�ڵ㱾��
```

<b>˵��</b>:

- ���нڵ��ֵ����Ψһ�ġ�
- p��q Ϊ��ͬ�ڵ��Ҿ������ڸ����Ķ������С�


**�ο�����**��

**˼·**�����õݹ�

- ״̬��ͨ��
- ִ����ʱ: 132 ms, ������ C# �ύ�л����� 96.10% ���û�
- �ڴ�����: 27.5 MB, ������ C# �ύ�л����� 20.00% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
 
public class Solution
{
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q)
    {
        return Find(root, p, q);
    }

    private TreeNode Find(TreeNode current, TreeNode p, TreeNode q)
    {
        if (current == null || current == p || current == q)
            return current;
        TreeNode left = Find(current.left, p, q);
        TreeNode right = Find(current.right, p, q);
        if (left != null && right != null)
            return current;
        return left != null ? left : right;
    }
}
```



---
## ��Ŀ08����������ǰ�����

> - ��ţ�144
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/binary-tree-preorder-traversal/


����һ������������������ ǰ�������

**ʾ��:**


```c
����: [1,null,2,3]  
   1
    \
     2
    /
   3 

���: [1,2,3]
```


����: �ݹ��㷨�ܼ򵥣������ͨ�������㷨�����


**�ο�����**��

**��һ�֣�����ջ**

- ִ�н����ͨ��
- ִ����ʱ��276 ms, ������ C# �ύ�л����� 84.15% ���û�
- �ڴ����ģ�29.9 MB, ������ C# �ύ�л����� 5.00% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> PreorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while (stack.Count != 0 || root != null)
        {
            if (root != null)
            {
                stack.Push(root);
                lst.Insert(lst.Count, root.val);
                root = root.left;
            }
            else
            {
                TreeNode node = stack.Pop();
                root = node.right;
            }
        }
        return lst;
    }
}
```

**�ڶ��֣����õݹ�**

- ִ�н����ͨ��
- ִ����ʱ��280 ms, ������ C# �ύ�л����� 79.27% ���û�
- �ڴ����ģ�29.8 MB, ������ C# �ύ�л����� 5.00% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> PreorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        PreOrder(root, lst);
        return lst;
    }
    private void PreOrder(TreeNode node, IList<int> lst)
    {
        if (node == null)
            return;

        lst.Add(node.val);
        PreOrder(node.left, lst);
        PreOrder(node.right, lst);
    }
}
```


---
## ��Ŀ09�����������������

> - ��ţ�94
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/binary-tree-inorder-traversal/

����һ���������������������� ������

**ʾ��:**

```c
����: [1,null,2,3]
   1
    \
     2
    /
   3

���: [1,3,2]
```

����: �ݹ��㷨�ܼ򵥣������ͨ�������㷨�����


**�ο����룺**

**��һ�֣�����ջ**

- ִ�н����ͨ��
- ִ����ʱ��284 ms, ������ C# �ύ�л����� 53.59% ���û�
- �ڴ����ģ�30 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> InorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while (stack.Count != 0 || root != null)
        {
            if (root != null)
            {
                stack.Push(root);
                root = root.left;
            }
            else
            {
                TreeNode node = stack.Pop();
                lst.Add(node.val);
                root = node.right;
            }
        }
        return lst;
    }
}
```



**�ڶ��֣�ʹ�õݹ�**

- ִ�н����ͨ��
- ִ����ʱ��264 ms, ������ C# �ύ�л����� 99.16% ���û�
- �ڴ����ģ�29.8 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> InorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        MidOrder(root, lst);
        return lst;
    }
    private void MidOrder(TreeNode node, IList<int> lst)
    {
        if (node == null)
            return;
        MidOrder(node.left, lst);
        lst.Add(node.val);
        MidOrder(node.right, lst);
    }
}
```



---
## ��Ŀ10���������ĺ������

> - ��ţ�145
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/binary-tree-postorder-traversal/


����һ������������������ ���� ������

**ʾ��:**


```c
����: [1,null,2,3]  
   1
    \
     2
    /
   3 

���: [3,2,1]
```


����: �ݹ��㷨�ܼ򵥣������ͨ�������㷨�����


**�ο�����**��


**��һ�֣�����ջ**

ǰ�����˳��Ϊ���� -> �� -> ��

�������˳��Ϊ���� -> �� -> ��

���1�����ǽ�ǰ������нڵ����������β�����߼����޸�Ϊ���ڵ�����������ͷ��

��ô�������ͱ�Ϊ�ˣ��� -> �� -> ��

���2�����ǽ�������˳���ɴ������޸�Ϊ���ҵ���������1

��ô�������ͱ�Ϊ�ˣ��� -> �� -> ��

��պ��Ǻ��������˳��

����������˼·�����Ǵ���ʽ���£�

��һ���޸�ǰ����������У��ڵ�д��������Ĵ��룬�������β�޸�Ϊ�������

�ڶ����޸�ǰ����������У�ÿ���Ȳ鿴��ڵ��ٲ鿴�ҽڵ���߼�����Ϊ�Ȳ鿴�ҽڵ��ٲ鿴��ڵ�

- ִ�н����ͨ��
- ִ����ʱ��272 ms, ������ C# �ύ�л����� 98.15% ���û�
- �ڴ����ģ�30 MB, ������ C# �ύ�л����� 6.90% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> PostorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while (stack.Count != 0 || root != null)
        {
            if (root != null)
            {
                stack.Push(root);
                lst.Insert(0, root.val);
                root = root.right;
            }
            else
            {
                TreeNode node = stack.Pop();
                root = node.left;
            }
        }
        return lst;
    }
}
```

**�ڶ��֣����õݹ�**

- ִ�н����ͨ��
- ִ����ʱ��276 ms, ������ C# �ύ�л����� 89.81% ���û�
- �ڴ����ģ�30 MB, ������ C# �ύ�л����� 6.90% ���û�

```c
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public IList<int> PostorderTraversal(TreeNode root)
    {
        IList<int> lst = new List<int>();
        PostOrder(root, lst);
        return lst;
    }
    private void PostOrder(TreeNode node, IList<int> lst)
    {
        if (node == null)
            return;
            
        PostOrder(node.left, lst);
        PostOrder(node.right, lst);
        lst.Add(node.val);
    }
}
```


