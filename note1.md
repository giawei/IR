# Introduction to Boolean Model
## Information retrieval
* Information retrieval is the activity of obtaining information    resources relevant to an information need from a collection of
    information resources
## web search engine
* A web search engine is designed to search for
    information on the World Wide Web
## Boolean retrieval model
* The Boolean retrieval model is being able to ask a
    query that is a Boolean expression
* Many search systems you still use are Boolean:
    1. Email
    2. library catalog
    3. Mac OS X Spotlight
## Inverted index
* For each term t, we store a list of all documents that contain t
    -Identify each doc by a docID, a document serial number
## Initial stages of text processing
* Tokenization

    -Cut character sequence into word tokens
    會有語言問題 ex:日文和中文字和字之間沒有空格
* Normalization

    -Map text and query term to same form
    * U.S.A. and USA
* Stemming

    -We may wish different forms of a root to match
    * authorize, authorization
* Stop words
    * the, a, to, of
* inverted index
    * dictionary + postings (frequency is also added)

* query processing 'AND'
    * intersection
    * merge : O(x+y)
```
Key: postings sorted by docID
加速方法:augment postings
利用空間換時間
多記 skip pointer (通常取sqrt(L))
```

##  More Complicated Queries
### Phrase Quries
* ex: "stanford university", 希望搜尋的是那間史丹佛大學, 而非位於史丹佛的一間大學
* biword index
    * For example the text “Friends, Romans, Countrymen” would generate the biwords
    -friends romans
    -romans countrymen
    * issue
        *單字更長更複雜該怎麼辦 ?
        *storage concern
* positional index
    * 記住 term 出現在哪一頁哪一位置
    * 所有 query 都可以支援 但需花時間檢查
    * 以時間換空間