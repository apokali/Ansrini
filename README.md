# Ansrini Reproduction

## Anserini: BM25 Baselines for MS MARCO Document Ranking
This project intends to replicate the experiment https://github.com/castorini/anserini/blob/master/docs/experiments-msmarco-doc.md

### Data Prep
```bash
$ mkdir collections/msmarco-doc

$ wget https://msmarco.blob.core.windows.net/msmarcoranking/msmarco-docs.trec.gz -P collections/msmarco-doc

Connecting to msmarco.blob.core.windows.net (msmarco.blob.core.windows.net)|20.150.34.4|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8501799926 (7.9G) [application/x-gzip]
Saving to: ‘collections/msmarco-doc/msmarco-docs.trec.gz’

msmarco-docs.trec.gz 100%[====================>]   7.92G  3.73MB/s    in 40m 40s 

2021-08-11 10:48:20 (3.32 MB/s) - ‘collections/msmarco-doc/msmarco-docs.trec.gz’ saved [8501799926/8501799926]
```

### Indexing

```bash
$ sh target/appassembler/bin/IndexCollection -threads 1 -collection CleanTrecCollection \
 -generator DefaultLuceneDocumentGenerator -input collections/msmarco-doc \
 -index indexes/msmarco-doc/lucene-index-msmarco -storePositions -storeDocvectors -storeRaw

2021-08-11 21:20:46,053 INFO  [main] index.IndexCollection (IndexCollection.java:643) - Setting log level to INFO
2021-08-11 21:20:46,057 INFO  [main] index.IndexCollection (IndexCollection.java:646) - Starting indexer...
2021-08-11 21:20:46,057 INFO  [main] index.IndexCollection (IndexCollection.java:647) - ============ Loading Parameters ============
2021-08-11 21:20:46,058 INFO  [main] index.IndexCollection (IndexCollection.java:648) - DocumentCollection path: collections/msmarco-doc
2021-08-11 21:20:46,059 INFO  [main] index.IndexCollection (IndexCollection.java:649) - CollectionClass: CleanTrecCollection
2021-08-11 21:20:46,059 INFO  [main] index.IndexCollection (IndexCollection.java:650) - Generator: DefaultLuceneDocumentGenerator
2021-08-11 21:20:46,060 INFO  [main] index.IndexCollection (IndexCollection.java:651) - Threads: 1
2021-08-11 21:20:46,060 INFO  [main] index.IndexCollection (IndexCollection.java:652) - Stemmer: porter
2021-08-11 21:20:46,061 INFO  [main] index.IndexCollection (IndexCollection.java:653) - Keep stopwords? false
2021-08-11 21:20:46,061 INFO  [main] index.IndexCollection (IndexCollection.java:654) - Stopwords:  null
2021-08-11 21:20:46,062 INFO  [main] index.IndexCollection (IndexCollection.java:655) - Store positions? true
2021-08-11 21:20:46,062 INFO  [main] index.IndexCollection (IndexCollection.java:656) - Store docvectors? true
2021-08-11 21:20:46,063 INFO  [main] index.IndexCollection (IndexCollection.java:657) - Store document "contents" field? false
2021-08-11 21:20:46,064 INFO  [main] index.IndexCollection (IndexCollection.java:658) - Store document "raw" field? true
2021-08-11 21:20:46,064 INFO  [main] index.IndexCollection (IndexCollection.java:659) - Optimize (merge segments)? false
2021-08-11 21:20:46,065 INFO  [main] index.IndexCollection (IndexCollection.java:660) - Whitelist: null
2021-08-11 21:20:46,065 INFO  [main] index.IndexCollection (IndexCollection.java:661) - Pretokenized?: false
2021-08-11 21:20:46,065 INFO  [main] index.IndexCollection (IndexCollection.java:681) - Directly building Lucene indexes...
2021-08-11 21:20:46,066 INFO  [main] index.IndexCollection (IndexCollection.java:682) - Index path: indexes/msmarco-doc/lucene-index-msmarco
2021-08-11 21:20:46,078 INFO  [main] index.IndexCollection (IndexCollection.java:731) - ============ Indexing Collection ============
2021-08-11 21:20:46,503 INFO  [main] index.IndexCollection (IndexCollection.java:829) - Thread pool with 1 threads initialized.
2021-08-11 21:20:46,505 INFO  [main] index.IndexCollection (IndexCollection.java:831) - Initializing collection in collections/msmarco-doc
2021-08-11 21:20:46,514 INFO  [main] index.IndexCollection (IndexCollection.java:840) - 1 file found
2021-08-11 21:20:46,515 INFO  [main] index.IndexCollection (IndexCollection.java:841) - Starting to index...
2021-08-11 21:21:46,528 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 40,000 documents indexed
2021-08-11 21:22:46,532 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 100,000 documents indexed
2021-08-11 21:23:46,539 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 150,000 documents indexed
2021-08-11 21:24:46,542 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 200,000 documents indexed
2021-08-11 21:25:46,551 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 240,000 documents indexed
2021-08-11 21:26:46,556 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 290,000 documents indexed
2021-08-11 21:27:46,561 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 340,000 documents indexed
2021-08-11 21:28:46,565 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 390,000 documents indexed
2021-08-11 21:29:46,570 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 440,000 documents indexed
2021-08-11 21:30:46,583 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 500,000 documents indexed
2021-08-11 21:31:46,594 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 550,000 documents indexed
2021-08-11 21:32:46,598 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 600,000 documents indexed
2021-08-11 21:33:46,605 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 640,000 documents indexed
2021-08-11 21:34:46,610 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 640,000 documents indexed
2021-08-11 21:35:46,617 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 680,000 documents indexed
2021-08-11 21:36:46,623 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 730,000 documents indexed
2021-08-11 21:37:46,631 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 780,000 documents indexed
2021-08-11 21:38:46,636 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 840,000 documents indexed
2021-08-11 21:39:46,641 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 890,000 documents indexed
2021-08-11 21:40:46,646 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 950,000 documents indexed
2021-08-11 21:41:46,649 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,010,000 documents indexed
2021-08-11 21:42:46,653 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,060,000 documents indexed
2021-08-11 21:43:46,660 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,120,000 documents indexed
2021-08-11 21:44:46,667 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,170,000 documents indexed
2021-08-11 21:45:46,670 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,230,000 documents indexed
2021-08-11 21:46:46,677 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,280,000 documents indexed
2021-08-11 21:47:46,684 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,280,000 documents indexed
2021-08-11 21:48:46,699 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,320,000 documents indexed
2021-08-11 21:49:46,708 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,360,000 documents indexed
2021-08-11 21:50:46,716 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,410,000 documents indexed
2021-08-11 21:51:46,724 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,450,000 documents indexed
2021-08-11 21:52:46,734 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,490,000 documents indexed
2021-08-11 21:53:46,738 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,540,000 documents indexed
2021-08-11 21:54:46,745 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,600,000 documents indexed
2021-08-11 21:55:46,752 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,660,000 documents indexed
2021-08-11 21:56:46,759 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,710,000 documents indexed
2021-08-11 21:57:46,767 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,770,000 documents indexed
2021-08-11 21:58:46,773 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,820,000 documents indexed
2021-08-11 21:59:46,781 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,880,000 documents indexed
2021-08-11 22:00:46,788 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,920,000 documents indexed
2021-08-11 22:01:46,794 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,920,000 documents indexed
2021-08-11 22:02:46,806 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 1,960,000 documents indexed
2021-08-11 22:03:46,813 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,020,000 documents indexed
2021-08-11 22:04:46,820 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,070,000 documents indexed
2021-08-11 22:05:46,840 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,130,000 documents indexed
2021-08-11 22:06:46,853 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,180,000 documents indexed
2021-08-11 22:07:46,858 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,240,000 documents indexed
2021-08-11 22:08:46,865 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,290,000 documents indexed
2021-08-11 22:09:46,872 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,340,000 documents indexed
2021-08-11 22:10:46,877 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,400,000 documents indexed
2021-08-11 22:11:46,881 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,460,000 documents indexed
2021-08-11 22:12:46,889 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,520,000 documents indexed
2021-08-11 22:13:46,896 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,570,000 documents indexed
2021-08-11 22:14:46,901 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,570,000 documents indexed
2021-08-11 22:15:46,908 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,620,000 documents indexed
2021-08-11 22:16:46,915 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,680,000 documents indexed
2021-08-11 22:17:46,919 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,730,000 documents indexed
2021-08-11 22:18:46,926 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,790,000 documents indexed
2021-08-11 22:19:46,934 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,850,000 documents indexed
2021-08-11 22:20:46,939 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,910,000 documents indexed
2021-08-11 22:21:46,943 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 2,970,000 documents indexed
2021-08-11 22:22:46,956 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 3,030,000 documents indexed
2021-08-11 22:23:46,963 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 3,080,000 documents indexed
2021-08-11 22:24:46,970 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 3,140,000 documents indexed
2021-08-11 22:25:46,978 INFO  [main] index.IndexCollection (IndexCollection.java:859) - 3,190,000 documents indexed
2021-08-11 22:27:21,030 INFO  [main] index.IndexCollection (IndexCollection.java:925) - Indexing Complete! 3,213,835 documents indexed
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:926) - ============ Final Counter Values ============
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:927) - indexed:        3,213,835
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:928) - unindexable:            0
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:929) - empty:                  0
2021-08-11 22:27:21,032 INFO  [main] index.IndexCollection (IndexCollection.java:930) - skipped:                0
2021-08-11 22:27:21,032 INFO  [main] index.IndexCollection (IndexCollection.java:931) - errors:                 0
2021-08-11 22:27:21,049 INFO  [main] index.IndexCollection (IndexCollection.java:934) - Total 3,213,835 documents indexed in 01:06:34
```
