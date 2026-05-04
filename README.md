// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MojeBaseNFT is ERC721URIStorage, Ownable {
    uint256 private _nextTokenId;
    
    uint256 public constant MAX_SUPPLY = 1000; 
    // NOWOŚĆ: Limit na jeden portfel, żeby uniknąć botów
    uint256 public constant MAX_PER_WALLET = 5;
    mapping(address => uint256) public addressMintedBalance;

    constructor(address initialOwner) 
        ERC721("Moja Kolekcja Base", "MNFT") 
        Ownable(initialOwner) 
    {}

    // Funkcja darmowego bicia (Free Mint)
    function freeMint(string memory uri) public {
        require(_nextTokenId < MAX_SUPPLY, "Kolekcja wyprzedana!");
        require(addressMintedBalance[msg.sender] < MAX_PER_WALLET, "Osiagnales limit na portfel");

        uint256 tokenId = _nextTokenId++;
        addressMintedBalance[msg.sender]++;
        _safeMint(msg.sender, tokenId);
        _setTokenURI(tokenId, uri);
    }
}

