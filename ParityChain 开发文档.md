# ParityChain 开发文档

#### parity_enode 查看节点
port是递增的，查看第二个节点的时候，用8181

	curl --data '{"jsonrpc":"2.0","method":"parity_enode","params":[],"id":0}' -H "Content-Type: application/json" -X POST 123.207.239.105:8180

#### parity_addReservedPeer 添加节点
命令行中的RESULT要替换成查看到的节点信息

	curl --data '{"jsonrpc":"2.0","method":"parity_addReservedPeer","params":["enode://RESULT"],"id":0}' -H "Content-Type: application/json" -X POST 123.207.239.105:8540

#### 发送交易

	curl --data '{"jsonrpc":"2.0","method":"personal_sendTransaction","params":[{"from":"0x004ec07d2329997267Ec62b4166639513386F32E","to":"0x00Bd138aBD70e2F00903268F3Db08f2D25677C9e","value":"0xde0b6b3a7640000"}, "user"],"id":0}' -H "Content-Type: application/json" -X POST 123.207.239.105:8180

#### 查看余额

	curl --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x00Bd138aBD70e2F00903268F3Db08f2D25677C9e", "latest"],"id":1}' -H "Content-Type: application/json" -X POST 123.207.239.105:8540

#### 查看coinbase帐号

	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_coinbase","params":[],"id":0}' -H "Content-Type: application/json" -X POST 123.207.239.105:8540

#### 查看帐号列表

	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}' -H "Content-Type: application/json" -X POST 123.207.239.105:8540

#### 查看交易笔数
查看从这个帐号往外发送交易笔数

	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x004ec07d2329997267ec62b4166639513386f32e","latest"],"id":1}' -H "Content-Type: application/json" -X POST 123.207.239.105:8540



### geth console测试

	// geth console 2>>geth.log   //geth console在Buffer过不去
	
	node  //替换成用node测试，能完成下面全部测试
	> var Web3 = require('web3');

	> if(typeof web3 !== 'undefined'){web3 = new Web3(web3.currentProvider);} else {web3 = new Web3(new Web3.providers.HttpProvider("http://123.207.239.105:8540"))}

	> web3.eth.getBlock(4,function(error,result){ if(!error){ console.log(JSON.stringify(result)); } else { console.error(error); } })

	
##### 批操作

	> var batch = web3.createBatch();
	> batch.add(web3.eth.getBalance.request('0x00a644704410cc2dcA34bC42cA1a2654cC9AB5FD', 'latest', callback));
	> batch.add(web3.eth.getBalance.request('0x00Bd138aBD70e2F00903268F3Db08f2D25677C9e', 'latest', callback));
	> batch.execute();


##### 哈希操作

	// the string to hash using the Keccak-256 SHA3 algorithm
	> var hash = web3.sha3("jianhuaixie");
	
	// set encoding to hex if the string to hash is encoded in hex. A leading 0x will be automatically ignored.
	> var hashOfHash = web3.sha3(hash,{encoding:'hex'});
	
	// return the hex string of mixed
	> var str = web3.toHex({test: 'test'});

	// return an ascii string made from the given hexString
	> web3.toAscii("0x7b2274657374223a2274657374227d")

	// return the converted HEX string. 32 (optional) meaing the number of bytes the returned HEX string should have
	> web3.fromAscii('etherem',32); 

	// return the number representing the data hexString
	> web3.toDecimal('0x15');

	// return the HEX string representing of the given number
	> web3.fromDecimal('21');

##### 数值转换操作

	// converts a number of wei into the following ethereum units.
	// 以太坊最小的单位是wei，往上还有很多单位，说实在的搞这么多单位，还不如把TPS做上去点，烦人。
	//Gwei,Kwei,Mwei,ether,finney,kether,microether,mei,noehter,picoether,szabo,tether,wei
	> web3.fromWei('21000000000000', 'finney');
	
	// converts an etherem unit into wei
	>  web3.toWei('1', 'ether');

	// converts a given number into a BigNumber instance
	> web3.toBigNumber('200000000000000000000001');

	// checks if the given string is a valid address format
	> web3.isAddress("0x8888f1f195afa192cfee860698584c030f4c9db1");

##### 网络操作

	// listening for network connections or not
	> web3.net.listening
	// returns the number of connected peers
	> web3.net.peerCount

