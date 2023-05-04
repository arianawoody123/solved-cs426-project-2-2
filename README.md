Download Link: https://assignmentchef.com/product/solved-cs426-project-2-2
<br>






<h1>1.      Problem Definition</h1>

In this homework , you will implement a parallel document search system. The algorithm that you will implement is similar to Supervised Search. However, it is a very simple version of it. Since this is a simplified, more abstract version tailored for this class project, do not overthink things. Instead carefully read everything about problem definition and what is expected of you.

In our system, each document  is represented with a weight vector . A weight vector  is composed of  number of elements such that each of the weight values  corresponds to the relationship between the file  and word  in our dictionary, and  is the dictionary size.  is only an integer here, we do not have an actual dictionary.

Set of documents  which contains  documents can be represented as follows:




Then, we will insert some queries to the system. A query  has same vector definition as a document vector .




Finally, your program will take  as input and will give least  related documents as output according to given <em>similarity function</em>.

You will give a document file as an input file to your system. Each line of the input file contains id of document, consecutive  integers which are seperated by a single space. Format of a line is as follows:

Doc_id: weight<sub>0 </sub>weight<sub>1</sub> … weight<sub>d </sub>

Example line for document with id 5 and a system with dictionary size 3 5: 0 5 3

And query will also be given with another input file. However, it does not contain an id field.

E.g. for a query with a dictionary size 3

2 0 7




Now, we will define our <em>similarity function</em>. Similarity of a document  to a query ,  , is defined as follows:




E.g. we can calculate similarity value for previous weight vector and query pair as follows:




To summarize, you will read documents file and query file. You will find similarity values for each document and output least related K documents’ ids, ie. With least similarity values.

<h1>2.      Implementation Details</h1>

First you will implement a <em>kreduce</em> function with the following function prototype. <em>void kreduce(int * leastk, int * myids, int * myvals, int k, int world_size, int my_rank) </em>

<em>kreduce </em>function is a collective communication function like MPI_Bcast or MPI_Reduce. All processes will call it, however only the master process will have k ids that correspond to least k values in ascending order according to their corresponding values. Meaning that <em>leastk </em>is only used by master process. Each process pass two integer arrays to this function. <em>Myids </em>array keeps ids of documents of a process and <em>myvals </em>array keeps similarity values for these documents. <em>k </em>tells that how many least elements will be selected. Last two parameters of this function is optional and their names are self explanatory.  Sizes of myids and myvals arrays are equal to k. And the values in myvals array is sorted in ascending order.

Let say, we have 2 processes running and their inputs to this function as follows:

k = 3

Process 0 (Master):

My_ids = [5, 6, 7]  My_vals = [4, 8, 14]

Process 1 (Slave):

My_ids = [1, 2, 11]

My_vals = [7, 10, 22]

And as an output of this function, process 0 should have the following values in leastk array:

leastk = [5, 1, 6]

<strong>You are not allowed to use any collective communication operations outside of this kreduce function. </strong>

<strong>The only collective communication operation that you can use in main part of your program is kreduce function and you have to use kreduce function in your main program. Better implementation of kreduce function will get better grades. </strong>

<h1>3.      Output</h1>

You will give outputs for three things. First you will print out the computation time for sequential part of your program e.g. time for reading files. Secondly, you will print out the computation time for parallel part of your program e.g. calculating least k documents for the query. Lastly, you will print out least k ids. Output format should be as follows:

Sequential Part: 1.50 ms

Parallel Part: 5.22 ms

Total Time: 7.12 ms

Least k = 3 ids:

5

1

6


