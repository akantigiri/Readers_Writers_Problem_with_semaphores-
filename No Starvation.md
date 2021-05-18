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
wait(enter);
wait(rwMutex);
...
...
//Writing is done here
...
...
signal(rwMutex);
signal(enter);
}while(true);
```
Structure of reader process:
```
do{
wait(enter);
wait(mutex);
readCount++;
if(readCount==1){
wait(rwMutex);}
signal(mutex);
signal(enter);
...
...
//Reading is done here
...
...
wait(mutex);
readCount--;
if(readCount==0){
signal(rwMutex);
}
signal(mutex);
}while(true);
```



