> CSCI 3120 Assignment 4
>
> Due date: 11:59pm , Sunday , July 24, 20 22, submitted via Git
>
> Objectives
>
> This assignment has several objectives: (i) provide an opportunity to implement thread synchronization in a multithreaded program (ii) reinforce the concept of process synchronization and the producer con- sumer problem; and (iii) provide additional practice in C programming and understanding specifications.
>
> Preparation:
>
> 1\. Complete Assignment 3 and/or review the provided solution to Assignment 3.
>
> 2\. Clone your assignment repository:

[TABLE]

> where???? is your CSID.
>
> 3\. Copy either your own solution or the provided solution as a starting point for Assignment 4 because Assignment 4 builds on Assignment 3. A solution will be accessible on July 8 from Brightspace.
>
> 4\. **Important**: If you are using CLion with CMake you will need to ensure your CMakeLists.txt file has the additional statements as provided in Assignment 3.
>
> The repository has the same structure and caveats as Assignment 1, Assignment 2, and Assignment 3.
>
> Background1
>
> Adding and removing transactions and searching for the*nonce* when mining blocks are all computationally intensive activities that prevent the miner from receiving new transactions and blocks. I.e., if the miner is very busy, it will become unresponsive causing other hosts in the network to wait until it can receive their broadcasts. This is not optimal. Ideally, the miner should be able to receive new transactions and blocks at anytime and process them later, when it becomes free.
>
> Problem Statement
>
> Extend your program from Assignment 3 (or the provided solution) to make the **main** thread of your miner spawn a **reader** thread that is responsible for reading all the input. The **reader** thread should then insert the input into a queue (buffer). The **main** thread will be responsible for dequeuing the input and pro- cessing it, just like in Assignment 3. This is essentially the Unbounded Buffer Producer-Consumer problem where the **reader** thread is the *producer*, and the **main** thread is the *consumer.* Your program must be compiled to an executable called **miner**. The program will read in five events, which are the same as in Assignment 3*.* Please see the Problem Statements in Assignment 1, 2 and 3 for a description of the events.
>
> The **reader** thread should consist of a loop that reads events from **stdin** and enqueues them onto an unbounded queue. The queue can never fill up, so a linked-list implementation is recommended.
>
> The **main** thread will use the same main loop as in Assignment 3, except that instead of reading from **stdin** it should dequeue events from the queue fed by the **reader** thread and process the events. Please note that if the queue is empty, the **main** thread should block until more events are added by the **reader** thread.
>
> 1 This background description assumes that you have read and understood the background of previous Assignments.
>
> Input
>
> Your program reads its input from **stdin**. The input consists of events described in previous assignments.
>
> Processing
>
> All events are processed in the same way as in Assignment 3. The only difference in processing is how the events are read in. A separate **reader** thread, which is spawned at the start of execution, should be the only thread reading from **stdin.** The **reader** should read in the events and insert them into a shared queue. The **reader** thread must never block. I.e., the queue is unbounded. If the **reader** thread receives the **end** event, it should leave its loop and end after it has inserted the event into the queue.
>
> The **main** thread should dequeue events from the shared queue. If the queue is empty, the **main** thread should be blocked (suspended) until the queue is not empty. Once the **main** thread is resumed, it pro- cesses the event in the same manner as in Assignment 3.
>
> Output
>
> The output for this assignment is the same as that of Assignment 3, except that when the **reader** thread inserts an event into the queue, it should printout one of two messages.
>
> • If the event is a **block** or **transaction**, it should printout

[TABLE]

> where ***E*** is either BLK or TRX and ***X*** is the identifier of the block or transaction.
>
> • If the event **end**, **epoch**, or **mine**, it should printout

[TABLE]

> where ***E*** is either END, EPOCH, or MINE.
>
> Example:

[TABLE]

> Note that the **Received** statements may be interleaved with the output in a different order for each run because they are being produced by a different thread.
>
> Assignment Submission
>
> Submission and testing are done using Git, Gitlab, and Gitlab CI/CD. You can submit as many times as you wish, up to the deadline. Everytime a submission occurs, functional tests are executed, and you can view the results of the tests. To submit use the same procedure as Assignments 1, 2, and 3 .
>
> Hints and Suggestions
>
> • The queue is shared and is a critical section.
>
> • The queue is unbounded and should be implemented with a linked list.
>
> • The **main** thread should block (be suspended) if the queue is empty. It should **not** spin! You will need to use locks to protect critical sections in your program.
>
> • Using pthread’s condition variables is an easy way to block the consumer if the queue is empty.
>
> • To make things simpler, the solution places the reader code into a separate file (reader.c) and uses aseparate file (event_q.c) for the multithreaded queue implementation.
>
> Grading
>
> The assignment will be graded based on three criteria:
>
> **Functionality**: “Does it work according to specifications?”. This is determined in an automated fashion by running your program on a number of inputs and ensuring that the outputs match the expected outputs. The score is determined based on the number of tests that your program passes. So, if your program passes t/T tests, you will receive that proportion of the marks.
>
> **Quality of Solution**: “Is it a good solution?” This considers whether the approach and algorithm in your solution is correct. This is determined by visual inspection of the code. It is possible to get a good grade on this part even if you have bugs that cause your code to fail some of the tests.
>
> **Code Clarity**: “Is it well written?” This considers whether the solution is properly formatted, well docu- mented, and follows coding style guidelines. A single overall mark will be assigned for clarity. Please see the Style Guide in the Assignment section of the course in Brightspace.
>
> **If your program does not compile, it is considered non-functional and of extremely poor quality, mean- ing you will receive 0 for the solution.**
>
> The following grading scheme will be used:

[TABLE]
