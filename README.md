# big-data-project

## Steps to create RDD's and processing data through Spark and performing word count operation.

- Obtain data from any text file or use [Dr.DeniseCase's repo](https://github.com/denisecase/setup-spark) and get the sample text file.
- Use ```curl "URL for Website" -O "file name to be saved"``` command to obtain HTML content into a text file.

### Step 1: Creating a Resilient Distributed Datasets

Resilient distributed datasets can be created in two ways.

1. By loading an external dataset

   ``` val sampleRDD = sc.textFile("D:/romeo.txt")```

1. By distributing collection of Objects

   ```val sampleRDD = sc.parallelize(List["red" "blue"])```

### Step 2: Breaking each line into words using flatMap

```val sampleWC = sampleRDD.flatMap(line => line.split(" "))```

### Step 3: Map each word to a count using map function and perform aggregation of words using reduceByKey

```val sampleMap = sampleWC.map(word => (word, 1)).reduceByKey((a, b) => a + b)```

### Step 4: Display the contents using collect() function

```sampleMap.collect()```

- #### Result: The above command displays all the unique words with their counts as key-value pairs:

```Array[(String, Int)] = Array((stumbled,1), (better.,1), (joy.,1), (drivelling,1), (nobleman,1), (dream'd,1), (shot,2), (Mantua,2), (woe!,2), (fast.,1), (Saints,1), (said;,2), (catch'd,1), (courtesy,,1), (behind,2), (lenten,1), (unluckily,,1), (Father,,1), (been,19), (they,,2), (watch'd,1), (countervail,1), (crying,2), (breath,5), (eyes,--,1), (knows,3), (shroud;,2), (tears?,2), (bride.,3), (tips,1), (are,62), (Pretty,1), (stand:,3), (smooth,2), (shut,2), (grant,2), (pilgrimage!,1), (morn,1), (Why,,14), (daughter's,3), (jaunt,1), (son,10), (dead,13), (am.,1), (what's,2), (earth:,1), (Alla,1), (name;,2), (thee,,33), (fourteen.,3), (thus,4), (execution.,1), (need,,1), (leap,,1), (iron,3), (Hark,,1), (you,',1), (drew,2), (already:,1), (air.,1), (swear,,2), (Francis,,1), (sharp,1), (co...```

### Step 5: Performing sorting(sortBy) and obtain the top results using take() method

```var res = sampleMap.sortBy(_._2,false).take(10);```

- #### Result: 
```Array[(String, Int)] = Array((the,611), (I,546), (and,471), (to,432), (a,398), (of,361), (my,315), (is,292), (in,280), (that,252))```

### Step 6: Transfer results from command prompt to a text file

```
def exportResults(f: java.io.File)(op: java.io.PrintWriter => Unit) {
|   val p = new java.io.PrintWriter(f)
|   try { op(p) } finally { p.close() }
| }
exportResults(new File("D:/example.txt")) { p =>
|   data.foreach(p.println)
| }
```

### Step 7: Transfer the results to an excel file and visualize them.

![results](results.PNG)



### Reference

1. Spark data set-up on windows --> https://github.com/denisecase/setup-spark

1. Creating and Managing RDD ---> https://spark.apache.org/docs/latest/rdd-programming-guide.html

1. File handling ---> https://stackoverflow.com/questions/4604237/how-to-write-to-a-file-in-scala
````
