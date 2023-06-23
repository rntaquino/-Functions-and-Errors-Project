# Functions-and-Errors-Project
The purpose of this code is to create contracts with the require(), assert(), and revert() statements implemented.
## Getting Started
Copy the file below:

```Java
// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

contract MyToken {
    // public variables here
    string public tokenName = "Sample";
    string public tokenAbbrv = "SMPLE";
    uint public totalSupply = 0;

    /// mapping from user wallet address to token balance
    mapping (address => uint) public balances;

    /**
     * @notice This function mint the _value tokens to the _address account
     * @param _address user wallet address
     * @param _value Amount of tokens to mint
     */
    function mint(address _address, uint _value) public {
        /// Checking _value to be greater than zero or return the mentioned error message
        require(_value > 0, "Value must be greater than zero");

        totalSupply += _value;
        balances[_address] += _value;

        /* Assert that the balance of address has increased 
            by _value or returns the error if condition failed
        */
        assert(balances[_address] >= _value);
    }

    /**
     * @notice This function burn the _value tokens from the _address account
     * @param _address user wallet address
     * @param _value Amount of tokens to burn
     */
    function burn(address _address, uint _value) public {
        if (_value == 0) {
            revert("Value must be greater than zero"); // Revert if _value is 42
        }
        require(balances[_address] >= _value, "Insufficient balance"); // Require sufficient balance to burn

        totalSupply -= _value;
        balances[_address] -= _value;

        assert(balances[_address] <= balances[_address] + _value); // Assert that the balance of address has decreased by _value or is zero
    }

    // name function
    function name() public view returns (string memory) {
        return tokenName;
    }

    // symbol function
    function symbol() public view returns (string memory) {
        return tokenAbbrv;
    }

    // decimals function
    function decimals() public pure returns (uint8) {
        return 18; // Assuming 18 decimals for this example
    }
}


```
## Executing the Program

To run this program, you must use Remix, an online IDE for developing, deploying, debugging, and testing Ethereum and EVM-compatible smart contracts. Head over to the Remix website at https://remix.ethereum.org/.

You should be redirected to the home page of the website. You should see the phrase "new file" highlighted in blue. Click it and enter your desired name for the file.

Once you have created the file, could you paste the code you copied earlier?

After pasting the file, please look over to the left side of the website. You will be able to see different icons, but I want you to hover your pointer and find "Solidity Compiler," and click on it.

In the solidity compiler, ensure the checkbox for auto compile is checked, and click the refresh icon named "Compile(your file name)."

Next, hover your pointer over the icon below and click "Deploy and run transactions."

Here, you can experiment with the number of tokens minted and burned. For starters, click the yellow "Deploy" button, which should officially create the token ready to be minted and burned.

Under the deployed contracts tab, click the following buttons to view the token name and abbreviation, and of course, the total supply you currently have. 

Now, if you want to experiment with the minting and burning function, scroll to the very top and see "Account" From there, you can choose what accounts you would like to transact with, but to make things easier, you can start with the default one. Copy the account details.

After copying the details, go to the "Deployed Contracts" tab page, and you should be able to see the buttons named "burn" and "mint." Click the arrow down beside them and text fields will be displayed as "_address."
and "_value." In the address text field, paste the copied account details from earlier, and in the value text field, input the number of tokens you would like to mint and burn.

Once you are done, click the "tokenSupply" button again to view your updated token amount.

Note that no transaction or error will happen if the token you burned exceeds the one you minted.

### For the require() statement:

```Java
require(_value > 0, "Value must be greater than zero");
```

The user cannot mint if the user inputs a zero value in the minting value field area because minting zero tokens don’t make any sense, and it unnecessarily uses a gas fee for doing the transaction, which is a waste.

### Next is the revert() statement:

```Java
revert("Value must be greater than zero"); // Revert if _value is 42
```

Here, we are checking that the value of the tokens we are burning should be greater than zero. If it is not, the condition becomes true where the user will receive a message that “Value must be greater than zero,” and it will revert all the gas consumed and undo all the changes. 

### Lastly, the assert() statement:

```Java
assert(balances[_address] <= balances[_address] + _value); // Assert that the balance of address has decreased by _value or is zero
```

It is a function wherein it checks the user's balance to see if it has decreased or not after deducting the amount from the balance. If it does not decrease, then the execution stops there, and reverts all changes.

