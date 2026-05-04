# Base #
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MojeBaseNFT is ERC721URIStorage, Ownable {
    uint256 private _nextTokenId;

    // Konstruktor ustawia nazwę i symbol Twojej kolekcji
    constructor(address initialOwner) 
        ERC721("Moja Kolekcja Base", "MNFT") 
        Ownable(initialOwner) 
    {}

    // Funkcja do tworzenia (mintowania) nowego NFT
    function safeMint(address to, string memory uri) public onlyOwner {
        uint256 tokenId = _nextTokenId++;
        _safeMint(to, tokenId);
        _setTokenURI(tokenId, uri);
    }
}
