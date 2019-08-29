# top Status bar explained

what does the color indicts in its status bar?

According to the manual, State means:

- __S__ for sleeping, idle
- __R__ for running
- __D__ for disk sleep (uninterruptible)
- __Z__ for zombie (waiting for parent to read its exit status)
- __T__ for traced or suspended
- __W__ for paging



CPU usage bar : 

- blue for __low priority__
- green for normal
- red for __kernel__



What is kernel threads?

The normal way of implementing threads nowadays is to do it in the kernel, so those can be considered "normal" threads. It's however also possible to do it in userland, using signals such as SIGALRM, whose handler will save the current process state (registers, mostly) and change them to another one previously saved. Several OSes used this as a way to implement threads before they got proper kernel thread support. They can be faster, since you don't have to go into kernel mode, but in practice they've faded away.

There's also cooperative userland threads, where one thread runs until it calls a special function (usually called yield), which then switches to another thread in a similar way as with SIGALRM above. The advantage here is that the program is in total control, which can be useful when you have timing concerns (a game for example). You also don't have to care much about thread safety. The big disadvantage is that only one thread can run at a time, and therefore this method is also uncommon now that processors have multiple cores.

Kernel threads are implemented in the kernel. Perhaps you meant how to use them? The most common way is to call `pthread_create`.