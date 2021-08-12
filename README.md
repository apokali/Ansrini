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
 
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:926) - ============ Final Counter Values ============
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:927) - indexed:        3,213,835
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:928) - unindexable:            0
2021-08-11 22:27:21,031 INFO  [main] index.IndexCollection (IndexCollection.java:929) - empty:                  0
2021-08-11 22:27:21,032 INFO  [main] index.IndexCollection (IndexCollection.java:930) - skipped:                0
2021-08-11 22:27:21,032 INFO  [main] index.IndexCollection (IndexCollection.java:931) - errors:                 0
2021-08-11 22:27:21,049 INFO  [main] index.IndexCollection (IndexCollection.java:934) - Total 3,213,835 documents indexed in 01:06:34
```
