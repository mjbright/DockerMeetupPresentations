name: title_inversed_whiteText
layout: false
class: center, middle

![](images/unikernel.org.png)
## The next big little thing ?
<!-- ## Unikernels: The next big little thing ?
     #### C'est quoi les Unikernels ?
-->
<!-- ![](images/logo-tmux.svg) -->

### Docker Grenoble Meetup, 19 Jan 2017
<h3> Mike Bright, <img src="images/Twitter_Bird.svg" width=24 /> @mjbright </h3>

.left[.footnote[.vlightgray[ @mjbright ]]]

???
SpeakerNotes:

Introduce ourselves.

Why this presentation?

---
name: section_raison
layout: false
class: center, middle, inverse

*Viktor Farcic, senior consultant at CloudBees*

...  One of the most exciting areas that will become prominent in 2017 will be unikernels.

While the majority of the industry is still trying to wrap their heads around containers, we will start seeing unikernels taking over the stage.

They will, in a way, unify functionalities provided by VMs and containers.

http://sdtimes.com/whats-horizon-2017/

???
SpeakerNotes:

'''
With the continued rise to domination of the container model led by Docker adoption, we think it's worth calling attention to the continued rapid development in the Unikernel space. Unikernels are single-purpose library operating systems that can be compiled down from high-level languages to run directly on the hypervisors used by commodity cloud platforms. They promise a number of advantages over containers, not least their superfast startup time and very small attack surface area. Many are still at the research-project phase—Drawbridge from Microsoft Research, MirageOS and HaLVM amongst others—but we think the ideas are very interesting and combine nicely with the technique of serverless architecture.
'''

---
name: section_overview
layout: false
class: center, left
## Unikernels - Overview
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
]

.right-column[

- What are Unikernels?

- How did we get here?

- Unikernel implementations
    - Clean Slate
    - POSIX compatible
    - Tools

-  Future

-  Resources
]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_history
layout: false
class: center, left
## .blue[What are Unikernels?] .lightgray["Library OS"]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

Unikernels are applications images built with only the Operating System components they actually require,
e.g. TCP Stack, Disk access.
<img src="images/comparison.png" width=600 />

Single process applications (no threads, forking or multi-user) with very small size
-> high performance, fast boot and small attack surface (secure).


.left[.footnote[.vlightgray[ @mjbright ]]]

???
Speaker Notes:
Contrast
  + Typical application stack
  + Unikernel application stack


---
name: section_history
layout: false
class: center, left
## .blue[What are Unikernels - how did we get here?]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
"Library OSes"
<img src="images/comparison.png" width=160/>
]

.right-column[
<img src="images/comparison-vm-unikernel_stack.png" width=400 />

A Unikernel is built by the compiler linking **only** the OS components needed by the application.

The OS becomes a "**Library OS**"

Unlike *"normal"* applications which sit atop a generic monolithic Linux kernel (or even &mu;-kernel) which has many unneeded features, e.g. floppy driver.

]


---
name: section_history
layout: false
class: center, left
## .blue[What are Unikernels - how did we get here?]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
"Library OSes"
<img src="images/comparison.png" width=160/>
]

.right-column[
Unneeded features consume resources unnecessarily.

Unneeded legacy features represent a security risk - especially in the cloud.

]
--
.right-column[
At October's "*Docker Distributed Summit*", Docker even talked of minimizing the Hypervisor also.

<a href="https://blog.docker.com/2016/10/docker-distributed-system-summit-videos-podcast-episodes/" /> <img src="images/youtube.jpg" width=30  /> "Unikernels The rise of the library hypervisor in MirageOS" </a>

(<a href="https://queue.acm.org/detail.cfm?id=2566628/" > ACM: Unikernels: Rise of the Virtual Library Operating System </a>, Jan 2014)
]

--
.right-column[
These minimal systems can take ~ 200msec to boot.

This opens up the possibility of services being spin up
<br/>*on demand* (MirageOS *jitsu*).
]

---
name: section_history
layout: false
class: center, left
## .blue[Where will Unikernels be used?]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
"Library OSes"
]

