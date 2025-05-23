## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity 中存储成本最高的变量类型是 <u>state</u> 变量，其数据永久存储在区块链上。
2. 使用 <u>immutable</u> 关键字声明的常量可以节省 Gas 费，其值必须在编译时确定。
3. 当合约收到不带任何数据的以太转账时，会自动触发 <u>receive</u> 函数。

---

### 二、选择题

4. 函数选择器(selector)的计算方法是：<u>B</u>  
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前 4 字节  
   **C)** 函数参数的 ABI 编码  
   **D)** 函数返回值的类型哈希

5. 以下关于 mapping 的叙述错误的是：<u>C</u>  
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套 mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和 Gas 退还角度）

答：  
| | require | assert | revert |
|----------|----------|----------|----------|
| 触发条件 | 基于条件 | 基于条件 | 手动触发 |
| Gas 退还 | 剩余 gas 退还 | 0.8.0 前，无退还<br>0.8.0 及以后版本，部分退还 | 剩余 gas 退还 |

7. 某合约同时继承 A 和 B 合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

答：实际执行时，不会调用任何父合约的函数，而是调用合约 C 的 foo() 函数。因为合约 C 中的 foo() 函数使用了 override(A,B)，重写了 foo() 函数。

8. 当使用`call`方法发送 ETH 时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

答：方式（1）属于低级调用，失败会返回 false，需手动处理，程序会继续执行后续代码；方式（2）使用了 transfer 函数，失败会自动回滚交易，并抛出异常。
