# DeCentraCore

## 🪙 Project Description
**DeCentraCore** is a blockchain-based decentralized identity and reputation management system. It enables users to create and manage secure, verifiable digital identities without relying on centralized platforms. The system ensures transparency, trust, and immutability for all user data.

---

## 🎯 Project Vision
To build a **trustless digital ecosystem** where individuals control their own identity and reputation, empowering secure interactions without intermediaries. DeCentraCore envisions a transparent, self-sovereign identity framework for the decentralized world.

---

## ✨ Key Features
- **Decentralized Identity:** Each user creates their identity directly on the blockchain.  
- **Transparent Reputation:** Reputation scores are public and immutable.  
- **Owner-Managed Control:** Only the contract owner can verify or remove users.  
- **Event Tracking:** Every registration, update, and removal is recorded on-chain for full traceability.

---

## 🚀 Future Scope
- **Self-Governed Reputation:** Introduce community voting for reputation updates.  
- **Cross-Chain Identity:** Enable identity usage across multiple blockchain networks.  
- **Integration with dApps:** Allow DeCentraCore IDs for login/authentication in decentralized apps.  
- **NFT Identity Badges:** Mint NFTs representing verified user profiles.  
- **DAO Governance:** Transition from a single owner to a decentralized governance model.
Contract address:// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @title DeCentraCore
 * @dev A decentralized identity and reputation management system.
 */
contract Project {
    address public owner;

    struct UserProfile {
        address userAddress;
        string name;
        uint256 reputation;
        bool isRegistered;
    }

    mapping(address => UserProfile) public users;

    event UserRegistered(address indexed user, string name);
    event ReputationUpdated(address indexed user, uint256 newReputation);
    event UserRemoved(address indexed user);

    constructor() {
        owner = msg.sender;
    }

    // Function 1: Register a new decentralized user
    function registerUser(string calldata _name) external {
        require(!users[msg.sender].isRegistered, "User already registered");
        users[msg.sender] = UserProfile(msg.sender, _name, 0, true);
        emit UserRegistered(msg.sender, _name);
    }

    // Function 2: Update a user’s reputation (only owner)
    function updateReputation(address _user, uint256 _newReputation) external {
        require(msg.sender == owner, "Only owner can update reputation");
        require(users[_user].isRegistered, "User not registered");
        users[_user].reputation = _newReputation;
        emit ReputationUpdated(_user, _newReputation);
    }

    // Function 3: Remove a user (only owner)
    function removeUser(address _user) external {
        require(msg.sender == owner, "Only owner can remove users");
        require(users[_user].isRegistered, "User not registered");
        delete users[_user];
        emit UserRemoved(_user);
    }
}