.right-column[
Application domains
- Cloud, e.g. serverless

- IoT (Embedded)

- HPC
- NFV (
<a href="https://www.youtube.com/watch?v=3jGClCBXuTg" /> <img src="images/youtube.jpg" width=30  /> Unikernels meet NFV </a> <a href="https://www.ericsson.com/research-blog/sdn/unikernels-meet-nfv/" /> Ericsson Research </a> </a>)
]

--
.right-column[
From the NFV Containers White Paper (2.3. Unikernels):

```
   Unikernels are essentially single-application virtual machines
   based on minimalistic OSes. Such minimalistic OSes have minimum
   overhead and are typically single-address space (so no user/kernel
   space divide and no expensive system calls) and have a
   co-operative scheduler (so reducing context switch costs).

   Examples of such minimalistic OSes are MiniOS [MINIOS] which
   runs on Xen and OSv [OSV] which runs on KVM, Xen and VMWare.
```
<a href="https://datatracker.ietf.org/doc/draft-natarajan-nfvrg-containers-for-nfv/?include_text=1" > https://datatracker.ietf.org/doc/draft-natarajan-nfvrg-containers-for-nfv/?include_text=1 </a>
]

.left[.footnote[.vlightgray[ @mjbright ]]]

???
Why unikernels for industry?

- Resource usage
- Security
- Improved infrastructure flows
- Advanced dev tooling
- Simplicity

---
name: section_families
layout: false
class: center, left
## .blue[Unikernel implementations]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Unikernel Families
]

.right-column[
Many Unikernel implementations exist, there are two main classes of Unikernels
]

--
.right-column[
Some take a clean-slate approach and emphasize safety and security.
These tend to use the same language for the application and the Library OS components.
- MirageOS (Ocaml)
- HalVM (Haskell)
]
--
.right-column[
Others favour backward compatibility of existing applications based on POSIX-compatibility.

Many applications have been ported
- OSv (Tomcat, Jetty, Cassandra, OpenJDK, ...)
- Rumprun (MySQL, PHP, Nginx)
]

???
Speaker Notes:

A number of unikernel open source projects are beginning to take off, each with its own unique focus and approach.
For example, MirageOS and HaLVM take a clean-slate approach and emphasize safety and security;
ClickOS stresses speed;
while OSv and Rump kernels aim for compatibility with existing applications. Both OSv and Rump kernels have made significant progress in porting existing applications: for example MySQL, PHP and Nginx have been ported to Rump Kernels, whereas many applications such as Tomcat, Jetty, Cassandra, OpenJDK and others have been ported to OSv. Meanwhile, MirageOS has demonstrated 1MB unikernels that serve DNS, Git and SSL web traffic with complete type safety down to the device drivers.


.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_families
layout: false
class: center, left
exclude: true
## .blue[Unikernel implementations]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Unikernels
]

.right-column[

Technology | Vendor | Description |
-|:-:|:-:|-
ClickOS | NEC | Unikernel for embedded network h/w.  ~ 5MB images, boots < 20msec, 45 usec delay, 100 VMs => 10Gbps 
Clive | | designed to work in distributed and cloud computing environments, written in the Go programming language.
Drawbridge | MS | Research prototype, little information available. a new form of virtualization for application sandboxing. Process-based picoprocess/container with minimal kernel API surface, and a Windows library OS to run in picoprocess
Graphene | | Linux-compatible library operating system that focuses on securing multi-process, server-type or shell-type legacy applications. Graphene spans a multi-process application across multiple picoprocesses, with inter-process abstractions (e.g., signals, message queues, semaphores) coordinated over simple pipe-like streams. For applications with multiple security principles, Graphene can dynamically sandbox an insecure picoprocess.
HaLVM | | Port of Glasgow Haskell Compiler tool suite that enables developers to write high-level, lightweight VMs that can run directly on the Xen hypervisor.
HermitCore | | Novel unikernel targeting a scalable and predictable runtime behavior for HPC and cloud environments. HermitCore supports C, C++, Fortran, Go, Pthreads, OpenMP and iRCCE[19] as message passing library. It is a research project that extends the multi-kernel approach and combines it with unikernel features. HermitCore can directly run on the KVM hypervisor but also on natively on x86_64 architecture.
IncludeOS | | C++, IncludeOS is a minimal, service oriented, open source, includable library operating system for cloud services. Currently a research project for running C++ code on virtual hardware.
LING | | Unikernel based on the Erlang/OTP and understands .beam files. Developers can create code in Erlang and deploy it as LING unikernels. LING removes the majority of vector files, uses only three external libraries and no OpenSSL.
MirageOS | | Clean-slate library OS for secure, high-performance network applications across a variety of cloud computing and mobile platforms. There are now more than 100 MirageOS libraries[22] and a growing number of compatible libraries within the wider OCaml ecosystem.
OSv | Cloudius Systems | New OS designed specifically for cloud VMs. Able to boot in less than a second, OSv is designed from the ground up to execute a single application on top of any hypervisor, resulting in superior performance, speed and effortless management. Can run unmodified Linux executables (with some limitations), and support for C, C++, JVM, Ruby and Node.js application stacks is available.
Rumprun | FreeBSD? | Software stack which enables running existing unmodified POSIX software as a unikernel. Rumprun supports multiple platforms, from bare ARM hardware to hypervisors such as Xen. It is based on rump kernels which provide free, portable, componentized, kernel quality drivers such as file systems, POSIX system call handlers, PCI device drivers, a SCSI protocol stack, virtio and a TCP/IP stack.[24]
Runtime.js | | Runtime.js is an open-source library operating system for the cloud that runs on JavaScript VM, could be bundled up with an application and deployed as a lightweight and immutable VM image. Runtime.js is built on the V8 Javascript engine and currently supports QEMU/KVM hypervisor.
]

