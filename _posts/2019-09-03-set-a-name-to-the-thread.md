---
layout: post
title:  "Set Name to Thread For Debug"
---


## method-I
### set the name in the thread's executation logic
```c
#include <thread>
#include <stdio.h>
#include <unistd.h>
#include <pthread.h>

void foo() {
    pthread_t self = pthread_self();
    pthread_setname_np(self, "worker");

    while (1) {
        sleep(1);
    }
}

int main() {
    std::thread th = std::thread(foo);
    th.join();
}
```

## method-II
### set the name of one thread external
```c
#include <thread>
#include <stdio.h>
#include <unistd.h>
#include <pthread.h>

void foo() {
    while (1) {
        sleep(1);
    }
}

int main() {
    std::thread th = std::thread(foo);

    pthread_t self = th.native_handle();
    pthread_setname_np(self, "worker");

    th.join();
}

```
