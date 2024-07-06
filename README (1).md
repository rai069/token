# ERC20 TOKEM  IN SOLIDITY

This Solidity program is a simple program that demonstrates how we can create an ERC20  token, mint it, and burn it.

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract demonstrate how we can create an ERC20 token in solidty. This program serves as a simple and straightforward purpose of learning solidity, and can be used as a stepping stone for more complex projects in the future.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., ERC20.sol). Copy and paste the following code into the file:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract CustomToken {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;
    address public owner;

    mapping(address => uint256) private balances;

    event Transfer(address indexed from, address indexed to, uint256 value); 
    event Mint(address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    constructor(string memory _name, string memory _symbol, uint8 _decimals, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        owner = msg.sender;
        _mint(owner, _initialSupply * 10 ** uint256(decimals)); // 100*10**1 = 1000
    }

    function balanceOf(address account) public view returns (uint256) {
        return balances[account];
    }

    function transfer(address to, uint256 amount) public returns (bool) {
        _transfer(msg.sender, to, amount);
        return true;
    }

    function mint(address to, uint256 amount) public onlyOwner returns (bool) {
        _mint(to, amount);
        return true;
    }

    function burn(uint256 amount) public returns (bool) {
        _burn(msg.sender, amount);
        return true;
    }

    function _transfer(address from, address to, uint256 amount) internal {
        require(balances[from] >= amount, "ERC20: transfer amount exceeds balance");
        balances[from] -= amount;
        balances[to] += amount;
        emit Transfer(from, to, amount);
    }

    function _mint(address to, uint256 amount) internal {
        totalSupply += amount;
        balances[to] += amount;
        emit Mint(to, amount);
        emit Transfer(address(0), to, amount);
    }

    function _burn(address from, uint256 amount) internal {
        require(balances[from] >= amount, "ERC20: burn amount exceeds balance");
        balances[from] -= amount;
        totalSupply -= amount;
        emit Burn(from, amount);
        emit Transfer(from, address(0), amount);
    }

}


```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile  ERC20.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "ERC20" contract from the dropdown menu,initialize all the values like name, symbol, decimal value and initial supply and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it. Click on the "ERC20" contract in the left-hand sidebar, and then click on call button to check the token name, token symbol and total supply after that you can use mint function to mint the token according to total supply, And after minting of token you can also burn the token form the token supply using burn function. You can only burn a limited amount of token that are present not more than that. After using mint function and burn function you can check your total supply for total amount of token left. Total supply of token changes every time you call the mint and burn function.You can also transfer tokens from one address to another address.
Only owner can mint the token.
Any user can transfer the token from it's own wallet to other wallet.
Any user can burn token.

## Authors

ANKIT KUMAR


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
