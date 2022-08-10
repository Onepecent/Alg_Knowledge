<a name="NTsMg"></a>
## 文章:
[leetcode论坛](https://leetcode.cn/circle/article/edYbW9/)<br />[csdn文章](https://blog.csdn.net/helloworldchina/article/details/104465772)<br />BF算法（Brute Force）<br />BM算法(Boyer-Moore)<br />KMP算法（Knuth-Morris-Pratt）<br />[点击查看【bilibili】](https://player.bilibili.com/player.html?bvid=BV1Px411z7Yo)

[印度三哥 超推荐](https://www.bilibili.com/video/BV18k4y1m7Ar?p=2&spm_id_from=333.1007.top_right_bar_window_history.content.click)<br />[点击查看【bilibili】](https://player.bilibili.com/player.html?bvid=BV18k4y1m7Ar&p=2&page=2)

<a name="iUB1r"></a>
#### [28. 实现 strStr()](https://leetcode.cn/problems/implement-strstr/)
实现 strStr() 函数。<br />给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回  -1 。<br />说明：<br />当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。<br />对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与 C 语言的 strstr() 以及 Java 的 indexOf() 定义相符。<br />示例 1：<br />输入：haystack = "hello", needle = "ll"<br />输出：2<br />示例 2：<br />输入：haystack = "aaaaa", needle = "bba"<br />输出：-1
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int[] next = getNext(needle);//初始化next数组
        char[] hay = haystack.toCharArray();
        char[] nee = needle.toCharArray();
        /*比较阶段*/
        int i=0,j=0;//用来比较两字符串数组
        while(i<haystack.length()){
            if(hay[i] == nee[j]){//相等情况
                i++;
                j++;
            }else if(j>0){//不相等,且j能前移
                j = next[j-1];
            }else{//不相等,j不能能前移
                i++;
            }
            if(j==needle.length()){//当j移动的长度与匹配串相等时,匹配成功
                return i-j;
            }
        }
        return -1;
    }
    /*获得next数组*/
    public int[]  getNext(String needle){
        int[] next = new int[needle.length()];
        char[] nee = needle.toCharArray();
        int j = 0;
        for(int i=1;i<needle.length();i++){
            while(j>0 && nee[i] != nee[j]){
                j = next[j-1];
            }
            if(nee[i] == nee[j]){
                next[i] = j+1;
                j++;
            }
        }
        return next;
    }
}
```
