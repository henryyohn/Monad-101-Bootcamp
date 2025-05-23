## 第一章：走进 Web3 世界

1. 简单描述一下本地开发、部署合约的流程                                                              

2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程                                                

3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧 



回答1：

本地开发SOLIDITY智能合约，一般会使用HARDHAT开发环境，编写智能合约后，可以通过CHAI进行单元测试，测试通过后就可以部署到测试链上验证，一般是用测试钱包进行各种功能的验证，如果验证没有问题了最后就部署到公链。



回答2：

DAPP一般理解为以浏览器插件的形式存在，用户安装DAPP后，可以通过UI界面控制DAPP连接RPC，再到部署在区块链的某个智能合约上，从而进行各种交易，或者查询链上数据等等。一些操作会需要用户授权，此时用户需要手动操作以确认授权。



回答3：

我认为最重要的是持续验证和零信任，即假设每一个步骤都可能会被黑客入侵，因此在操作的每一步，都要进行检视后再行动。

其次是双因子认证，在重要操作，比如授权，转账等场景下，应该都要开启双因子认证。

最后是钱包备份，最好使用冷钱包，需要保存在安全的地方。

