# DIOtoken - Desafio DIO

## 💡 Sobre o Projeto

Este projeto consiste na criação de um token ERC-20 simples, desenvolvido como parte de um desafio da [DIO](https://www.dio.me/). O objetivo é oferecer uma introdução prática ao desenvolvimento de smart contracts na blockchain Ethereum.

## 🛠️ Ferramentas Utilizadas

- **[OpenZeppelin](https://www.openzeppelin.com/)**: Biblioteca confiável e segura para contratos inteligentes. Facilitou a criação do token com uma estrutura simples e intuitiva — ideal para iniciantes.
- **[Remix - Ethereum IDE](https://remix.ethereum.org/)**: Ambiente de desenvolvimento online usado para escrever, compilar e implantar o smart contract.
- **[MetaMask](https://metamask.io/)**: Carteira digital utilizada para interagir com a blockchain. Recomendada para quem está começando a desenvolver na Web3.
- **Sepolia Testnet**: Rede de testes utilizada no projeto. Permite minerar ETH de teste (para pagar o *gas*) usando um mecanismo de Prova de Trabalho (*Proof of Work*).

## 🚀 Objetivo

Criar um token próprio na rede de testes Ethereum, compreendendo na prática conceitos como:

- Deploy de contratos inteligentes
- Transações com MetaMask
- Cálculo e pagamento de taxas de gas
- Utilização de bibliotecas como o OpenZeppelin
## 📜 Código do Token

```solidity
// SPDX-License-Identifier: MIT
// Compatible with OpenZeppelin Contracts ^5.0.0
pragma solidity ^0.8.27;

import {ERC1363} from "@openzeppelin/contracts/token/ERC20/extensions/ERC1363.sol";
import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {ERC20Burnable} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import {ERC20FlashMint} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20FlashMint.sol";
import {ERC20Pausable} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Pausable.sol";
import {ERC20Permit} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";

contract DIOtoken is ERC20, ERC20Burnable, ERC20Pausable, Ownable, ERC1363, ERC20Permit, ERC20FlashMint {
    constructor(address recipient, address initialOwner)
        ERC20("DIOtoken", "DIO")
        Ownable(initialOwner)
        ERC20Permit("DIOtoken")
    {
        _mint(recipient, 10000 * 10 ** decimals());
    }

    function pause() public onlyOwner {
        _pause();
    }

    function unpause() public onlyOwner {
        _unpause();
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    // The following functions are overrides required by Solidity.
    function _update(address from, address to, uint256 value)
        internal
        override(ERC20, ERC20Pausable)
    {
        super._update(from, to, value);
    }
}



  