???
Speaker Notes:
ClickOS | a high-performance, virtualized software middle box platform based on open source virtualization. Early performance analysis shows that ClickOS VMs are small (5MB), boot quickly (as little as 20 milliseconds), add little delay (45 microseconds) and more than 100 can be concurrently run while saturating a 10Gb pipe on an inexpensive commodity server.
Clive | Clive[15] is an operating system designed to work in distributed and cloud computing environments, written in the Go programming language.
Drawbridge | Drawbridge is a research prototype of a new form of virtualization for application sandboxing. Drawbridge combines two core technologies: a picoprocess, which is a process-based isolation container with a minimal kernel API surface, and a library OS, which is a version of Windows enlightened to run efficiently within a picoprocess.[16]
Graphene | Graphene[5][17] is a Linux-compatible library operating system that focuses on securing multi-process, server-type or shell-type legacy applications. Graphene spans a multi-process application across multiple picoprocesses, with inter-process abstractions (e.g., signals, message queues, semaphores) coordinated over simple pipe-like streams. For applications with multiple security principles, Graphene can dynamically sandbox an insecure picoprocess.
HaLVM | The Haskell Lightweight Virtual Machine (HaLVM) is a port of the Glasgow Haskell Compiler tool suite that enables developers to write high-level, lightweight VMs that can run directly on the Xen hypervisor.
HermitCore | HermitCore[18] is a novel unikernel targeting a scalable and predictable runtime behavior for HPC and cloud environments. HermitCore supports C, C++, Fortran, Go, Pthreads, OpenMP and iRCCE[19] as message passing library. It is a research project that extends the multi-kernel approach and combines it with unikernel features. HermitCore can directly run on the KVM hypervisor but also on natively on x86_64 architecture.
IncludeOS | IncludeOS is a minimal, service oriented, open source, includable library operating system for cloud services. Currently a research project for running C++ code on virtual hardware.
LING | LING[20] is a unikernel based on the Erlang/OTP and understands .beam files. Developers can create code in Erlang and deploy it as LING unikernels. LING removes the majority of vector files, uses only three external libraries and no OpenSSL.
MirageOS | MirageOS[21] is a clean-slate library operating system that constructs unikernels for secure, high-performance network applications across a variety of cloud computing and mobile platforms. There are now more than 100 MirageOS libraries[22] and a growing number of compatible libraries within the wider OCaml ecosystem.
OSv | OSv is a new OS designed specifically for cloud VMs from Cloudius Systems.[23] Able to boot in less than a second, OSv is designed from the ground up to execute a single application on top of any hypervisor, resulting in superior performance, speed and effortless management. Can run unmodified Linux executables (with some limitations), and support for C, C++, JVM, Ruby and Node.js application stacks is available.
Rumprun | Rumprun is a software stack which enables running existing unmodified POSIX software as a unikernel. Rumprun supports multiple platforms, from bare ARM hardware to hypervisors such as Xen. It is based on rump kernels which provide free, portable, componentized, kernel quality drivers such as file systems, POSIX system call handlers, PCI device drivers, a SCSI protocol stack, virtio and a TCP/IP stack.[24]
Runtime.js | Runtime.js is an open-source library operating system for the cloud that runs on JavaScript VM, could be bundled up with an application and deployed as a lightweight and immutable VM image. Runtime.js is built on the V8 Javascript engine and currently supports QEMU/KVM hypervisor.

