#简介

##什么是Docker
Docker是一个开源项目，诞生于2013年初，最初是dotCloud公司内部的一个业余项目。它基于Google公司推出的Go语言实现。
项目后来加入了Linux基金会，遵从了Apache 2.0协议，项目代码在[GitHub](https://github.com/docker/docker)上进行维护。

Docker自开源后受到广泛的关注和讨论，以至于dotCloud公司后来都改名为Docker Inc。Redhat已经在其RHEL6.5中集中支持Docker；Google也在其PaaS产品中广泛应用。

Docker项目的目标是实现轻量级的操作系统虚拟化解决方案。

Docker的基础是Linux的容器技术（LXC）。

我们知道，传统的虚拟机通过在宿主主机中运行hypervisor来模拟一整套完整的硬件环境提供给虚拟机的操作系统。虚拟机系统看到的环境是可限制的，也是彼此隔离的。
这种直接的做法实现了对资源最完整的封装，但很多时候往往意味着系统资源的浪费。
例如，以宿主机和虚拟机系统都为Linux系统为例，虚拟机中运行的应用其实可以利用宿主机系统中的运行环境。

我们知道，在操作系统中，包括内核、文件系统、网络、PID、UID、IPC、内存、硬盘、CPU等等，所有的资源都是应用进程直接共享的。
要想实现虚拟化，除了要实现对内存、CPU、网络IO、硬盘IO、存储空间等的限制外，还要实现文件系统、网络、PID、UID、IPC等等的相互隔离。
前者相对容易实现一些，后者则需要宿主机系统的深入支持。

随着Linux系统对于名字空间功能的完善实现，程序员已经可以实现上面的所有需求，让某些进程在彼此隔离的名字空间中运行。大家虽然都共用一个内核和某些运行时环境（例如一些系统命令和系统库），但是彼此却看不到，都以为系统中只有自己的存在。这种机制就是容器（Container），例如名字空间来做权限的隔离控制，利用cgroups来做资源分配。


而Docker，正是在容器的基础上进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作Docker的容器就像操作一个快速轻量级的虚拟机一样简单。

下面的图片比较了Docker和传统虚拟化方式的不同之处，可见容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，而传统方式则是在硬件层面实现。

![传统虚拟化](../_images/virtualization.png)

![Docker](../_images/docker.png)


##为什么要使用docker？
作为一种新兴的虚拟化方式，Docker跟传统的虚拟化方式相比具有众多的优势。

首先，Docker容器的启动可以在秒级实现，这相比传统的虚拟机方式要快得多。

其次，Docker对系统资源的利用率很高，一台主机上可以同时运行数千个Docker容器。

而且容器除了运行其中应用外，基本不消耗额外的系统资源，使得应用的性能很高，同时系统的开销尽量小。
