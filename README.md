Download Link: https://assignmentchef.com/product/solved-cnt4714-project-2
<br>
<strong> </strong><strong>Title:</strong>  “Project 2:  An Application Employing Synchronized/Cooperating Multiple Threads In Java Using Locks – A Banking Simulator”

<strong>Objectives:</strong>  To practice programming cooperating, synchronized multiple threads of execution.

<strong>Description:</strong>  In this programming assignment you will simulate the deposits and withdrawals made to a fictitious bank account (I’ll let you use my real bank account if you promise to make only deposits! J).  In this case the deposits and withdrawals will be made by synchronized threads.  Synchronization is required for two reasons – (1) mutual exclusion (updates cannot be lost) and (2) because a withdrawal cannot occur if the amount of the withdrawal request is greater than the current balance in the account.  This means that access to the account (the shared object) must be synchronized.  This application requires cooperation and communication amongst the various threads (cooperating synchronized threads).  (In other words, this problem is similar to the producer/consumer problem where there is more than one producer and more than one consumer process active simultaneously.)  If a withdrawal thread attempts to withdraw an amount greater than the current balance in the account – then it must block itself and wait until a deposit has occurred before it can try again.  As we covered in the lecture notes, this will require that the deposit threads signal all waiting withdrawal threads whenever a deposit is completed.




<ol>

 <li>To keep things relatively simple, as well as to see immediate results from a series of transactions (deposits and withdrawals), assume that deposits are made in amounts ranging from $1 to $250 (whole dollars only) and withdrawals are made in amounts ranging from $1 to $50 (again, whole dollars only).</li>

</ol>




<ol start="2">

 <li>You should have four deposit threads and eight withdrawal threads simultaneously executing.</li>

</ol>




<ol start="3">

 <li>Once a deposit thread has executed, put it to sleep for few milliseconds (randomly generate this number – don’t use a constant sleep time) or so (depends a little bit on the speed of your system as to how long you will want to sleep the depositor threads – basically we want to ensure a lot more withdrawals than deposits) to allow other threads to execute. This is the only situation in which a deposit thread will block.</li>

</ol>




<ol start="4">

 <li>For withdrawal threads, things will be a bit different depending on whether you are working on a single or multi-core processor.</li>

</ol>




<ol>

 <li>For single core processors, once a withdrawal thread has executed, have it yield to another thread. Since the thread is giving up the processor voluntarily, it will be unlikely to run again (attempt a second withdrawal in a row), before another thread runs.  Note however, that it does not prevent it from running again, if all other withdrawal threads are blocked and all depositors are sleeping, it will run again.</li>

 <li>For multi-core processors, once a withdrawal thread has executed, have it sleep for some random period of time (again, a few milliseconds should be fine). Depending on which core a thread is executing, yielding the CPU won’t ensure that the same thread will not run again immediately.  While, sleeping the thread will also not ensure that it will not run two or more times in succession, it is less likely to do so in the multi-core environment.</li>

 <li>What we don’t want to happen is a single withdrawal thread gaining the CPU and then executing a long sequence of withdrawal operations. Recall though that withdrawal threads block if they attempt to withdraw more than the current balance in the account.</li>

 <li>Similarly, we don’t want depositor threads monopolizing the CPU either and causing the balance in the account to grow continuously. This would most likely occur when the withdrawal threads are sleeping too long in comparison to the average sleep time of the deposit threads.  See page 7 for an illustration of this.</li>

</ol>




<ol start="5">

 <li>Assume all threads have the same priority. Do not give different priority to depositor and withdrawal threads.</li>

</ol>




<ol start="6">

 <li>The output from your program must look reasonably similar to the sample output shown below.</li>

</ol>




<ol start="7">

 <li><strong>Do not</strong> <strong>put the threads into a counted loop for your simulation.</strong> In other words, the run() method should be an infinite loop.  Just stop the simulation from your IDE after a few seconds.</li>

</ol>




<ol start="8">

 <li><strong>Do not</strong> <strong>use the Java synchronized statement.</strong> I want you to handle the locking and signaling yourself.  No monitors!</li>

</ol>




<ol start="9">

 <li>You must utilize a reentrant lock from the java.util.concurrent.locks package for implementing your locking protocols. We will specify no fairness policy for this application. Do not create your own lock using a Boolean or any other type of variable.</li>

</ol>




<strong> </strong>

<strong>References:  </strong>

Notes:  Lecture Notes for Multithreaded Applications.




<strong>Restrictions: </strong>

Your source files shall begin with comments containing the following information:

<strong> </strong>

<strong>/*  Name:   </strong>

<strong>     Course: CNT 4714 Fall 2019 </strong>

<strong>     Assignment title: Project 2 – Synchronized, Cooperating Threads Under Locking      Due Date: October 6, 2019 </strong>

<h1>*/</h1>

<strong>Input Specification:</strong>  Internal to the program.




<strong>Output Specification:  </strong>Console based.  Your output should appear reasonably

similar to the output shown below.




<strong>Deliverables: </strong>

<ul>

 <li>Zip up all of your .java files and submit them via WebCourses no later than 11:59pm Sunday October 6, 2019.</li>

</ul>




<ul>

 <li>Include at least one screen shot which illustrates the execution of your synchronized threaded application. See below for some representative examples.  You can either do a screen shot of the console window like I did below or redirect your output to a file and take a screen shot from an editor.</li>

</ul>




<strong>Additional Information:</strong>




Shown below are three example screen shots of the output from this program to help illustrate how your application is to operate and display the results.  The last page illustrates execution runs that you do not want to produce.

We don’t want to see this sort of scenario where the depositors are monopolizing the account.  Indication is the depositor threads aren’t sleeping long enough.