---
name: section_families
layout: false
class: center, left
## .blue[Unikernel Implementations]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

Technology | Description |
-|:-|:-|-
ClickOS <a href="http://cnp.neclab.eu"> cnp.neclab.eu </a> | For embedded network h/w.<br/>~5MB images, boots <20ms, 45 &mu;s delay, 100 VMs => 10Gbps 
 | | |
Clive<br/><a href="http://lsub.org/ls/clive.html"> lsub.org</a> | Written in Go.  For distributed and cloud.
 | | |
Drawbridge<br/><a href="https://www.microsoft.com/en-us/research/project/drawbridge/"> MS </a> | Research prototype. Picoprocess/container with minimal kernel API surface, and Windows library OS.
 | | |
Graphene <a href="http://graphene.cs.stonybrook.edu/"> graphene</a> | Securing "*multi-process*" legacy apps - adds IPC.
 | | |
HaLVM <a href="galois.com"> galois.com </a> | Port of GHC (Glasgow Haskell Compiler) suite.<br/> Write apps in Haskell to run on Xen.
 | | |
IncludeOS <a href="http://www.includeos.org/"> includeos.org </a> | Research project for C++ code on virtual hardware.
 | | |
LING <a href="http://erlangonxen.org/"> erlangonxen.org </a> | Erlang/OTP runs on Xen.
 | | |
MirageOS <a href="https://mirage.io/"> mirage.io </a> | Clean-slate library OS for secure, high-perf network apps.  More than 100 MirageOS libraries plus OCaml ecosystem.
 | | |
OSv <a href="http://osv.io/"> osv.io </a> Cloudius | Run Linux binaries (w. limitations), supports C/C++, JVM, Ruby, Node.js
 | | |
Rumprun <a href="http://rumpkernel.org/"> rumpkernel.org </a> | FreeBSD - Runs POSIX s/w on BM or VM (Xen).
 | | |
Runtime.js <a href="http://runtimejs.org/"> runtimejs.org </a> | For cloud, JavaScript V8, lightweight immutable VM image runs on Qemu/KVM.

---
name: section_mirageos
layout: false
class: center, left
## .blue[Unikernel implementations - MirageOS]/Ocaml
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Clean-Slate
<br/>
<br/>
<img src="images/mirageos.png" width=80 />
<br/>
<a href="https://mirage.io/" >  https://mirage.io/ </a>

OCaml-Based
<img src="images/ocaml.jpg" width=80 />
]

.right-column[

MirageOS "Library OS" components are written in <a href="https://en.wikipedia.org/wiki/OCaml"> Ocaml </a>.

ML-derived languages are best known for their static type systems and type-inferring compilers.

OCaml unifies functional, imperative, and object-oriented programming under an ML-like type system.

OCaml has extensive libraries available

(Unison utility)
]

---
name: section_mirageos
layout: false
class: center, left
## .blue[Unikernel implementations - MirageOS]-2
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Clean-Slate
<br/>
<br/>
<img src="images/mirageos.png" width=80 />
<br/>
<a href="https://mirage.io/" >  https://mirage.io/ </a>

OCaml-Based
<img src="images/ocaml.jpg" width=80 />
]

.right-column[
MirageOS Unikernels are based on the Mirage-OS Unikernel base (OS library).

The mirage tool is used to build Unikernels for various backends:
- Xen Hypervisor (PV)
- Unix (Linux or OS/X binaries)
- Browser (via Ocaml->JS compiler !!)
- Even an experimental BM backend for Raspberry Pi
]

