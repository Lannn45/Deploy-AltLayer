## Deploying a token on the AltLayer dashboard


![Logo](https://miro.medium.com/v2/resize:fit:720/format:webp/1*rsAHPZkNXFfTPEPQx53TMQ.png)

### What is AltLayer?

AltLayer is a decentralized and elastic Rollup-as-a-Service (RaaS) protocol for application developers to launch highly scalable application-tailored execution layers (aka Layer 2s). Built on top of the RaaS protocol,  AltLayer offers:  1) an SDK for developers who wish to manage their rollups themselves, and 2) a no-code dashboard that allows not only developers but also those with little to no coding experience to spin up a customized execution layer within 2 mins through a few simple clicks.

> - [Dashboard AltLayer](https://dashboard.alt.technology/)
> - [Faucet](https://testnet-faucet.altlayer.io/)
> - [Explorer](https://testnet-rollup-explorer.altlayer.io/)
> - [Bridge](https://testnet-rollup-bridge.altlayer.io/)
> - [Guide](https://docs.altlayer.io/altlayer-documentation/testnet/overview)

```
// SPDX-License-Identifier: UNLISCENSED

pragma solidity ^0.8.18;

contract PythonDefi{
    string public name = "Python Defi";
    string public symbol = "PYD";
    uint256 public totalSupply = 100000000000000000000; 
    uint8 public decimals = 18;
    
    /**
     * @dev Emitted when `value` tokens are moved from one account (`from`) to
     * another (`to`).
     *
     * Note that `value` may be zero.
     */
    event Transfer(address indexed _from, address indexed _to, uint256 _value);

     /**
     * @dev Emitted when the allowance of a `spender` for an `owner` is set by
     * a call to {approve}. `value` is the new allowance.
     */
    event Approval(
        address indexed _owner,
        address indexed _spender,
        uint256 _value
    );

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    /**
     * @dev Constructor that gives msg.sender all of existing tokens.
     */
    constructor() {
        balanceOf[msg.sender] = totalSupply;
    }

     /**
     * @dev Moves `amount` tokens from the caller's account to `recipient`.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transfer(address _to, uint256 _value)
        public
        returns (bool success)
    {
        require(balanceOf[msg.sender] >= _value);
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
    }
    
     /**
     * @dev Sets `amount` as the allowance of `spender` over the caller's tokens.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * IMPORTANT: Beware that changing an allowance with this method brings the risk
     * that someone may use both the old and the new allowance by unfortunate
     * transaction ordering. One possible solution to mitigate this race
     * condition is to first reduce the spender's allowance to 0 and set the
     * desired value afterwards:
     * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
     *
     * Emits an {Approval} event.
     */

    function approve(address _spender, uint256 _value)
        public
        returns (bool success)
    {
        allowance[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    /**
     * @dev Moves `amount` tokens from `sender` to `recipient` using the
     * allowance mechanism. `amount` is then deducted from the caller's
     * allowance.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transferFrom(
        address _from,
        address _to,
        uint256 _value
    ) public returns (bool success) {
        require(_value <= balanceOf[_from]);
        require(_value <= allowance[_from][msg.sender]);
        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        allowance[_from][msg.sender] -= _value;
        emit Transfer(_from, _to, _value);
        return true;
    }
}

```

### Changing a contract,name,symbol,totalSupply,decimals with a custom name

