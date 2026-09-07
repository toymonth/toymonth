// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PocketTwo {
    address public owner;
    uint256 public total;

    event Deposited(address indexed from, uint256 amount);
    event Withdrawn(uint256 amount);

    constructor() {
        owner = msg.sender;
    }

    function deposit() external payable {
        require(msg.value > 0, "Must send ETH");
        total += msg.value;
        emit Deposited(msg.sender, msg.value);
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");
        uint256 amount = address(this).balance;
        total = 0;
        (bool success, ) = owner.call{value: amount}("");
        require(success, "Transfer failed");
        emit Withdrawn(amount);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AuraTwo {
    mapping(address => uint256) public auras;
    mapping(address => uint256) public lastAura;

    event AuraGained(address indexed user, uint256 level);

    function gain() external {
        if (block.timestamp <= lastAura[msg.sender] + 8 minutes) {
            auras[msg.sender] += 1;
        } else {
            auras[msg.sender] = 1;
        }
        lastAura[msg.sender] = block.timestamp;
        emit AuraGained(msg.sender, auras[msg.sender]);
    }

    function getAuras(address user) external view returns (uint256) {
        return auras[user];
    }
}