--
.right-column[
Building applications for unix or xen
```
mirage configure -t unix
make
./mir-console
```

```
mirage configure -t xen
make
****xen create ./mir-console.xen
```

]

.left[.footnote[.vlightgray[ @mjbright ]]]

???
Speaker Notes:

See sources:
    /home/mjb/src/git/Unikernels/mirage-skeleton/hello
ean Grove - From Unikernels to Databases to UIs: Truly full-stack apps in OCaml - Curry On
Sean Grove - From Unikernels to Databases to UIs: Truly full-stack apps in OCaml - Curry On
      https://www.youtube.com/watch?v=QWfHrbSqnB0

---
name: section_mirageos
layout: false
class: center, left
## .blue[Unikernel implementations - MirageOS - Use Cases]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Clean-Slate
<br/>
<br/>
<img src="images/mirageos.png" width=80 />
<br/>
<a href="https://mirage.io/" >  https://mirage.io/ </a>
]

.right-column[
- <div> BNC Pinata: http://ownme.ipredator.se/ <img src="images/pinata.svg" width=100 /> </div>

- Networking applications
    - e.g. CyberChaff  "false network hosts"

- PayGarden, Sean Grove
  <br/><a href="https://www.youtube.com/watch?v=i9eu9e7gN0Q" /> <img src="images/youtube.jpg" width=30  /> "Baby steps to unikernels in production" </a>
    - Too painful to create/configure AMI images on AWS
    - Solo5 allows to create KVM images deployable on GCE

]

.left[.footnote[.vlightgray[ @mjbright ]]]

???
Speaker Notes:

For me:
<a href="https://eventil.com/users/sgrove" /> sgrove </a>
<a href="https://github.com/ocamllabs/icfp2016-blog/blob/master/CUFP/baby-steps-to-unikernels-in-pr.md" /> Blog notes </a>


---
name: section_halvm
layout: false
class: center, left
## .blue[Unikernel implementations - HalVM]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Clean-Slate
<br/>
<img src="images/halvm.jpg" width=80 />
<br/>
<img src="images/haskell-logo.jpg" width=80 />
]

.right-column[
HalVM - The Haskell Lightweight Virtual Machine: GHC running on Xen
- https://github.com/GaloisInc/HaLVM

- <a href="https://github.com/GaloisInc/HaLVM/tree/halvm3"> HalVM3 </a> is reconsidering it's Unikernel base
    http://uhsure.com/halvm3.html
    - Use rumpkernel (NetBSD base)
    - Shift to Solo5?

]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_osv
layout: false
class: center, left
## .blue[Unikernel implementations - OSv]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
POSIX-based
<img src="images/osv.jpg" width=80 />
<a href="http://osv.io/" > http://osv.io </a>
<a href="http://blog.osv.io/" > http://blog.osv.io </a>
]

.right-column[
OSv - Capable of running POSIX binaries
- can run JVM
- Cassandra: https://www.penninkhof.com/2015/05/minimalist-cassandra-vm-using-osv/
- Used in Mikelangelo (EU Project)
The MIKELANGELO project aims to bring High Performance Computing (HPC) to the cloud. HPC traditionally involves bleeding edge technologies, including lots of CPU cores, Infiniband interconnects between nodes, MPI libraries for message passing, and, surprise—NFS, a very old timer of the UNIX universe.

- Building OSv Images Using Docker: http://blog.osv.io/blog/blog/2015/04/27/docker/

- SDI: ODL + OSv: http://blog.osv.io/blog/blog/2015/03/31/sdi/


]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_tools
layout: false
class: center, left
## .blue[Unikernel Tools]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Tools
]

.right-column[
- <a href="https://github.com/emc-advanced-dev/unik"> Unik </a>: tool for compiling apps to unikernels (various technologies)

- <a href="https://developer.ibm.com/open/openprojects/solo5-unikernel/"> Solo5 </a>: An alternative unikernel-base for MirageOS 
    - Provides qemu/KVM support for MirageOS

- ukvm: An alternative VM Monitor
    - a "*library hypervisor*"

- <a href="http://osv.io/capstan/"> capstan </a>: OSv build tool

]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_tools
layout: false
class: center, left
## .blue[Unikernel Tools]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Clean-Slate
<img src="images/mirageos.png" width=80 />
]

