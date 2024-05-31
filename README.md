## Project: Degen Token (ERC-20): Unlocking the Future of Gaming
Degen Gaming has selected the Avalanche blockchain, a leading blockchain platform for web3 gaming projects, to create a fast and low-fee token. With these tokens, players can not only purchase items in the store. Degen project is to revolutionize online content creation by making it possible for the student to reward content creators with Degen tokens when they post quality content and enjoy the student to transact the tokens.

## Getting Started
Executing program

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "./Ownable.sol";


contract LuceroCharacterSkin is ERC20, Ownable {

    mapping (uint256 => uint256) public SkinCharacterId;

    event ItemRedeemed(address indexed player, uint256 indexed SkinId, uint256 diasAmount);

    constructor(address initialOwner) ERC20("Diamond", "DIAS") {
        _mint(initialOwner, 3000); 

        SkinCharacterId[11] = 1000; // Item 1: Jawhead The Nutcracker, Dias = 1000 Value 
        SkinCharacterId[22] = 1500; // Item 2: Leomord Inferno Soul, Dias = 1500 Value 
        SkinCharacterId[33] = 2000; // Item 3: Mathilda Dream Groove, Dias = 2000 Value 
        SkinCharacterId[44] = 2500; // Item 4: Khufra Volcanic Overlord, Dias = 2500 Value 
        SkinCharacterId[55] = 3000; // Item 5: Gusion Dimension Walker, Dias = 3000 Value 
    }

    function mint(address to, uint256 diasAmount) external onlyOwner {
        _mint(to, diasAmount);
    }

    function transfer(address to, uint256 diasAmount) public override returns (bool) {
        _transfer(_msgSender(), to, diasAmount);
        return true;
    }

    function setSkinCharacterId(uint256 SkinId, uint256 diasAmount) external onlyOwner {
        SkinCharacterId[SkinId] = diasAmount;
    }

    function redeemSkin(uint256 SkinId) public returns (uint256) {
        uint256 Amount = SkinCharacterId[SkinId];
        require(Amount > 0, "Invalid Skin ID or Skin not for sale");
        require(balanceOf(msg.sender) >= Amount, "Insufficient Dias");
        
        _burn(msg.sender, Amount);
        emit ItemRedeemed(msg.sender, SkinId, Amount);
        return SkinCharacterId[SkinId];
    }

    function redeemBalance(address player) public view returns (uint256) {
        return balanceOf(player);
    }

    function burn(uint256 diasAmount) external {
        _burn(msg.sender, diasAmount);
    }

    function balanceOf(address account) public view override returns (uint256) {
        return super.balanceOf(account);
    }
}


Author NTC

Rogelio A Lucero Jr.

8215129@ntc.edu.ph
