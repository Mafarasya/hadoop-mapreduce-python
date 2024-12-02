# Word Count MapReduce for Pembukaan UUD 1945

## Deskripsi Proyek
Proyek ini menghitung jumlah kata dalam teks Pembukaan UUD 1945 menggunakan MapReduce di Hadoop Standalone Cluster dengan Hadoop Streaming.

## Struktur Direktori
```
project-folder/
├── data/
│   ├── pembukaan_uud1945.txt       # File teks yang digunakan sebagai input
│   ├── output_wordcount.txt        # Hasil output MapReduce
├── scripts/
│   ├── mapper.py                   # Script mapper untuk MapReduce
│   ├── reducer.py                  # Script reducer untuk MapReduce
└── README.md                       # Dokumentasi proyek
```

## Cara Menjalankan
1. Copy file `pembukaan_uud1945.txt` ke dalam direktori HDFS:
    ```bash
   hdfs dfs -put pembukaan_uud1945.txt /input/

2. Jalankan hadoop streaming:
    ``` 
    !$HADOOP_HOME/bin/hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.2.3.jar \
    -input /word_count_with_python/pembukaan_uud1945.txt \
    -output /word_count_with_python/output \
    -mapper "python /content/mapper.py" \
    -reducer "python /content/reducer.py"
    ```
3. Salin hasil output ke lokal:
    ```
    !$HADOOP_HOME/bin/hdfs dfs -copyToLocal /word_count_with_python/output/part-00000 /content/hdfs-wordcount.txt
    ```

## Hasil Output
    ```
    Dan	1
    Dasar	1
    Esa,	1
    INDONESIA	1
    Indonesia	9
    Indonesia,	2
    Indonesia.	1
    ```