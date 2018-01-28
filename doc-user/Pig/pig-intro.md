# Introduction for Apache Pig Latin

This guide is an introduction for the Pig Latin language used by Apache Pig



## What is Pig Latin

Apache Pig is an abstraction over MapReduce. It is a platform used for the analyze of data sets as data flows. To write theses analyzes, the tool provides a High-level language named Pig Latin. The scripts written in Pig Latin are internally converted in MapReduce tasks by the Pig engine.



## Uses and Limitations of Pig Latin

### Usages

- Using Pig Latin, programmers can easily perform MapReduce tasks without typing complex Java program
- Pig uses a multi-query approach, thereby reducing drastically the length of the scripts ( a traditional script of over 200 lines can be written in 10 lines of Latin Pig) 
- Pig Latin is an SQL-like language
- Apache Pig provides many built-in operators to support data operations like joins, filters, ordering, etc. In addition, it also provides nested data types like tuples, bags, and maps that are missing from the initial MapReduce.
- Apache Pig is generally used to perform tasks involving ad-hoc processing and quick prototyping such as web logs, data processing for search platforms, time sensitive data loads, ...

### Limitations

- Debugging of Pig Latin script are difficult due to the UDFS.
- Data schemas are not enforced explicitly but implicitly, it may transform types in byteArray during execution
- The commands are not executed unless either you dump or store an intermediate or final result. This increases the iteration between debug and resolving the issue.
- The language is not mature yet.

## Links for useful information

**Apache Pig Reference :**

http://pig.apache.org/docs/r0.15.0/