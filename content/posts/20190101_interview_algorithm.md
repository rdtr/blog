---
title: "凡人のためのインタビュー対策: アルゴリズム編 まとめ"
date: 2019-01-07T00:07:50-08:00
draft: true
slug: "algorithms_in_technical_interview"
---

## 整数

#### 反転
下の位からとって * 10 しながら足していくだけだが, 一度やってないと出てこないかも。

- Reverse Integer: [LeetCode](https://leetcode.com/problems/reverse-integer/) | [GeeksForGeeks](https://www.geeksforgeeks.org/reverse-digits-integer-overflow-handled/)
- Palindrome Number: [LeetCode](https://leetcode.com/problems/palindrome-number/)
 
---

## 配列

### 配列の末尾から走査する  

後ろからiterateするだけで余計な考慮が不要になって問題が簡単になるケースがある.

- Find And Replace in String: [LeetCode](https://leetcode.com/problems/find-and-replace-in-string/)  
走査しながら文字列をreplaceしていくので末尾から走査することでindexのずれを考慮しなくてよくなる

### 2 pointerで走査する

- 3 Sum: [LeetCode](https://leetcode.com/problems/3sum/)  
  

### Binary Search
指定された値を探す定番の binary search と, bisect left / right は暗記する.
(が, それ以外にいくらでも類型問題は作れる. 「最終的に無限ループにならずにちゃんと収束するか？」を気にするとバグを拾いやすいかも. [Pythonの bisectのコード](https://github.com/python/cpython/blob/3.6/Lib/bisect.py#L24)が参考になる.

- Search a 2D Matrix: [LeetCode](https://leetcode.com/problems/search-a-2d-matrix/)
- Kth Smallest Element in a Sorted Matrix (Heapでも解ける. 後述): [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) | [GeeksForGeeks](https://www.geeksforgeeks.org/kth-smallest-element-in-a-row-wise-and-column-wise-sorted-2d-array-set-1/)

### 区間和
区間[i, j]の和SUM(i, j) = SUM(0, j) - SUM(0, i-1)で求まる。

- Subarray Sum Equals K: [LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/)
- Random Pick With Weight: [LeetCode](https://leetcode.com/problems/random-pick-with-weight/) 

### 配列のShuffle

### Bucket sort
参考資料: [バケットソート](http://www.ics.kagoshima-u.ac.jp/~fuchida/edu/algorithm/sort-algorithm/bucket-sort.html)

現れる値が既知かつ有限の時のみ使えるテクニック。現れうる値の数だけバケット(配列)を用意して各要素を(配列あるいはリストで)詰めていく. この手法によりソートしなくても解ける種の問題が存在する.

- Top K Frequent Elements: [LeetCode](https://leetcode.com/problems/top-k-frequent-elements/)

### Quick select
参考資料: [Selecting median using Quick Select Algorithm(1)](http://agw.hatenablog.jp/entry/20090505/1241602074)

quick sortを途中で止めることで平均 `O(N)` で n 番目の要素を配列から取得できる. ただし最悪計算量は変わらず `O(N^2)`.
- Kth Largest Element in an Array: [Leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [GeeksForGeeks](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)

### External sort
参考資料: [External Sorting](https://www.geeksforgeeks.org/external-sorting/)

実際にコードを書くことを求められるというより, 2D matrix系の問題なんかでfollow upとして「もしmatrixすべてのデータがメモリに乗り切らないとしたらどうする?」といったときによく説明に使うテクニックだという認識. 

--- 

## 文字列

### Palindrome


### Sliding Window
2 pointerの派生で、文字列内で文字の出現頻度などの条件を満たす部分文字列を求めるような問題で使える。
最初に右のpointerを最初に条件が成立するまで進めて、そこから先は (1) 条件が成立しなくなるまで左のpointerを進める (2) 条件が再び成立するまで右の pointerを進める の繰り返し。個人的には尺取り虫のようなイメージで覚えている。

- Minimum Window Substring: [LeetCode](https://leetcode.com/problems/minimum-window-substring/) | [GeeksForGeeks](https://www.geeksforgeeks.org/find-the-smallest-window-in-a-string-containing-all-characters-of-another-string/)

## Binary Tree, Binary Search Tree

基本的な操作は覚える

- Insert into a BST: [LeetCode](https://leetcode.com/problems/insert-into-a-binary-search-tree/) | [GeeksForGeeks](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)

---

### Linked list

基本的な操作は覚える

- Reverse Linked List: [LeetCode](https://leetcode.com/problems/reverse-linked-list/)

---

## Heap

### Kth element系
与えられたデータ構造の中でK番目に大きい/小さい要素を求めよ系の問題. Binary searchでいけることもあるけど, 一番大きい/小さい要素から順に候補となる次の要素を全部ヒープに詰めて、最大/最小要素を取り出しては次の候補を詰める...と繰り返すことで検索範囲を絞れる.

- Find K Pairs with Smallest Sums: [LeetCode](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/) | [GeeksForGeeks](https://www.geeksforgeeks.org/find-k-pairs-smallest-sums-two-arrays/)
- Kth Smallest Element in a Sorted Matrix: [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) | [GeeksForGeeks](https://www.geeksforgeeks.org/kth-smallest-element-in-a-row-wise-and-column-wise-sorted-2d-array-set-1/)

--- 
## Bit演算

### 使えるテクニック
- get rightmost set bit: `i & (-i)` 
- clear rightmost set bit: `i & (i + 1)`

---
## DP

### ナップサックDP
参考資料: [典型的な DP (動的計画法) のパターンを整理 Part 1 ～ ナップサック DP 編 ～](https://qiita.com/drken/items/a5e6fe22863b7992efdb)

- Minimu Window Subsequence: [LeetCode](https://leetcode.com/problems/minimum-window-subsequence/)

### bit DP
### 区間DP

---

## グラフ

### オイラー閉路
[Hierholzer’s Algorithm](https://www.geeksforgeeks.org/hierholzers-algorithm-directed-graph/) 
例題: 
- [Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

---

## Union Find (Disjoint Set)
参考資料: [Union find(素集合データ構造)(pdf)](https://www.slideshare.net/chokudai/union-find-49066733) 

### 典型パターン
グラフ, 2D Matrix などなど応用範囲は広い。何かの条件をもとに集合をグループごとにまとめる処理があれば検討。rank, path compressionも覚えるのは比較的楽なので実装する。

例題:

- [Most Stones Removed with Same Row or Column (LeetCode)](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)

---

## Binary Indexed Tree
参考資料: [Binary Indexed Tree のはなし(pdf)](http://hos.ac/slides/20140319_bit.pdf) | [Fenwick (Binary Indexed) Trees - Hackerearch](https://www.hackerearth.com/practice/data-structures/advanced-data-structures/fenwick-binary-indexed-trees/tutorial/)

### 配列
**「i < j でA[i]とA[j]がある条件を満たすようなjはいくつあるか?」**のような問題で使える.元の配列をソートしてBITで個数を管理するのがポイント. (ちなみに変形merge sortでも解ける)

例題:

- Inversion Count: [GeeksForGeeks](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/) 
- Reverse Pairs: [LeetCode](https://leetcode.com/problems/reverse-pairs/)
- Count of Smaller Numbers After Self: [LeetCode](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)

## Square Root Decomposition
参考資料: [Sqrt (or Square Root) Decomposition Technique | Set 1 (Introduction)](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)

### 配列

Interviewでどれくらい知名度のあるテクニックなのかは未知数. 配列をsqrt(length)ごとの長さのブロックに分割することで, iterationしたりinsertするときのコストを`O(sqrt(length))`に圧縮しようというもの.

- Queue Reconstruction by Height: [LeetCode](https://leetcode.com/problems/queue-reconstruction-by-height/)

Longest Increasing Subsequence
Tailを格納してbinary searchするテクニックはおさえておく