.right-column[

<a href="https://github.com/mirage/jitsu" > MirageOS *jitsu* </a> : "Just-In-Time Summoning of Unikernels"

A DNS server that starts unikernels on demand.

![](images/jitsu.jpg)

Tested with MirageOS and Rumprun unikernels.

<a href="https://github.com/mirage/jitsu"> https://github.com/mirage/jitsu </a>

]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_docker
layout: false
class: center, left
## .blue[Unikernels and Containers]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left-column[
Unikernels or
Containers?
]

.right-column[
So what has this got to do with Containers?

Why did Docker buy Unikernel Systems (Jan 2016)?

<a href="https://www.infoq.com/interviews/chaudhry-unikernels-docker" /> Info.Q / Amir, Aug 2016 </a>

]

--
.right-column[
- Unikernel Systems are involved in MirageOS/Xen
- Use of Unikernels in Docker for Mac
    - VPNKit, DataKit
- To provide build/run/ship tools for Unikernels?
- To secure Container deployments
    - Running Unikernels in containers????
    - Secure front-ends in hybrid solutions made of unikernels and containers
        - e.g. for OCaml MediaWiki (http2https, tls, ...)
]

.left[.footnote[.vlightgray[ @mjbright ]]]

???
Speaker Notes:

```
So yes, it's right. I'm still working on Unikernels. I'm very happy today. So one of the things that's important to think about is that essentially where do Unikernels and containers sit? We see them as sitting on the same continuum and that continuum is one of specialization, some degree of isolation. So containers is something you can use to help package up your application and share a kernel across the containers. And that makes it easy for me to develop essentially a great application and deploy it. But you can think about the progression from that, from a full traditional OS to containerized applications and what comes next, what is further along on that spectrum of specialization. And that's where Unikernels sit. 

So it's like an extreme form of specialization which is something we have already talked about for many years. So you essentially take the components that you need, your application, the components you need, compile that down into an image that you can deploy. So given these things are all on the same continuum, it just made sense that the same tooling should work for all of them. So that's why it makes sense for Unikernel Systems and Docker, Unikernels themselves and containers to work together.
```

---
name: section_subsecn
layout: false
class: center, middle, inverse
## Demo


???
  <img src=images/demo.png width=100 /><br/>

SpeakerNotes:
#### - <a href="https://github.com/xxx/xxx"/> xxx </a> [xx yy]

---
layout: false
class: center, left

## Resources

|   | |    |
|---|---|----|
| <img src="images/scoopit.png" width=60 /> | Scoop.it<br/>Unikernels| <a href="http://www.scoop.it/t/unikernels"> www.scoop.it/t/unikernels </a> |
| <img src="images/wikipedia.jpg" width=60 /> | Wikipedia| <a href="https://en.wikipedia.org/wiki/Unikernel"> en.wikipedia.org/wiki/Unikernel </a> |
| <img src="images/unikernel.org.png" width=60 /> | unikernels.org| <a href="https://unikernels.org"> unikernels.org </a> |
| <img src="images/mirageos.png" width=60 /> | mirageos.io | <a href="https://mirageos.io"> mirageos.io </a> <br/> <a href="https://mirage.io/docs/papers"> mirage.io/docs/papers </a> |
| <img src="images/book_oreillyfree_unikernel.gif" width=60 /> | OReilly<br/>"Unikernels" | <a href="http://unikernel.org/blog/2016/unikernel-ebook"> Free download </a> |
| <img src="images/Twitter_Bird.svg" width=40 /> | @unikernel| <a href="https://twitter.com/unikernel"> @unikernel </a> |
| <img src="images/github.png" width=40 /> | github.com/ocamllabs | <a href="https://github.com/ocamllabs"> ocamllabs </a> |
| <img src="images/github.png" width=40 /> | github.com/mirage | <a href="https://github.com/mirage"> MirageOS </a> |


                                                                  

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_qa
layout: false
class: center, middle, inverse
## Thank you
## Q&A


???
SpeakerNotes:

  <img src=images/demo.png width=100 /><br/>
#### - <a href="https://github.com/xxx/xxx"/> xxx </a> [xx yy]