##### eth

	> var eth = web3.eth;
	
	// return the number of a block.if return a string:"earliest","latest" or "peding".the words representing the different meaning.the "earliest":the genesis block,"latest":the latest block(current head of the blockchain),"pending":the currently mined block(including pending transactions)
	> web3.eth.defaultBlock

	// returns the number of hashes per second that the node is mining with.
	> web3.eth.hashrate

	// returns the current gas price,the gas price is determined by the x latest blocks median gas price.
	> web3.eth.gasPrice

	// returns a list of accounts the node controls 
	> web3.eth.personal.getAccounts();

	// returns the current block number
	> web3.eth.blockNumber

	
	// 新建一个帐号 address:0xa46443424141804B2Cca1BA42baAB212F062A96A
	> web3.eth.personal.newAccount("xiejianhuai");

	// return the coinbase address of the client
	> web3.eth.coinbase

	// 获取帐号余额
	> web3.eth.getBalance("0xa46443424141804B2Cca1BA42baAB212F062A96A")
	
	// 获取帐号列表
	> web3.eth.personal.getAccounts();
		
	// get the storage at a specific position of an address
	> web3.eth.getStorageAt("0xa46443424141804B2Cca1BA42baAB212F062A96A", 0);

	// return the data at given address addressHexString
	> web3.eth.getCode("0xa46443424141804B2Cca1BA42baAB212F062A96A");

	// returns a block matching the block number or block hash
	> web3.eth.getBlock(3150);

	// return the number of transactions in the given block
	> web3.eth.getBlockTransactionCount("0x100b4025db180526e2aeea26da804311224b4e50626076e52185a1ee64cce9b4");

	// returns a transction matching the given transaction hash
	> web3.eth.getTransaction('0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b');
	
	// get the numbers of transactions sent from this address
	> web3.eth.getTransactionCount("0x407d73d8a49eeb85d32cf465507dd71d507100c1");


	> 
	> web3.eth.sendTransaction({data:code},function(err,transactionHash){ if(!err){ console.log(transactionHash); } });

	// 一个帐号给另外一个帐号转账
	var Web3 = require('web3');
	if(typeof web3 !== 'undefined'){web3 = new Web3(web3.currentProvider);} else {web3 = new Web3(new Web3.providers.HttpProvider("http://123.207.239.105:8540"))}
	var myAddress = "0x002D137e2676F057801755BE62EcFE5Ae8B24Cc3";
	var destAddress = "0x0002868f4d49042981e7F7318D5B809EA6B6F482";
	var transferAmount = 1;
	var count = web3.eth.getTransactionCount(myAddress);
	
	var contractAddress = "0x2DC4984F1EBa9B8b4ab7F79c8edA2AC57C28d664";

	var abiArray = JSON.parse('[{\"constant\":true,\"inputs\":[],\"name\":\"name\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"wiairInitialSupply\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_spender\",\"type\":\"address\"},{\"name\":\"_value\",\"type\":\"uint256\"}],\"name\":\"approve\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"totalSupply\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_from\",\"type\":\"address\"},{\"name\":\"_to\",\"type\":\"address\"},{\"name\":\"_value\",\"type\":\"uint256\"}],\"name\":\"transferFrom\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"wiairSymbol\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"decimals\",\"outputs\":[{\"name\":\"\",\"type\":\"uint8\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_value\",\"type\":\"uint256\"}],\"name\":\"burn\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"\",\"type\":\"address\"}],\"name\":\"balanceOf\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_from\",\"type\":\"address\"},{\"name\":\"_value\",\"type\":\"uint256\"}],\"name\":\"burnFrom\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"symbol\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_to\",\"type\":\"address\"},{\"name\":\"_value\",\"type\":\"uint256\"}],\"name\":\"transfer\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"wiairTokenName\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_spender\",\"type\":\"address\"},{\"name\":\"_value\",\"type\":\"uint256\"},{\"name\":\"_extraData\",\"type\":\"bytes\"}],\"name\":\"approveAndCall\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"wiairDecimal\",\"outputs\":[{\"name\":\"\",\"type\":\"uint8\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"\",\"type\":\"address\"},{\"name\":\"\",\"type\":\"address\"}],\"name\":\"allowance\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"initialSupply\",\"type\":\"uint256\"},{\"name\":\"tokenName\",\"type\":\"string\"},{\"name\":\"tokenSymbol\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":true,\"name\":\"from\",\"type\":\"address\"},{\"indexed\":true,\"name\":\"to\",\"type\":\"address\"},{\"indexed\":false,\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"Transfer\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":true,\"name\":\"from\",\"type\":\"address\"},{\"indexed\":false,\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"Burn\",\"type\":\"event\"}]');

	var contract = new web3.eth.Contract(abiArray, contractAddress, { from: myAddress });
	
	var balance = contract.methods.balanceOf(myAddress).call();
	web3.eth.personal.unlockAccount(myAddress,"").then(console.log);  //用密码解锁，当然密码是需要绝密保存的
	contract.methods.transfer('0x006C7634CCb4fd623F5d692c59f131A5459Da56d', 1).send().then(console.log).catch(console.error); //然后转就OK了
	balance = contract.methods.balanceOf(myAddress).call();
  	
	
	
	