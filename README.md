## Testing GitHub Pages site locally with Jekyll
1. Prerequisites
    - Install [Ruby](https://www.ruby-lang.org/en/documentation/installation/)
    - Install [Bundler](https://bundler.io/)
    - Install [Jekyll](https://jekyllrb.com/docs/installation/)
2. Run
    ```bash
    # use --baseurl="/${repo_name} for dealing with url reference in local mode and production mode
    bundle exec jekyll serve --baseurl="/spark-notes"
    ```
3. To preview your site, in your web browser, navigate to [http://localhost:4000](http://localhost:4000)

## Spark Config Generator
- [Spark Conf Generator](../spark-notes/spark-conf-generator)

### TODO
- [x] If additional config, if value is input then add it to spark submit generator else return nothing
- [x] If additional config, if value is input then add it to spark conf generator else return nothing
- [x] If hover over the label or input, definition should be pop up
- [x] Create a copy button to copy generated text

## Parsing nested XML using XSD structure
- [Parsing nested XML](../spark-notes/parsing-nested-xml)

### TO DO
- [x] Extract a Spark DataFrame schema from XSD file
- [x] Pyspark notes

## Apache Iceberg guide
- [Iceberg 101](https://www.dremio.com/blog/apache-iceberg-101-your-guide-to-learning-apache-iceberg-concepts-and-practices/)

### TO DO

## Poetry with Conda
- [Poetry with Conda](https://michhar.github.io/2023-07-poetry-with-conda/)

## Spark streaming

## References Contents
- [Spark Conf Optimizer](https://sparkconfigoptimizer.com/)

## Test Contents
Following are the blogs that I compiled from my learnings on Spark:
- [Where does Spark fit in Hadoop ecosystem?](https://spoddutur.github.io/spark-notes/hadoop-map-reduce-vs-spark)
- [How to Size Executors, Cores and Memory for a Spark application running in memory](https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application)
- [Deep dive into Spark Data Layout](https://spoddutur.github.io/spark-notes/deep_dive_into_storage_formats)
- [Evolution of Second generation Tungsten Engine](https://spoddutur.github.io/spark-notes/second_generation_tungsten_engine)
- [Task Memory Management in ApacheSpark](https://spoddutur.github.io/spark-notes/task_memory_management_in_spark)
- [Spark as cloud-based SQL Engine for BigData via ThriftServer](https://spoddutur.github.io/spark-notes/spark-as-cloud-based-sql-engine-via-thrift-server)
- [Building real-time interactive applications with Spark](https://spoddutur.github.io/spark-notes/build-real-time-interations-with-spark)
- [Spark as Knowledge Browser and the impact of DataSchema on performance](https://spoddutur.github.io/spark-notes/knowledge-browser)
- [Rebroadcasting a Broadcast Variable](https://spoddutur.github.io/spark-notes/rebroadcast_a_broadcast_variable)
- [How to weave a periodically changing cached-data with your streaming application?](https://spoddutur.github.io/spark-notes/weaving_a_changing_broadcast_variable)
- [Spark-Scala Setup in Jupyter](https://spoddutur.github.io/spark-notes/jupyter-spark-setup)
- [Troubles of using filesystem (S3/HDFS) as data source in Spark](https://spoddutur.github.io/spark-notes/s3-filesystem-as-datasource-in-spark)