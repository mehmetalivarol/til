## RDD types in Spark 

Spark allows for the import of different kinds of data through RDDs. Mainly, people use it to access either HDFS directories or local files. the textFile method is prety flexible in both Python and Scala. It can read directories, textfiles, or groups of directories. It creates one partition in the assigned RDD for each file it reads in. 

#### Load data from HDFS into Spark shell

Python:

	pyspark
	file = sc.textFile("/hdfs/dir/files* ")
	file.getNumPartitions()
	
Other file types: 

	pyspark
	file = sc.textFile("/hdfs/dir/part-00000 ")
	file.getNumPartitions()
	
	pyspark
	file = sc.textFile("/hdfs/dir/myfile.txt ")
	file.getNumPartitions()


The vanilla install of Spark will default to reading files from your local directory; if you have Hadoop configured, you have to specify that the file is local. 
	
	pyspark
	file = sc.textFile("localdirectory://file ")
	file.getNumPartitions()
	
And:

sc.textFile("/my/dir1,/my/paths/part-00[0-5]*,/another/dir,/a/specific/file")
	
Scala

	spark-shell
	val file = sc.textFile("/hdfs/dir/files* ")
	file.getNumPartitions()

All of these are great for data that is delimited by lines. For XML, and data delimited by |, or other characters, you can also read in with a method called wholeTextFiles that creates pairRDD with first value being the path and the second being all of the contents of the file. 

	file = sc.wholeTextFiles("/hdfs/dir/files*")


Here's the difference: 	

	In [1]: logs = sc.textFile("/logdata/access_log_20160329-153657.log")
	In [2]: logs.first()
	Out[2]: u'244.157.45.12 - - [10/Oct/2013:00:04:23 ] "GET /wheelsets HTTP/1.0" 200 4677 "http://bleater.com" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1944.0 Safari/537.36"'
	In [5]: logs.getNumPartitions()
	Out[5]: 1



	In [6]: logs = sc.wholeTextFiles("/logdata/access_log_20160329-153657.log")

	In [7]: logs.first()
	Out[7]: 
	(u'hdfs://localhost:8020/logdata/access_log_20160329-153657.log',u'244.157.45.12 - - [10/Oct/2013:00:04:23 ] "GET /wheelsets 	HTTP/1.0" 200 4677 "http://bleater.com" "Mozilla/5.0 	(Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 	(KHTML, like Gecko) Chrome/36.0.1944.0 Safari/	537.36"\n123.221.14.56 - -
 	In [8]: logs.getNumPartitions()
	Out[8]: 1

To work with the second one, you'll need to flatten it: 

	In [11]: values = logs.map(lambda (fname,data): data)
	
	In [12]: values.first()
	Out[12]: u'244.157.45.12 - - [10/Oct/2013:00:04:23 ] "GET /wheelsets HTTP/1.0" 200 4677 "http://bleater.com" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1944.0 Safari/537.36"\n123.221.1