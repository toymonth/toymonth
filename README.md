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
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ClickTwo {
    address[] public clickers;
    uint256[] public timestamps;

    event Clicked(address indexed user, uint256 timestamp, uint256 index);

    function click() external {
        clickers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Clicked(msg.sender, block.timestamp, clickers.length - 1);
    }

    function getClick(uint256 index) external view returns (address, uint256) {
        require(index < clickers.length, "Invalid index");
        return (clickers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return clickers.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AccessThree {
    address public owner;
    mapping(address => bool) public hasAccess;

    event AccessGranted(address indexed user);
    event AccessRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasAccess[msg.sender] = true;
    }

    function grantAccess(address user) external {
        require(msg.sender == owner, "Not owner");
        hasAccess[user] = true;
        emit AccessGranted(user);
    }

    function revokeAccess(address user) external {
        require(msg.sender == owner, "Not owner");
        hasAccess[user] = false;
        emit AccessRevoked(user);
    }

    function checkAccess(address user) external view returns (bool) {
        return hasAccess[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BoxThree {
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

contract PulseThree {
    mapping(address => uint256) public pulses;
    mapping(address => uint256) public lastPulse;

    event Pulsed(address indexed user, uint256 level);

    function pulse() external {
        if (block.timestamp <= lastPulse[msg.sender] + 7 minutes) {
            pulses[msg.sender] += 1;
        } else {
            pulses[msg.sender] = 1;
        }
        lastPulse[msg.sender] = block.timestamp;
        emit Pulsed(msg.sender, pulses[msg.sender]);
    }

    function getPulses(address user) external view returns (uint256) {
        return pulses[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract VisaThree {
    address public owner;
    mapping(address => bool) public hasVisa;

    event VisaGranted(address indexed user);
    event VisaRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasVisa[msg.sender] = true;
    }

    function grantVisa(address user) external {
        require(msg.sender == owner, "Not owner");
        hasVisa[user] = true;
        emit VisaGranted(user);
    }

    function revokeVisa(address user) external {
        require(msg.sender == owner, "Not owner");
        hasVisa[user] = false;
        emit VisaRevoked(user);
    }

    function checkVisa(address user) external view returns (bool) {
        return hasVisa[user];
    }
}
