## 进程 && 线程

#### 【Linux Case Study】为什么说，在Linux内核看来进程和线程是没有区别的？

linux内核调度中没有process和thread的概念，调度的基本单位是结构体task_struct。

`task_struct`

```cpp
	pid_t pid; // thread id
	pid_t tgid; // process id
	void *stack; // kernel stack
```

```cpp
union thread_union {
	 #ifndef CONFIG_ARCH_TASK_STRUCT_ON_STACK
          struct task_struct task;
     #endif
     #ifndef CONFIG_THREAD_INFO_IN_TASK
          struct thread_info thread_info;
     #endif
          unsigned long stack[THREAD_SIZE/sizeof(long)];
  };
```

#### 【Linux Case Study】Linux Kernel Scheduler



#### 【Linux Case Study】Linux Process State



#### 【Linux Case Study】Linux Kernel Stack

