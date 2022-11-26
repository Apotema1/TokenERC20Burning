# TokenERC20Burning
Mi primer código de token ERC20 que tiene una extención para auto-quema.
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract DesafioExtensiones is ERC20Burnable, Pausable, Ownable {

    constructor() ERC20Burnable() ERC20("elizaldeToken", "ET") {
        _mint(msg.sender, 1000 * (10**decimals()));
    }

    function decimals() public pure override returns (uint8) {
        return 6;
    }

    function Pausar() public onlyOwner {
        _pause();
    }

    function Despausar() public onlyOwner {
        _unpause();
    }

    function Quemar(uint cantidad) public {
        require(paused() != true, "El contracto esta pausado");
        burn(cantidad);
    }


}
