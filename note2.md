# Introaduction to Toleerant Retrideval
## 本篇重點
```
Dictionary
Tolerant Retrieval
    -Wildcard Query
    -Misspelled Correction
Dictionary Compression
```
##
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
WHY? 
-> 效率問題
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
    ```
        O((m * n) * M)
    ```
    2. weighted edit distance
    3. k-gram overlap
    ```
        O((m + n) * M)
    ```
    * 避免太長的單字 而相似高 

        -> **Jaccard coefficient**
        * 交集 / 聯集
        * always assigns a number between 0 and 1

## Dictionary Compression
* Problem
```
Uncompressed indexes might be large
```
* Vocablary Size ?
    * Heaps' Law
```
    estimating the number of terms
    M = k(T)^b 
    M : vocabulary size ; T : collection size ; k, b : constant
```
##
* fixed-width terms are wasteful
    * 假設每個單字固定 20 bytes 來存
    * frequency 也用 4 個 bytes 來存
    * 指標 (指向 postings list) 也用 4 個 bytes 來存
    * 假設有 40 萬個單字, 那麼我們共需要 M * (20 + 4 + 4) = 400,000 * 28 = 11.2 MB 來存下這整個 dictionary

* Dictionary as a string
    * store dictionary as a long string characters
    * 假設40萬個單字
    * Freq 4 bytes
    * pointer to Postings 4 bytes
    * pointer 3 bytes
    * 400K terms x 19 ->7.6 MB (against 11.2MB
    for fixed width)
```
    40萬個字平均單字8個字=3.2MB
    3,200,000個位置 取LOG可知指標(pointer用來記得起始點, 區隔哪裡到哪裡是某個單字)需幾bit
    約3個bytes
``` 
## Postings compression
* 比起 dictionary, postings 大很多
* 假設有 80 萬篇文章, 那麼一個 docID 需要的大小就是 80 萬取 log, 約為 20 bits
* 因此改採用的方式 : 不直接存文章的 ID, 而是存它們的 gap, 來降低編碼的數字