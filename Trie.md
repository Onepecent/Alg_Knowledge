# Trie

Trie补题:

概念:`前缀树 `是 N叉树 .通常来说,前缀树是用来`存储字符串` 的.`前缀树`的每一个节点代表一个 `字符串`（前缀）.每一个节点会有多个子节点，通往不同子节点的路径上有着不同的字符。子节点代表的字符串是由节点本身的 `原始字符串 `，以及 通往该子节点路径上所有的`字符` 组成的.

前缀树广泛应用于 `存储` 字符串和 `检索` 关键字，特别是和 `前缀` 相关的关键字	

----

### 实现 Trie (前缀树)

#### [208. 实现 Trie (前缀树)](https://leetcode.cn/problems/implement-trie-prefix-tree/)

**建议直接撸一边就熟悉了**

----

```java
class Trie {
    Trie[] children;
    boolean isWord;
    //char c;
    public Trie() {
        children = new Trie[26];
    }
    
    public void insert(String word) {
        Trie node = this;
        int n = word.length();
        if(n == 0) return;
        for(int i = 0; i < n; i++){
            int cc = word.charAt(i) - 'a';
            if(node.children[cc] == null) node.children[cc] = new Trie();//这步很关键
            node = node.children[cc];
        }
        node.isWord = true;
    }
    
    public boolean search(String word) {
        Trie node = find(word);
        return  node!=null && node.isWord;
    }
    
    public boolean startsWith(String prefix) {
        return find(prefix) != null;
    }
    private Trie find(String word){
        Trie node = this;
        int n = word.length();
        for(int i = 0; i < n; i++ ){
            int t = word.charAt(i) - 'a';
            node = node.children[t];
            if(node == null) break;
        }
        return node;
    }
}
```

当你熟悉了基础的结构后,可以进行一些与实际相关的应用:

1.浏览器的自动补全[Ngram?]

2.单词拼写检查[在前缀树中找到具有相同前缀的单词很容易。但是怎么找到相似的单词呢？]

[677. 键值映射](https://leetcode.cn/problems/map-sum-pairs/)

```java
class MapSum {

    MapSum[] child;
    int sumCount;
    int preVal;

    public MapSum() {
        child = new MapSum[26];
        sumCount = 0;
        preVal = 0;
    }
    
    private MapSum find(String key){
        MapSum node = this;
        int n = key.length();
        for(int i = 0; i < n; i++){
            int index = key.charAt(i) - 'a';
            if(node.child[index] == null) return null;
            node = node.child[index];
        }
        return node;
    }
    
    public void insert(String key, int val) {//边插入边维护
        int n = key.length();
        MapSum temp = find(key);
        int t = val;
        if(temp != null) t = val - temp.preVal;
        MapSum node = this;
        for(int i = 0; i < n; i++){
            int index = key.charAt(i) - 'a';
            if(node.child[index] == null) node.child[index] = new MapSum();
            node = node.child[index];
            node.sumCount += t;
        }
        node.preVal = val;
    }
    
    public int sum(String key) {
        MapSum node = this;
        int n = key.length();
        for(int i = 0; i < n; i++){
            int index = key.charAt(i) - 'a';
            if(node.child[index] == null) return 0;
            node = node.child[index];
        }
        return node.sumCount;
    }
}
```
#### [648. 单词替换](https://leetcode.cn/problems/replace-words/)

```java
class Solution {
    public String replaceWords(List<String> dictionary, String sentence) {
        int len = sentence.length();
        if(len == 1) return sentence;
        Trie node = new Trie();
        StringBuilder sb = new StringBuilder();
        String[] arr = sentence.split(" ");
        for(String str : dictionary){
            node.insert(str);
        }
        for(int i = 0; i < arr.length; i++){
            String temp = node.search(arr[i]);
            if(temp == null){
                sb.append(arr[i] + " ");
            }else{
                sb.append(temp + " ");
            }
        }
        return sb.toString().trim();
    }

    class Trie{
        boolean isWord;
        Trie[] child;
        public Trie(){
            isWord = false;
            child = new Trie[26];
        }
        
        void insert(String word){
            int n = word.length();
            Trie node = this;
            for(int i = 0; i < n; i++){
                int index = word.charAt(i) - 'a';
                if(node.child[index] == null) node.child[index] = new Trie();
                node = node.child[index];
            }
            node.isWord = true;
        }

        String search(String word){
            int n = word.length();
            Trie node = this;
            StringBuilder sb = new StringBuilder();
            for(int i = 0; i < n; i++){
                if(node.isWord) break;
                int index = word.charAt(i) - 'a';
                if(node.child[index] == null) return null;//如果有最短能匹配上的就已经break了,能走进这步代表没有能匹配上的
                sb.append(word.charAt(i));
                node = node.child[index];
            }
            return sb.toString();
        }
    }
}
```


