This is also called as Second Readers-Writers problem. It has a constraint apart form that of First Readers-Writers problem that no writer once added to queue shall be kept waiting than absolute neccessary. This is also called writers-preference. This results in readers waiting and which ultimately may lead to readers starving.

Semaphores and Variables used:
```
//All semaphores initialised to 1
semaphore rwMutex;           // This semaphore is used for mutual exclusion of reading or writing processes
semaphore readMutex;        //This semaphore is used for mutual exclusion between reading processes. It is used for short duration while updating read_count, not during the reading process itself
semaphore writeMutex;       //This semaphore is used for mutual exclusion between writing processes. It is used for a short duration while updating write_count, not during the writing process itself.
semaphore readTry;          //This semaphore is used by writing processes to lock out reading processes.
int readCount=0;            // This semaphore is used to count number of reading process
int writeCount=0;           // This semaphore is used to count number of writing process   
```
Structure of Writer Process:
```



