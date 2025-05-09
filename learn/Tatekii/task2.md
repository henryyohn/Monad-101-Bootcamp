## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity中存储成本最高的变量类型是`state`变量，其数据永久存储在区块链上。  
2. 使用`constant`关键字声明的常量可以节省Gas费，其值必须在编译时确定。  
4. 当合约收到不带任何数据的以太转账时，会自动触发`receive`函数。  

---

### 二、选择题

4. 函数选择器(selector)的计算方法是：B  
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前4字节  
   **C)** 函数参数的ABI编码  
   **D)** 函数返回值的类型哈希  

5. 以下关于mapping的叙述错误的是：D  
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对  

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和Gas退还角度）

require、assert 和 revert 是用于处理错误和异常的三种常用机制

`require(bool,(string|error)?)`

检查一个条件,为false则抛出异常；

⚠️所有已消耗的 Gas 都会被消耗掉，但它会退还剩余的 Gas（在 EVM中是通过中断交易的执行来退还未消耗的 Gas）。

`assert(bool)`

用于内部错误捕获，通常用来验证代码的不可达状态，可以在合约内检查不变性条件；不可自定义抛出的错误。

⚠️不会退换任何Gas。

`revert((string|error)?)`

手动调用，回滚交易并return 错误信息。

💡传入自定义Error实例会更省gas；

⚠️所有已消耗的 Gas 都会被消耗掉，但它会退还剩余的 Gas。


7. 某合约同时继承A和B合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

```
调用B.foo，按照override(...)中指定的顺序(后=>前/右=>左)
```


8. 当使用`call`方法发送ETH时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

```solidity
- <address>.call(bytes memory) returns (bool, bytes memory)

可以发送代货同时调用目标合约中的函数，返回执行结果boolean与数据；
低级API，使用时需小心，有被对方call回来的风险；

- <address payable>.transfer(uint256 amount)

转账失败（余额不足，拒收）时revert，失败最多花费2300Gas，
```

💡本质区别，限制Gas的使用，防范重入攻击