# safely-mutable-ERC-20-interface
An interface for an ERC-20 token smart contract that enforces the expected behaviour of each entry-point.

1. *erc20-interface.sol* - is a vanilla interface for an ERC-20 token, using a hub-spoke (or proxy) pattern that allows the implementation to be updated post-deployment (through calls).

2. *clean-erc20-implementation.sol* - is an implementation of an ERC-20 token reproduced from [here](https://theethereum.wiki/w/index.php/ERC20_Token_Standard). 

3. *erc20-implementation.sol* - is an adaption of implementation of *clean-erc20-implementation.sol* to be used with erc20-interface.sol, note how some methods (e.g. transfer) have an added argument so that the original caller's address can be passed on from the interface. Note how this has the effect of leaving the implementation uncompliant with the ERC-20 standard, but compliance is restored through the interface. 

4. *erc20-behavioual-specification.dea* - is a specification of the expected behaviour of an implementation of the ERC-20 standard. This goes beyond the simple specification of an API, but, e.g., specifies when a transfer should be successful or not and what effect it should have. This respects the informal definition given in the standard's description, see [here](https://theethereum.wiki/w/index.php/ERC20_Token_Standard). Moreover, the specification used here is specified in a specification language used by the runtime verification tool [contractLARVA](https://github.com/gordonpace/contractLarva).

5. *erc20-behavioural-interface.sol* - is the interface *erc20-interface.sol* with the behavioural specification specified in *erc20-behavioual-specification.dea* enforced at runtime. See [contractLARVA](https://github.com/gordonpace/contractLarva) for how to produce this file.

6. *ERC20 Behavioural Interface Gas Costs.xlsx* - lists the total gas costs for each step here. This includes the gas costs of setting up the whole framework (which includes deploying the interface and the implemenation, and making the interface the owner of the implementation, so that the implementation can only be accessed from the interface), and the costs of added by monitoring for the behavioural specification at runtime for each individual function.
