# Leetcodeͬ����ϰ���壩
## Ŀ¼
- ��Ŀ01����ջʵ�ֶ���
- ��Ŀ02���������ľ���
- ��Ŀ03����������ת����
- ��Ŀ04�������ǰ׺
- ��Ŀ05����ת�ַ���
- ��Ŀ06�����ظ��ַ�����Ӵ�
- ��Ŀ07��������Ӵ�
- ��Ŀ08���ַ������
- ��Ŀ09��������ʽƥ��
- ��Ŀ10��ͨ���ƥ��


---
## ��Ŀ01����ջʵ�ֶ���

> - ��ţ�232
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/implement-queue-using-stacks/

ʹ��ջʵ�ֶ��е����в�����

- `push(x)` -- ��һ��Ԫ�ط�����е�β����
- `pop()` -- �Ӷ����ײ��Ƴ�Ԫ�ء�
- `peek()` -- ���ض����ײ���Ԫ�ء�
- `empty()` -- ���ض����Ƿ�Ϊ�ա�


ʾ��:

```c
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // ���� 1
queue.pop();   // ���� 1
queue.empty(); // ���� false
```

˵��:

- ��ֻ��ʹ�ñ�׼��ջ���� -- Ҳ����ֻ��push to top��peek/pop from top��size �� is empty �����ǺϷ��ġ�
- ����ʹ�õ�����Ҳ��֧��ջ�������ʹ��`list`����`deque`��˫�˶��У���ģ��һ��ջ��ֻҪ�Ǳ�׼��ջ�������ɡ�
- �������в���������Ч�ģ����磬һ���յĶ��в������`pop`����`peek`��������

**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��112 ms, ������ C# �ύ�л����� 95.10% ���û�
- �ڴ����ģ�24.3 MB, ������ C# �ύ�л����� 5.33% ���û�

```c
public class MyQueue
{
    private Stack<int> _stack = new Stack<int>();

    /** Initialize your data structure here. */
    public MyQueue()
    {
        ;
    }

    /** Push element x to the back of queue. */
    public void Push(int x)
    {
        if (_stack.Count == 0)
        {
            _stack.Push(x);
            return;
        }

        Stack<int> temp = new Stack<int>();
        while (_stack.Count != 0)
        {
            temp.Push(_stack.Pop());
        }
        _stack.Push(x);
        while (temp.Count != 0)
        {
            _stack.Push(temp.Pop());
        }
    }

    /** Removes the element from in front of queue and returns that element. */
    public int Pop()
    {
        return _stack.Count > 0 ? _stack.Pop() : -1;
    }

    /** Get the front element. */
    public int Peek()
    {
        return _stack.Count > 0 ? _stack.Peek() : -1;
    }

    /** Returns whether the queue is empty. */
    public bool Empty()
    {
        return _stack.Count == 0;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.Push(x);
 * int param_2 = obj.Pop();
 * int param_3 = obj.Peek();
 * bool param_4 = obj.Empty();
 */
```

---
## ��Ŀ02���������ľ���

> - ��ţ�766
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/toeplitz-matrix/


���������ÿһ�������ϵ����µĶԽ����ϵ�Ԫ�ض���ͬ����ô��������� �������ľ��� ��

����һ��`M x N`�ľ��󣬵��ҽ��������������ľ���ʱ����`True`��

**ʾ�� 1:**

```c
����: 
matrix = [
  [1,2,3,4],
  [5,1,2,3],
  [9,5,1,2]
]
���: True
����:
������������, ��Խ���Ϊ:
"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]"��
�����Խ����ϵ�����Ԫ�ؾ���ͬ, ��˴���True��
```

**ʾ�� 2:**

```c
����:
matrix = [
  [1,2],
  [2,2]
]
���: False
����: 
�Խ���"[1, 2]"�ϵ�Ԫ�ز�ͬ��
```

**˵��:**

1. `matrix`��һ�����������Ķ�ά���顣
2. `matrix`���������������� [1, 20]��Χ�ڡ�
3. `matrix[i][j]`������������ [0, 99]��Χ�ڡ�


**����:**

