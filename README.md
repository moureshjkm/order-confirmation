# OrderConfirmation 

This Ethereum smart contract, named **OrderConfirmation**, is designed to facilitate the confirmation and cancellation of orders between a buyer and a seller. The contract is written in Solidity, a programming language specifically designed for smart contracts on the Ethereum blockchain.

## License

This smart contract is released under the MIT License. Please refer to the [LICENSE](LICENSE) file for more details.

## Overview

The smart contract includes the following key components:

1. **State Variables:**
   - `seller`: The Ethereum address of the seller.
   - `buyer`: The Ethereum address of the buyer.
   - `orderConfirmed`: A boolean flag indicating whether the order has been confirmed.

2. **Constructor:**
   - The contract constructor is executed at the time of deployment and takes the buyer's address as a parameter. The seller is automatically set to the address deploying the contract.

```solidity
constructor(address _buyer) {
    seller = msg.sender;
    buyer = _buyer;
}
```

3. **confirmOrder Function:**
   - The `confirmOrder` function allows the buyer to confirm the order. It sets the `orderConfirmed` flag to true.
   - Only the buyer can execute this function to ensure the confirmation comes from the correct party.

```solidity
function confirmOrder() external {
    require(msg.sender == buyer, "Only the buyer can confirm the order");
    assert(!orderConfirmed); // Ensure order is not confirmed twice
    orderConfirmed = true;
}
```

4. **cancelOrder Function:**
   - The `cancelOrder` function allows either the buyer or the seller to cancel the order.
   - It is marked as `view` to indicate that it doesn't modify the contract state.
   - Order cancellation is not allowed after confirmation, and an error is thrown in such cases.

```solidity
function cancelOrder() public view {
    require(msg.sender == buyer || msg.sender == seller, "Only the buyer or seller may cancel");
    revert("Order cancellation is not allowed after confirmation");
}
```

## Usage

1. Deploy the contract, providing the buyer's address as a parameter.
2. The buyer can confirm the order using the `confirmOrder` function.
3. Either the buyer or the seller can cancel the order using the `cancelOrder` function, with restrictions to prevent cancellation after confirmation.

## Author 

Mouresh

monu360v@gmail.com
