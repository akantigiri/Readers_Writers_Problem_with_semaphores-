We call this as Third Readers-Writers problem. The solution implied by both first and second reader-writer problem ca result in starvation. Like the first problem might starve writers in the queue and the second one might starve readers in the queue. This problem requires that no thread should be allowed to starve which means that operation of obtaining a lock on the shared data will always terminate in a bounded amount of time.

Structure of writer process:
```
a
```



