What is Map Reduce
=========================
MapReduce is a software framework that allows developers to write programs that process massive amounts of unstructured data in parallel across a distributed cluster of processors or stand-alone computers. It was developed at Google for indexing Web pages and replaced their original indexing algorithms and heuristics in 2004.

The framework is divided into two parts:
- Map, a function that parcels out work to different nodes in the distributed cluster.
- Reduce, another function that collates the work and resolves the results into a single value.

The MapReduce framework is fault-tolerant because each node in the cluster is expected to report back periodically with completed work and status updates. If a node remains silent for longer than the expected interval, a master node makes note and re-assigns the work to other nodes.

<hr>
### MapReduce and Hadoop

MapReduce is the heart of Hadoop. It is this programming paradigm that allows for massive scalability across hundreds or thousands of servers in a Hadoop cluster. The MapReduce concept is fairly simple to understand for those who are familiar with clustered scale-out data processing solutions.

For people new to this topic, it can be somewhat difficult to grasp, because it’s not typically something people have been exposed to previously. If you’re new to Hadoop’s MapReduce jobs, don’t worry: we’re going to describe it in a way that gets you up to speed quickly.
The term MapReduce actually refers to two separate and distinct tasks that Hadoop programs perform. 
The first is the map job, which takes a set of data and converts it into another set of data, where individual elements are broken down into tuples (key/value pairs). The reduce job takes the output from a map as input and combines those data tuples into a smaller set of tuples. As the sequence of the name MapReduce implies, the reduce job is always performed after the map job.
<hr>
### An example of MapReduce
Let’s look at a simple example. Assume you have five files, and each file contains two columns (a key and a value in Hadoop terms) that represent a city and the corresponding temperature recorded in that city for the various measurement days. Of course we’ve made this example very simple so it’s easy to follow. You can imagine that a real application won’t be quite so simple, as it’s likely to contain millions or even billions of rows, and they might not be neatly formatted rows at all; in fact, no matter how big or small the amount of data you need 
to analyze, the key principles we’re covering here remain the same. Either way, in this example, city is the key and tempera­ture is the value.

<pre><code>
Toronto, 20 
Whitby, 25 
New York, 22 
Rome, 32 
Toronto, 4 
Rome, 33 
New York, 18
</code></pre>
Out of all the data we have collected, we want to find the maximum tem­perature for each city across all of the data files (note that each file might have the same city represented multiple times). Using the MapReduce framework, we can break this down into five map tasks, where each mapper works on one of the five files and the mapper task goes through the data and returns the maximum temperature for each city. For example, the results produced from one mapper task for the data above would look like this:

<pre><code>
(Toronto, 20) (Whitby, 25) (New York, 22) (Rome, 33)
</code></pre>
Let’s assume the other four mapper tasks (working on the other four files not shown here) produced the following intermediate results:
<pre><code>
(Toronto, 18) (Whitby, 27) (New York, 32) (Rome, 37)(Toronto, 32) (Whitby, 20) (New York, 33) (Rome, 38)(Toronto, 22) (Whitby, 19) (New York, 20) (Rome, 31)(Toronto, 31) (Whitby, 22) (New York, 19) (Rome, 30)
</code></pre>
All five of these output streams would be fed into the reduce tasks, which combine the input results and output a single value for each city, producing a final result set as follows:
<pre><code>
(Toronto, 32) (Whitby, 27) (New York, 33) (Rome, 38)
</code></pre>
As an analogy, you can think of map and reduce tasks as the way a cen­sus was conducted in Roman times, where the census bureau would dis­patch its people to each city in the empire. Each census taker in each city would be tasked to count the number of people in that city and then return their results to the capital city. There, the results from each city would be reduced to a single count (sum of all cities) to determine the overall popula­tion of the empire. This mapping of people to cities, in parallel, and then com­bining the results (reducing) is much more efficient than sending a single per­son to count every person in the empire in a serial fashion.
