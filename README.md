# Alg_Knowledge
leedcode + Knowledge
学习数据结构与算法期间做的好题与好知识博客

# 基础知识

----

int 类型占4个字节，每个字节占8位，所以一共有32位，除去一位符号位，也就31位，能表示整数大小是2^31 次方 2^10约等于10^3 所以 2^31约等于10^9

----

Map的遍历:<br />
for(Map.Entry<T,T> entry : map.entrySet()){ <br />
  entry.getKey(); <br />
  entry.getValue(); <br />
} <br />
Entry的运用: <br />
Map.Entry<T, T>[] entry = new Map.Entry[Length];  <br />
#遍历 <br />
for (int i = 0; i < Length; i++) {  <br />
			entry[i] = Map.entry(a[i], b[i]); <br />
} <br />
#排序(降序) <br />
Arrays.sort(entry, (o, p) -> p.getValue() - o.getValue());  <br />

----
