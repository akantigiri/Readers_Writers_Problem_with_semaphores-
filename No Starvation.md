We call this as Third Readers-Writers problem. The solution implied by both first and second reader-writer problem ca result in starvation. Like the first problem might starve writers in the queue and the second one might starve readers in the queue. This problem requires that no thread should be allowed to starve which means that operation of obtaining a lock on the shared data will always terminate in a bounded amount of time.

Semaphores and variables used:
```
// All semaphores are intialized to 1
semaphore enter;          //This semaphore is used to check which process is going to enter critical section.
semaphore mutex;         // This semaphore is used for mutual exculsion in reading processes while updating read_count.
semaphore rwMutex;     // This semaphore is used for mutual exclusion between two writing processes.
int readCount=0;       // This semaphore is used to count no of reading process

```
Structure of writer process:
```
do{
wait(enter);            //Lock enter semaphore to prevent reader process from reading
wait(rwMutex);          //Lock rwMutex to prevent other writing processes from writing
... 
...
//Writing is done here
...
...
//After writing release the semaphores resource access for next reader/writer.
signal(rwMutex);
signal(enter);
}while(true);
```
Structure of reader process:
```
do{
wait(enter);           //Wait if there are any writers using enter. 
wait(mutex);          //Lock mutex to update readCount 
readCount++;
if(readCount==1){      //if it is the first reader lock rwMutex to prevent writers from writing.
wait(rwMutex);}
signal(mutex);         //Release enter and mutex 
signal(enter);
...
...
//Reading is done here
...
...
wait(mutex);          //lock mutex to update readCount
readCount--;
if(readCount==0){       //if it is last reading process release rwMutex to allow other writers to write
signal(rwMutex);
}
signal(mutex);
}while(true);
```
 This solution for third Readers-Writers problem will only satisfy the condition that no thread shall be allowed to starve iff semaphores preserve first-in first-out ordering when blocking and releasing threads. If else a blocked writer may remain blocked indefinitely with a cycle of other writers decrementing the semaphore before it can and it is similar with that of readers.


