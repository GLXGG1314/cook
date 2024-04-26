# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "headers",
    hdrs = glob(["include/**/*.h"]),
    strip_include_prefix = "include",
)
Language:        Cpp
BasedOnStyle:  Google
PointerAlignment: Left
Checks:          'clang-analyzer-*,readability-redundant-*,performance-*'
WarningsAsErrors: 'clang-analyzer-*,readability-redundant-*,performance-*'
HeaderFilterRegex: '.*'
AnalyzeTemporaryDtors: false
FormatStyle:     none
User:            user
pragma solidity ^0.8.0;

// 在 Solidity 中定义一个代币合约
contract MyToken {
    // 代币的名称
    string public name = "My Token";
    // 代币的符号
    string public symbol = "MTK";
    // 代币的小数位数
    uint8 public decimals = 18;
    // 代币的总供应量
    uint256 public totalSupply;
    // 保存每个地址的余额
    mapping(address => uint256) public balanceOf;
    // 保存授权的余额
    mapping(address => mapping(address => uint256)) public allowance;

    // 当合约被创建时执行的函数
    constructor(uint256 _initialSupply) {
        // 将初始供应量分配给合约创建者
        balanceOf[msg.sender] = _initialSupply;
        // 设置总供应量
        totalSupply = _initialSupply;
    }

    // 转移代币
    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(_to != address(0), "Invalid address");
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;

        emit Transfer(msg.sender, _to, _value);

        return true;
    }

    // 授权他人代币转移
    function approve(address _spender, uint256 _value) public returns (bool success) {
        allowance[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    // 代币转移从授权列表中
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        require(_from != address(0), "Invalid address");
        require(_to != address(0), "Invalid address");
        require(balanceOf[_from] >= _value, "Insufficient balance");
        require(_value <= allowance[_from][msg.sender], "Insufficient allowance");

        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        allowance[_from][msg.sender] -= _value;

        emit Transfer(_from, _to, _value);

        return true;
    }

    // 事件，用于通知客户端代币转移
    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    // 事件，用于通知客户端代币被授权
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}