1. �������洢�ڴ����ϣ����Ҵ����ڴ������޵ģ����һ�����ֻ�ܽ�һ�о�����ص��ڴ��У�����ô�죿
2. �������̫��������ֻ��һ�ν������м��ص��ڴ��У�����ô�죿

**˼·**�����жԽ����ϵ�Ԫ�ض�����$a_{11} = a_{00}, a_{22} = a_{11}, a_{kk} = a_{k-1k-1}$���ڶԽ����ϵ�Ԫ����˵�������ǰԪ�ز��ǵ�һ�����ֵ�Ԫ�أ���ô��ǰ���Ԫ��һ���ڵ�ǰԪ�ص����Ͻǡ������Ƴ�������λ������$(r, c)$�ϵ�Ԫ�أ�ֻ��Ҫ���`r == 0 OR c == 0 OR matrix[r-1][c-1] == matrix[r][c]`�Ϳ����ˡ�

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��128 ms, ������ C# �ύ�л����� 47.50% ���û�
- �ڴ����ģ�27.5 MB, ������ C# �ύ�л����� 16.13% ���û�

```c
public class Solution
{
    public bool IsToeplitzMatrix(int[][] matrix)
    {
        for (int i = 1; i < matrix.Length; i++)
        {
            int[] row = matrix[i];
            for (int j = 1; j < row.Length; j++)
            {
                if (matrix[i][j] != matrix[i - 1][j - 1])
                    return false;
            }
        }
        return true;
    }
}
```


---
## ��Ŀ03����������ת����

> - ��ţ�13
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/roman-to-integer/

�������ְ������������ַ�: `I�� V�� X�� L��C��D`��`M`��

```
�ַ�          ��ֵ
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

���磬 �������� 2 д��`II`����Ϊ�������е� 1��12 д��`XII`����Ϊ`X + II`�� 27 д��`XXVII`, ��Ϊ`XX + V + II`��


ͨ������£�����������С�������ڴ�����ֵ��ұߡ���Ҳ�������������� 4 ��д��`IIII`������`IV`������ 1 ������ 5 ����ߣ�����ʾ�������ڴ��� 5 ��С�� 1 �õ�����ֵ 4 ��ͬ���أ����� 9 ��ʾΪ`IX`���������Ĺ���ֻ�������������������

```
I ���Է��� V (5) �� X (10) ����ߣ�����ʾ 4 �� 9��
X ���Է��� L (50) �� C (100) ����ߣ�����ʾ 40 �� 90��
C ���Է��� D (500) �� M (1000) ����ߣ�����ʾ 400 �� 900��
```

����һ���������֣�����ת��������������ȷ���� 1 �� 3999 �ķ�Χ�ڡ�

**ʾ�� 1:**

```c
����:"III"
���: 3
```

**ʾ�� 2:**

```c
����: "IV"
���: 4
```

**ʾ�� 3:**
```c
����: "IX"
���: 9
```

**ʾ�� 4:**
```c
����: "LVIII"
���: 58
����: L = 50, V= 5, III = 3.
```

**ʾ�� 5:**
```c
����: "MCMXCIV"
���: 1994
����: M = 1000, CM = 900, XC = 90, IV = 4.
```

**˼·**��ֱ�ӷ������ݡ�����������С�������ڴ�����ֵ��ұߡ��Լ�������������Ĺ���ֱ��ȥд���롣

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��96 ms, ������ C# �ύ�л����� 95.88% ���û�
- �ڴ����ģ�25.7 MB, ������ C# �ύ�л����� 5.27% ���û�

```c
public class Solution
{
    public int RomanToInt(string s)
    {
        int result = 0;
        int count = s.Length;
        int i = 0;
        while (i < count)
        {
            char c = s[i];
            int move = 0;
            switch (c)
            {
                case 'I':
                    result += PreI(i, s, ref move);
                    break;
                case 'V':
                    result += 5;
                    move = 1;
                    break;
                case 'X':
                    result += PreX(i, s, ref move);
                    break;
                case 'L':
                    result += 50;
                    move = 1;
                    break;
                case 'C':
                    result += PreC(i, s, ref move);
                    break;
                case 'D':
                    result += 500;
                    move = 1;
                    break;
                case 'M':
                    result += 1000;
                    move = 1;
                    break;
            }
            i += move;
        }
        return result;
    }
    private int PreI(int index, string s, ref int move)
    {
        //I  1
        //IV 4
        //IX 9
        //II 2
        int result = 0;
        int count = s.Length;
        if (index + 1 < count)
        {
            char c = s[index + 1];
            switch (c)
            {
                case 'V':
                    result = 4;
                    move = 2;
                    break;
                case 'X':
                    result = 9;
                    move = 2;
                    break;
                case 'I':
                    result = 2;
                    move = 2;
                    break;
            }
        }
        else
        {
            result = 1;
            move = 1;
        }
        return result;
    }

