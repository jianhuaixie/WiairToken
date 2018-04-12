# <center>IPFS系统</center>

### 安装

	tar -zxvf go-ipfs_v0.4.10_linux-amd64.tar.gz
	cd  go-ipfs
	sudo ./install.sh
	

### 基本命令

- ipfs init

  initialize ipfs local configuration

- ipfs add -r .
	
  add a file to IPFS

- ipfs cat QmZne3Uwu2urGCg84BsnwmX4CuyM6cFwka15ppdG1xCq1m > image.jpg

 show IPFS object data

- ipfs get 

  download IPFS objects

- ipfs ls

  list links from an object

- ipfs refs 

  list hashes of links from an object

### 数据结构命令

- ipfs block

  interact with raw blocks in the datastore

- ipfs object

  interact with raw dag nodes

- ipfs files

  interact with objects as if they were a unix filesystem

- ipfs dag

  interact with IPLD documents

### 高级命令

- ipfs daemon

  start a long-running daemon process

- ipfs mount 

  mount an IPFS read-only mountpoint

- ipfs resolve

  resolve any type of name

- ipfs name

  publish and resolve IPNS names

- ipfs key

  create and list IPNS name keypairs

- ipfs dns

  resolve DNS links

- ipfs pin

  pin objects to local storage

- ipfs repo

  manipulate the IPFS repository

- ipfs stats

  various operational stats

- ipfs p2p

  libp2p stream mounting

- ipfs filestore

  manage the filestore

### 网络命令

- ipfs id

  show info about IPFS peers

- ipfs bootstrap

  add or remove bootstrap peers

- ipfs swarm

  manage connections to the p2p network

- ipfs dht

  query the DHT for values or peers

- ipfs ping 

  measure the latency of a connection

- ipfs diag

  print diagnostics

#### blocks

ipfs add命令来创建一个Merkle DAG。其会遵循'unixfs data format'，将数据切分成一个个blocks，按照一棵树的结构用'link nodes'将blocks重新组织起来。一个文件的hash值实际上在DAG上根节点的hash值。对于一个DAG，能够通过命令ipfs ls来轻易查看其sub-blocks。

	ipfs add exampledir
	ipfs ls thathash

	ipfs block get someblockhash :to see just the data of a given block and not its children

	ipfs block stat someblockhash :will tell you the exact size of a given block(without its children)
	ipfs refs someblockhash :will tell you all the children of that block
	ipfs ls someblockhash / ipfs object links someblock hash : will show you all children and their sizes
	
######## blocks 和 objects的区别

In IPFS, a block refers to a single unit of data, identified by its key (hash). A block can be any sort of data, and does not necessarily have any sort of format associated with it. An object, on the other hand, refers to a block that follows the Merkle DAG protobuf data format. 


#### swarm

'ipfs swarm' 就是一个操作网络群的工具，网络群是一个什么概念呢？The swarm is the componet that opens,listens for, and maintains connections to other ipfs peers in the internet.

其命令如下：

- ipfs swarm addrs:list known addresses.Useful for debugging
- ipfs swarm connect <address>...:open connection to a given address
- ipfs swarm disconnect <address>...:close connection to a given address
- ipfs swarm filters:manipulate address filters
	
	- ipfs swarm filters add <address>...:add an address filter
	- ipfs swarm filters rm <address>...:remove an address filter
- ipfs swarm peers:list peers with open connections

	- ipfs swarm peers -v: --verbose:display all extra information
	- ipfs swarm peers --also streams:list information about open streams for each peer
	- ipfs swarm peers --also latency:list information about latency to each peer


#### pinning

pinning是IPFS一个重要的概念,IPFS尽量尝试让文件存储在本地一样，不需要从远处服务端拉取过来。IPFS有一个相当激进的缓存机制来使得对象在一个非常短的时间内本地化，不管你对这个对象实行何种操作。但是需要定时的不断来收集这些对象垃圾。为了阻止垃圾回收简单的定位成你管关注的hash，对象通过ipfs add添加的时候是默认通过pinned recursively的方式。

在IPFS世界里，有三种pins方式：

- direct pins:which pin just a single block
- recursive pins:which pin a given block and all of its children
- indirect pins:the result of a given blocks parent being pinned recursively

a pinned object cannnot be garbage collected

	ipfs add foo
	ipfs repo gc
	ipfs cat <foo hash>

but if foo were to somehow become unpinned

	ipfs pin rm <foo hash>
	ipfs repo gc
	ipfs cat <foo hash>


#### Service

 IPFS有一些默认跑的服务，比如dht，bitswap和diagnostics service。每一个读都会在IPFS PeerHost简单注册一个handler,并且监听新的连接。

 为什么要用这个服务？

 - you dial a specific peerID,no matter what their IP address happens to be at the moment
 - you take advantage of the NAT traversal built into our net package
 - instead of a 'port' number,you get a much more meaningful protocol ID string


#### snapshots

	ipfs add -r .
	echo $hash `date` >> snapshots
	// or all at once
	echo `ipfs add -q -r . | tail -n1` `date` >> snapshots
	
make sure to have the placeholders for the mount points

	sudo mkdir /ipfs /ipns
	sudo chown `whoami` /ipfs /ipns

you will need to have Fuse installed in order to be able to mount directories from the ipfs.

	ipfs mount
	ls /ipfs/$hash
	cd /ipfs/$hash

#### The Inter-Planetary Naming System

updating an ipns entry can "break links" because anything referencing an ipns entry might no longer point to the content it expected.

ipns links should be used carefully if you want to ensure permanence. 



