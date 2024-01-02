# escrow_journal

The evolution of programs on solana

To be able to see the evolution of tools and programming practices on solana, 3 techincally comparable escrow contracts 
written in different phases of the network and tooling development been chosen.

## 1: Escrow contract by PaulX. https://paulx.dev/blog/2021/01/14/programming-on-solana-an-introduction/

Key features:
 - Written in pure rust
 - Utilizes only available generic functionality to complete the task
 
 When PaulX wrote the first escrow contract to showcase the possibilities of solana smart contracts, very little 
 toolig/examples or documentation was available. The solana foundation created it's own ebpf version called rbpf 
 wich is an expanded set of instructions compared to ebpf. The idea was to make the rbpf framework for solana 
 more or less turing complete, so functions like byte operations were added. This can be discovered in the 
 sourcecode of the escrow, just by looking at it people can recognise that low level operations are happening. 
 For some people it can be tedious, or very hard to wrap their head around complex concepts, and the programming 
 on solana was not helping in developing easy at all. There are clear advantages in having low level control 
 of operations on the chain, the most obvious is speed and efficiency. Building up a contract with only basic, 
 computationally cheap operations will produce a fast and efficient program that feels good to use. The clear 
 disadvantage is in complexity. You don't just have to understand the rust programming language and it's operations, 
 but also the raw structure of data and accounts used on solana. The most noticable downside of this contract 
 is there are no account validation checks at all, which opens up a multitude of possible vulnerabilities, 
 ending in loss of funds.	
 
## 2: Escrow by ironaddicteddog. https://hackmd.io/@ironaddicteddog/solana-anchor-escrow

Key features: 
 - Written using the Anchor framework
 - Utilizes anchor utilities to build the contract and make it relatively readable and safe
  
 With the release of the anchor framework, a lot of difficulty was removed from smartcontract development with rust. 
 The best features of anchor is abstracting away the accounts iterator, and doing the right account validity checks 
 for the developer. This was a huge improvement in security, as accounts like the System program, 
 and the TokenProgram are automatically checked under the hood. The other big advantage of anchor is the clearly defined 
 account structure, and while in itself the abstraction to see account structs is achieved with some smart macro 
 manipulation, it makes it much easier for the developer to visualize the structure he has to work with. 
 Under the hood is all just bytes and offsets, but removing the burden of understanding byte structures from 
 the developer does make focusing on business logic much easier. People can focus on what they want to achieve 
 instead of how to build the structures for what they want to achieve. Anchor also helped to motivate developers
 using ancor as best practice for smartcontract development.

## 3: Escrow by Dean Little. https://github.com/deanmlittle/anchor-escrow-2023

Key features:
 - Written in anchor
 - Uses clearly defined file and function structure for better readability
 
 Besides using thew anchor framework and ejoying it's advantages, Dean has put in extra effort to make the code
 readable for everyone. And while understanding traits and struct implementations might need some rust knowledge,
 which in general applies to all of the contracts, reading and following the flow of code is way easier if the 
 functions have their own file, associated with their own context. In ironaddicteddog's contract, a single file 
 was used to write everything, which makes it harder to differenciate between looking at the deposit, or the 
 withdraw impl functions. Making a clear difference with storing the functions in named files not just makes the 
 code readable for other developers, but also makes auditors work easier. A concious representation of the logic
 is key for safety, and this contract is clearly the strongest in that.