    private int PreX(int index, string s, ref int move)
    {
        //X 10
        //XL 40
        //XC 90
        int result = 0;
        int count = s.Length;
        if (index + 1 < count)
        {
            char c = s[index + 1];
            switch (c)
            {
                case 'L':
                    result = 40;
                    move = 2;
                    break;
                case 'C':
                    result = 90;
                    move = 2;
                    break;
                default:
                    result = 10;
                    move = 1;
                    break;
            }
        }
        else
        {
            result = 10;
            move = 1;
        }
        return result;
    }

    private int PreC(int index, string s, ref int move)
    {
        //C 100
        //CD 400
        //CM 900
        int result = 0;
        int count = s.Length;
        if (index + 1 < count)
        {
            char c = s[index + 1];
            switch (c)
            {
                case 'D':
                    result = 400;
                    move = 2;
                    break;
                case 'M':
                    result = 900;
                    move = 2;
                    break;
                default:
                    result = 100;
                    move = 1;
                    break;
            }
        }
        else
        {
            result = 100;
            move = 1;
        }
        return result;
    }
}
```

---
## ��Ŀ04�������ǰ׺

> - ��ţ�14
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/longest-common-prefix/

��дһ�������������ַ��������е������ǰ׺��

��������ڹ���ǰ׺�����ؿ��ַ��� ""��

<b>ʾ�� 1</b>:
```c
����: ["flower","flow","flight"]
���: "fl"
```

<b>ʾ�� 2</b>:
```c
����: ["dog","racecar","car"]
���: ""
����: ���벻���ڹ���ǰ׺��
```

<b>˵��</b>:

��������ֻ����Сд��ĸ a-z��


**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 144 ms, ������ C# �ύ�л����� 94.92% ���û�
- �ڴ�����: 23.4 MB, ������ C# �ύ�л����� 11.69% ���û�


```c
public class Solution {
    public string LongestCommonPrefix(string[] strs) 
    {
        if (strs.Length == 0)
            return string.Empty;

        string result = strs[0];
        for (int i = 1; i < strs.Length; i++)
        {
            result = Prefix(result, strs[i]);
            if (string.IsNullOrEmpty(result))
                break;
        }
        return result;        
    }
    
    public string Prefix(string str1, string str2)
    {
        int len1 = str1.Length;
        int len2 = str2.Length;
        int len = Math.Min(len1, len2);
        int i = 0;
        for (; i < len; i++)
        {
            if (str1[i] != str2[i])
                break;
        }
        return i == 0 ? string.Empty : str1.Substring(0, i);
    }    
}
```

---
## ��Ŀ05����ת�ַ���

> - ��ţ�344
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/reverse-string/



��дһ���������������ǽ�������ַ�����ת�����������ַ������ַ����� char[] ����ʽ������

��Ҫ�����������������Ŀռ䣬�����ԭ�� <b>�޸���������</b>��ʹ�� O(1) �Ķ���ռ�����һ���⡣

����Լ��������е������ַ����� ASCII ����еĿɴ�ӡ�ַ���


<b>ʾ�� 1</b>��
```c
���룺["h","e","l","l","o"]
�����["o","l","l","e","h"]
```

<b>ʾ�� 2</b>��
```c
���룺["H","a","n","n","a","h"]
�����["h","a","n","n","a","H"]
```



**�ο����룺**

- ״̬��ͨ��
- ִ����ʱ: 572 ms, ������ C# �ύ�л����� 94.94% ���û�
- �ڴ�����: 33.6 MB, ������ C# �ύ�л����� 5.05% ���û�

```c
public class Solution {
    public void ReverseString(char[] s) {
        int i = 0;
        int j = s.Length-1;
        while (i < j)
        {
            char c = s[i];
            s[i] = s[j];
            s[j] = c;
            i++;
            j--;
        }
    }
}
```

---
## ��Ŀ06�����ظ��ַ�����Ӵ�

> - ��ţ�3
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

����һ���ַ����������ҳ����в������ظ��ַ��� **��Ӵ�** �ĳ��ȡ�

**ʾ�� 1:**

```c
����: "abcabcbb"
���: 3 
����: ��Ϊ���ظ��ַ�����Ӵ��� "abc"�������䳤��Ϊ 3��
```

**ʾ�� 2:**

```c
����: "bbbbb"
���: 1
����: ��Ϊ���ظ��ַ�����Ӵ��� "b"�������䳤��Ϊ 1��
```

**ʾ�� 3:**
```c
����: "pwwkew"
���: 3
����: ��Ϊ���ظ��ַ�����Ӵ��� "wke"�������䳤��Ϊ 3��
     ��ע�⣬��Ĵ𰸱����� �Ӵ� �ĳ��ȣ�"pwke" ��һ�������У������Ӵ���
```

**˼·��**

������̬�滮��˼·����ǰ���������ÿ��λ��Ϊ��ֹλ�ã����������ظ��Ӵ��ĳ��ȣ�֮������Щ���ȵ����ֵ���ɡ�

��������λ��`index`������ظ��Ӵ��ĳ���Ϊ`result[index] = min{k1,k2}`��`k1 = result[index-1] + 1`��`k2`Ϊ��`index`λ����ǰ��ֱ������`index`λ�õ��ַ���`index=0`Ϊֹ���Ӵ����ȡ�


**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��96 ms, ������ C# �ύ�л����� 82.81% ���û�
- �ڴ����ģ�25.2 MB, ������ C# �ύ�л����� 25.52% ���û�

```c
public class Solution
{
    public int LengthOfLongestSubstring(string s)
    {
        if (string.IsNullOrEmpty(s))
            return 0;
        int[] result = new int[s.Length];
        result[0] = 1;

        for (int i = 1; i < s.Length; i++)
        {
            int count = GetLength(i, s);
            result[i] = result[i-1] < count ? result[i-1]+1 : count;
        }
        return result.Max();
    }
    private int GetLength(int index,string s)
    {
        char c = s[index];
        int result = 1;
        for (int i = index-1; i >= 0; i--)
        {
            if (s[i] != c)
                result += 1;
            else
                break;
        }
        return result;
    }
}
```

---
## ��Ŀ07��������Ӵ�

> - ��ţ�5
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/longest-palindromic-substring/


����һ���ַ��� s���ҵ� s ����Ļ����Ӵ�������Լ��� s ����󳤶�Ϊ 1000��

<b>ʾ�� 1</b>��
```c
����: "babad"
���: "bab"
ע��: "aba" Ҳ��һ����Ч�𰸡�
```

<b>ʾ�� 2</b>��
```c
����: "cbbd"
���: "bb"
```

<b>ʾ�� 3</b>��
```c
����: "a"
���: "a"
```

**˼·��** ���ö�̬�滮�ķ�����

������һ�������ͷ�������ͬ���ַ��������磬��aba���ǻ��ģ�����abc�����ǡ�

��̬�滮�㷨����η����ƣ������˼��Ҳ�ǽ����������ֽ�����ɸ������⣬����������⣬Ȼ�����Щ������Ľ�õ�ԭ����Ľ⡣

����η���ͬ���ǣ�<u>�ʺ����ö�̬�滮�������⣬���ֽ�õ��������������ǻ�������ģ�����һ���ӽ׶ε�����ǽ�������һ���ӽ׶εĽ�Ļ����ϣ����н�һ������⣩</u>�����÷��η������������⣬��ֽ�õ�����������Ŀ̫�࣬��Щ�����ⱻ�ظ������˺ܶ�Ρ���������ܹ�<u>�����ѽ����������Ĵ𰸣�������Ҫʱ���ҳ�����õĴ𰸣������Ϳ��Ա���������ظ����㣬��ʡʱ��</u>��

���ǿ�����һ��������¼�����ѽ��������Ĵ𰸡����ܸ��������Ժ��Ƿ��õ���ֻҪ������������ͽ�����������С�����Ƕ�̬�滮���Ļ���˼·��

����Ķ�̬�滮�㷨���ֶ����������Ǿ�����ͬ��<u>����ʽ</u>��

ʹ�üǺ� `s[l, r]` ��ʾԭʼ�ַ�����һ���Ӵ���`l`��`r` �ֱ�����������ұ߽������ֵ��ʹ����ա��ұ������ʾ���ұ߽����ȡ����

`dp[l, r]` ��ʾ�Ӵ� `s[l, r]`�������������Ҷ˵㣩�Ƿ񹹳ɻ��Ĵ�����һ����ά���������顣

- ���Ӵ�ֻ���� 1 ���ַ�����һ���ǻ����Ӵ���
- ���Ӵ����� 2 �������ַ���ʱ��`s[l, r]` ��һ�����Ĵ�����ô������Ĵ����߸�����������һ���ַ���������ԵĻ������Ӵ� `s[l + 1, r - 1]` Ҳһ���ǻ��Ĵ���

�ʣ��� `s[l] == s[r]` ������ʱ��`dp[l, r]`��ֵ�� `dp[l + 1, r - l]` ���������ﻹ��Ҫ�ٶ࿼��һ��㣺��ԭ�ַ���ȥ�����ұ߽硱���Ӵ��ı߽������

- ��ԭ�ַ�����Ԫ�ظ���Ϊ 3 ��ʱ��������ұ߽���ȣ���ôȥ�������Ժ�ֻʣ�� 1 ���ַ�����һ���ǻ��Ĵ�����ԭ�ַ���Ҳһ���ǻ��Ĵ���
- ��ԭ�ַ�����Ԫ�ظ���Ϊ 2 ��ʱ��������ұ߽���ȣ���ôȥ�������Ժ�ֻʣ�� 0 ���ַ�����Ȼԭ�ַ���Ҳһ���ǻ��Ĵ���

���ϣ����һ���ַ��������ұ߽���ȣ��ж�Ϊ����ֻ�����¶���֮һ�������ɣ�
- ȥ�����ұ߽��Ժ���ַ������������䣬��`s[l + 1, r - 1]`����Ԫ������2��������`r - l <= 2`��
- ȥ�����ұ߽��Ժ���ַ����ǻ��Ĵ�����`dp[l + 1, r - 1] == true`��

![](https://img-blog.csdnimg.cn/20200317155934443.png)

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 232 ms, ������ C# �ύ�л����� 46.79% ���û�
- �ڴ�����: 40.9 MB, ������ C# �ύ�л����� 5.43% ���û�


```c
public class Solution {
    public string LongestPalindrome(string s) 
    {
        if (string.IsNullOrEmpty(s))
            return string.Empty;
        int len = s.Length;
        if (len == 1)
            return s;
        int longestPalindromelen = 1;
        string longestPalindromeStr = s.Substring(0, 1);
        bool[,] dp = new bool[len, len];

        for (int r = 1; r < len; r++)
        {
            for (int l = 0; l < r; l++)
            {
                if (s[r] == s[l] && (r - l <= 2 || dp[l + 1, r - 1] == true))
                {
                    dp[l, r] = true;
                    if (longestPalindromelen < r - l + 1)
                    {
                        longestPalindromelen = r - l + 1;
                        longestPalindromeStr = s.Substring(l, r - l + 1);
                    }
                }
            }
        }
        return longestPalindromeStr;        
    }
}
```


---
## ��Ŀ08���ַ������

> - ��ţ�43
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/multiply-strings/


�����������ַ�����ʽ��ʾ�ķǸ�����`num1`��`num2`������`num1`��`num2`�ĳ˻������ǵĳ˻�Ҳ��ʾΪ�ַ�����ʽ��

<b>ʾ�� 1</b>:
```c
����: num1 = "2", num2 = "3"
���: "6"
```

<b>ʾ�� 2</b>:
```c
����: num1 = "123", num2 = "456"
���: "56088"
```



<b>ʾ�� 3</b>:
```c
����: num1 = "498828660196", num2 = "840477629533"
���: "419254329864656431168468"
```


<b>˵��</b>��

- `num1`��`num2`�ĳ���С��110��
- `num1`��`num2`ֻ�������� 0-9��
- `num1`��`num2`�������㿪ͷ������������ 0 ����
- ����ʹ���κα�׼��Ĵ������ͣ����� BigInteger����ֱ�ӽ�����ת��Ϊ����������


**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ��132 ms, ������ C# �ύ�л����� 94.74% ���û�
- �ڴ����ģ�24.1 MB, ������ C# �ύ�л����� 31.82% ���û�

```c
public class Solution {
    public string Multiply(string num1, string num2) {
        if (num1 == "0" || num2 == "0")
            return "0";
        int len1 = num1.Length;
        int len2 = num2.Length;
        int len = len1 + len2;
        int[] temp = new int[len];

        for (int i = len2 - 1; i >= 0; i--)
        {
            int k = len2 - i;
            int b = num2[i] - '0';
            for (int j = len1 - 1; j >= 0; j--)
            {
                int a = num1[j] - '0';
                int c = a*b;

                temp[len - k] += c%10;
                if (temp[len - k] >= 10)
                {
                    temp[len - k] = temp[len - k]%10;
                    temp[len - k - 1]++;
                }

                temp[len - k - 1] += c/10;
                if (temp[len - k - 1] >= 10)
                {
                    temp[len - k - 1] = temp[len - k - 1]%10;
                    temp[len - k - 2]++;
                }
                k++;
            }
        }

        StringBuilder sb = new StringBuilder();
        int s = temp[0] == 0 ? 1 : 0;
        while (s < len)
        {
            sb.Append(temp[s]);
            s++;
        }
        return sb.ToString();        
    }
}
```






---
## ��Ŀ09��������ʽƥ��

> - ��ţ�10
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/regular-expression-matching/

����һ���ַ���`s`��һ���ַ�����`p`��������ʵ��һ��֧�� '.' �� '*' ��������ʽƥ�䡣

```c
'.' ƥ�����ⵥ���ַ�
'*' ƥ���������ǰ�����һ��Ԫ��
```

��νƥ�䣬��Ҫ���� **����** �ַ���`s`�ģ������ǲ����ַ�����

**˵��:**

- `s`����Ϊ�գ���ֻ������ a-z ��Сд��ĸ��
- `p`����Ϊ�գ���ֻ������ a-z ��Сд��ĸ���Լ��ַ� '.' �� '*'��

**ʾ�� 1:**

```c
����: 
s = "aa"
p = "a"
���: false
����: "a" �޷�ƥ�� "aa" �����ַ�����
```
**ʾ�� 2:**

```c
����:
s = "aa"
p = "a*"
���: true
����: ��Ϊ '*' �������ƥ���������ǰ�����һ��Ԫ��, ������ǰ���Ԫ�ؾ��� 'a'����ˣ��ַ��� "aa" �ɱ���Ϊ 'a' �ظ���һ�Ρ�
```

**ʾ�� 3:**

```c
����:
s = "ab"
p = ".*"
���: true
����: ".*" ��ʾ��ƥ�����������'*'�������ַ���'.'����
```

**ʾ�� 4:**

```c
����:
s = "aab"
p = "c*a*b"
���: true
����: ��Ϊ '*' ��ʾ������������� 'c' Ϊ 0 ��, 'a' ���ظ�һ�Ρ���˿���ƥ���ַ��� "aab"��
```

**ʾ�� 5:**

```c
����:
s = "mississippi"
p = "mis*is*p*."
���: false
```

**˼·**�����ݷ���

����ƥ��˼·��ʵ���ǲ��ϵؼ���`s`��`p`�Ŀ���ƥ���ײ���ֱ��һ���������ַ�������Ϊ�յ�ʱ�򣬸�������������ó����ۡ�

���ֻ��������ͨ�ַ�������ƥ�䣬��������Ƚϼ��ɣ�

```c
if (s[i] == p[i])
```

���������ʽ�ַ���pֻ��һ��"."һ�������ǣ���Ȼ�ǰ�������Ƚϼ��� ��

```c
if (s[i] == p[i] || p[i] == '.')
```

�����������ʵ��ʱ����Ҫ�ж��ַ������Ⱥ��ַ����пյĲ�����

���ǣ�"*"��������ַ���Ҫ���⴦����p�ĵ�i��Ԫ�ص���һ��Ԫ�����Ǻ�ʱ�������������

- `i`Ԫ����Ҫ����0�Σ����Ǿͱ���`s`���䣬��`p`�ļ�������Ԫ�أ�����`IsMatch`������`s��bc��p��a*bc`�����Ǿͱ���`s`���䣬����`p`��"a*"������`IsMatch(s:bc,p:bc)`��
- `i`Ԫ����Ҫ����һ�λ����Σ��ȱȽ�`i`Ԫ�غ�`s`��Ԫ�أ�����򱣳�`p`���䣬`s`������Ԫ�أ�����`IsMatch`������`s��aabb��p��a*bb`���ͱ���`p`���䣬����`s`����Ԫ�أ�����`IsMatch(s:abb,p:a*bb)`��

��ʱ����һЩ��Ҫ˼�������������`s��abb��p��a*abb`���������ַ�ʽ����

- ���������ڶ�������Ƚ�`i`Ԫ�غ�`s`��Ԫ�أ�������Ⱦͻ����`s`�����ַ�������`IsMatch(s:bb,p:a*abb)`���ڰ���������һ�������ȥ`p`������Ԫ�أ�����`IsMatch(s:bb,p:abb)`�����յ���`false`��
- ֱ�Ӱ���������һ�������ȥ`p`������Ԫ�أ�����`IsMatch(s:abb,p:abb)`�����յ���`true`��

����˵������һ�ֱ����������Ὣ���е������һ�ߣ������Ƿ���ڿ���ƥ��������




**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��768 ms, ������ C# �ύ�л����� 10.69% ���û�
- �ڴ����ģ�25.6 MB, ������ C# �ύ�л����� 5.00% ���û�

```c
public class Solution
{
    public bool IsMatch(string s, string p)
    {
        //������pΪ�մ�����sΪ�մ�ƥ��ɹ���s��Ϊ�մ�ƥ��ʧ�ܡ�
        if (string.IsNullOrEmpty(p))
            return string.IsNullOrEmpty(s) ? true : false;

        //�ж�s��p�����ַ��Ƿ�ƥ�䣬ע��Ҫ���ж�s��Ϊ��
        bool headMatched = string.IsNullOrEmpty(s) == false
            && (s[0] == p[0] || p[0] == '.');

        if (p.Length >= 2 && p[1] == '*')
        {
            //���p�ĵ�һ��Ԫ�ص���һ��Ԫ����*����ֱ��������������ж�
            return IsMatch(s, p.Substring(2)) ||
                (headMatched && IsMatch(s.Substring(1), p));
        }
        else if (headMatched)
        {
            //�������s��p�����ַ����
            return IsMatch(s.Substring(1), p.Substring(1));
        }
        else
        {
            return false;
        }
    }
}
```

## ��Ŀ10��ͨ���ƥ��


> - ��ţ�44
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/wildcard-matching/


����һ���ַ���(`s`) ��һ���ַ�ģʽ(`p`) ��ʵ��һ��֧��`'?'`��`'*'`��ͨ���ƥ�䡣

```
'?' ����ƥ���κε����ַ���
'*' ����ƥ�������ַ������������ַ�������
�����ַ�����ȫƥ�����ƥ��ɹ���
```

**˵��:**

- `s`����Ϊ�գ���ֻ������`a-z`��Сд��ĸ��
- `p`����Ϊ�գ���ֻ������`a-z`��Сд��ĸ���Լ��ַ�`?`��`*`��

**ʾ�� 1:**

```c
����:
s = "aa"
p = "a"
���: false
����: "a" �޷�ƥ�� "aa" �����ַ�����
```
**ʾ�� 2:**

```c
����:
s = "aa"
p = "*"
���: true
����: '*' ����ƥ�������ַ�����
```

**ʾ�� 3:**

```c
����:
s = "cb"
p = "?a"
���: false
����: '?' ����ƥ�� 'c', ���ڶ��� 'a' �޷�ƥ�� 'b'��
```

**ʾ�� 4:**

```c
����:
s = "adceb"
p = "*a*b"
���: true
����: ��һ�� '*' ����ƥ����ַ���, �ڶ��� '*' ����ƥ���ַ��� "dce".
```

**ʾ�� 5:**

```c
����:
s = "acdcb"
p = "a*c?b"
���: false
```

**ʾ�� 6:**

```c
���룺
"abefcdgiescdfimde"
"ab*cd?i*de"
�����true
```

**ʾ�� 7:**

```c
���룺
"aaaa"
"***a"
�����true
```


**˼·**��˫��������

������`i`��`j`�ֱ���`s`��`p`�ĵ�һ���ַ��±꣬������ʼ��Ϊ0����`istart`��`jstart`�ֱ���`s`��`p`��`'*'`ƥ�����λ�ã�����ʼ��Ϊ`-1`��

����ͨ�ַ���ƥ���˼·��࣬�Ѿ�ƥ��ɹ��Ĳ��־Ͳ��ٿ����ˣ�����Ҫ��`i`��`j`��ǵ�ǰ���ڱȽϵ��ַ����������ƥ�����`'*'`���ܻᱻ�ظ�ʹ��ȥƥ�������ַ�����������Ҫ��`istart`��`jstart`�ֱ���`s`��`p`�����ƥ���`'*'`��λ�á�

1. ���`i`��`j`��ǵ��ַ�������Ȼ���`j`�ַ���`'?'`ƥ��ɹ�����"�Ƴ�"`i`��`j`Ԫ�أ�������`i`��`j`��
2. �������`j`�ַ���`'*'`��Ȼ����ƥ��ɹ�������`istart`��`jstart`�ֱ���`i`Ԫ�غ�`j`Ԫ�أ�����`j`��
3. �ٷ������`istart>-1`˵��֮ǰƥ���`'*'`����Ϊ`'*'`����ƥ�����ַ�����������Ҫ�ٴ�����������ƥ�����`'*'`ƥ�������ַ����ƶ�`i`���`istart`����һ���ַ�������`istart`���±��`i`Ԫ�أ�ͬʱ�ƶ�`j`���`jstart`����һ���ַ���
4. ������������������㣬��ƥ��ʧ�ܣ�����`false`��

���`s`�е��ַ����ж���ϣ�����Ϊ`s`Ϊ�գ���ʱ��Ҫ`p`Ϊ�ջ���`p`��ֻʣ���Ǻŵ�ʱ�򣬲��ܳɹ�ƥ�䡣

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��92 ms, ������ C# �ύ�л����� 95.00% ���û�
- �ڴ����ģ�25.7 MB, ������ C# �ύ�л����� 66.67% ���û�

```c
public class Solution
{
    public bool IsMatch(string s, string p)
    {
        //������pΪ�մ�����sΪ�մ�ƥ��ɹ���s��Ϊ�մ�ƥ��ʧ�ܡ�
        if (string.IsNullOrEmpty(p))
            return string.IsNullOrEmpty(s) ? true : false;

        int i = 0, j = 0, istart = -1, jstart = -1, plen = p.Length;

        //�ж�s�������ַ��Ƿ�ƥ��
        while (i < s.Length)
        {
            //����ƥ��ɹ�����Լ�ƥ��ʧ�ܷ���false
            if (j < plen && (s[i] == p[j] || p[j] == '?'))
            {
                i++;
                j++;
            }
            else if (j < plen && p[j] == '*')
            {
                istart = i;
                jstart = j;
                j++;
            }
            else if (istart > -1)
            {
                i = istart + 1;
                istart = i;
                j = jstart + 1;
            }
            else
            {
                return false;
            }
        }
        //s�е��ַ����ж���ϣ�����ΪsΪ��
        //��ʱ��ҪpΪ�ջ���p��ֻʣ���Ǻŵ�ʱ�򣬲��ܳɹ�ƥ�䡣
        //���p��ʣ��Ķ���*��������Ƴ�ʣ���*
        while (j < plen && p[j] == '*')
        {
            j++;
        }
        return j == plen;
    }
}
```

