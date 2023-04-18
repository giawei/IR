# Introaduction to Toleerant Retrideval
## 本篇重點
```
Dictionary
Tolerant Retrieval
    -Wildcard Query
    -Misspelled Correction
Dictionary Compression
```
* Some IR systems use
    * hashes O(1)
        * No prefix search
    * trees O(logM)
        * Simplest : Binary tree
        * More usual : B-trees
        * support wild query (solve the prefix problem)
        * rebalancing binary trees is expensive

### Wild-card queries
* mon*
    -easy
    -retrieve mon <= w < moo
* *mon
    -harder
    -retrieve nom <= w < non

### Bigram(k-gram) index
* k 太小沒效率 太大湊不出來 難處理

```
Google wildcard used in whole words, not parts of words
☆Google has very limited support for wildcard queries
WHY? -> 效率問題
```

## Spell correction
```
Misspelled
    Information -> Infomaition
Context sensitive
    from -> form
    I flew form Heathrow to Narita
```
### Misspelled
* When 
    quite rare or not at all the dictionary
* Apporach
    1. 找相似的
    2. 計算相似度
    3. 選擇頻率最高的字
* method
    1. Edit distance (Levenshtein distance)
        * O((m * n) * M)
    2. weighted edit distance
    3. k-gram overlap
        * O((m + n) * M)
    * 避免太長的單字 而相似高 

        -> **Jaccard coefficient**
        * 交集 / 聯集
        * always assigns a number between 0 and 1

