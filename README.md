# Java-based Desktop and Android applications to control the class seating layout

The repository contains an Android app that connects to the Java based server. Once logged-in a student can select the seat s/he wishes to have. Teachers can also log-in to the server to monitor the present class layout at any time.


### Java Server

Server.java creates a server using socket programming. It uses multi threading to deal with heavy traffic by assigning each client to a different thread. The thread takes input from client app and saves it for further request in a synchronized list. 

On request by teacher, it makes a query to the database, and sends the data to Teacher via network. The database is local to the server and this is important as most of the heavy processing is done on the server and having a local database will reduce the latencies of replies to the student and teacher's requests.

To start the server:
```
$ javac Server.java
$ java Server
```


### Client Android Application

This application has been developed for Android versions 7.0 and above. Student logs in by providing name and roll number(or any other authentication as needed), and then selects the seat. It also informs the user if the selected seat is available or not.

**Code and apk is present in the folder SeatPlanner**

### Teacher Application

**Teacher** is a desktop application with GUI created using Java's swing library. Teacher, on request, requests the server for current seating data.The data is sorted using **MergeSort and ForkJoin Principle**. The application then displays the layout in a new window, rendered using the GUI library. Three variations of the Teacher application are included:

* **Teacher A**: S/He creates the layout without the use of threads. The method is slowest and hence can be used to compare the advantages of multi-threading over single threaded applications.

* **Teacher B**: S/He uses ForkJoinPool to create a thread pool that is tasked with rendering of Layout. Each thread is rendering one Row of the layout and Divide and Conquer approach is used to divide task among threads. 

* **Teacher C**: S/He uses **ExecutorService** to create a thread pool.  Each thread is rendering one Row of the layout and Divide and Conquer approach is used to divide task among threads. 


To generate layout (similar for the 3 Teacher apps:
```
$ javac TeacherA.java
$ java TeacherA
```
