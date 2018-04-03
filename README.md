# blockchain
Information on blockchains and cryptocurrencies as well as the programming language Solidity

__ A tutorial for Solidity can be found here https://ethereumbuilders.gitbooks.io/guide/content/en/solidity_tutorials.html

__ A reference for Ethereum is Mastering Ethereum by Andreas Antonopoulos and Gavin Wood
   + The latest text for this book is here https://github.com/ethereumbook/ethereumbook
   + First edition of the book is here https://github.com/ethereumbook/ethereumbook/tree/first_edition/

__ Popular blockchain explorers include    
      
      Bitcoin Block Explorer (https://blockexplorer.com/)      
      BlockCypher Explorer (https://live.blockcypher.com/)
      blockchain.info (https://blockchain.info/)
      BitPay Insight (https://insight.bitpay.com/)
      
__ Mycelium for Android (https://wallet.mycelium.com/) is probably a good wallet for Android smart phones

__ Current transaction fees can be found here: https://bitcoinfees.earn.com/

__ You can programmatically estimate fees using an API as follows

      Using the fee estimation API
            $ curl https://bitcoinfees.21.co/api/v1/fees/recommended

            {"fastestFee":80,"halfHourFee":80,"hourFee":60}
            
      The API returns a JSON object with the current fee estimate for fastest confirmation (fastestFee), confirmation within three             blocks (halfHourFee) and six blocks (hourFee), in satoshi per byte.

__ Applications/concepts built on the Blockchain (mostly from the book "Mastering Bitcoin")
   + Proof-of-Existence (Digital Notary) - A digital fingerprint can be committed with a transaction to the blockchain, proving that a document existed (Timestamp) at the time it was recorded. The fingerprint cannot be modified ex-post-facto (Immutability) and the proof will be stored permanently (Durability)
   + Kickstarter (Lighthouse) - If you sign one input and the output of a fundraiser transaction, others can contribute to the fundraiser but it cannot be spent until the goal (output value) is funded.
   + Payment Channels (discussed further below) - A multisig 2-of-2 with a timelock used as the "settlement" transaction of a payment channel can be held and spent whenever by either party.  The two parties can then create commitment transactions that double-spend the settlement on a shorter timelock (in essence invalidating previous commitment transactions)
   + Colored Coins are used to track assets that are not stored directly on the bitcoin blockchain, as opposed to bitcoin itself, which is an asset intrinsic to the blockchain.
      + Colored coins are used to track digital assets as well as physical assets held by third parties and traded through colored coins certificates of ownership.  Digital assets colored coins can represent intangible assets such as a stock certificate, license, virtual property (game items), or most any form of licensed intellectual property (trademarks, copyrights, etc).  Tangible colored coins can represent certificates of ownership of commodities (gold, silver, oil), land title, automobiles, boats, aircraft, etc.
      + The term derives from the idea of "coloring" or marking a nominal amount of bitcoin, for example, a single satoshi, to represent something other than the bitcoin value itself
      + More recent implementations of colored coins use the OP_RETURN script opcode to store metadata in a transaction, in conjunction with external data stores that associate the metadata to specific assets.
      + The two most common implementations today of colored coins are Open Assets (http://www.openassets.org/ and Colored Cois by Colu (http://coloredcoins.org).  These two systems use different approaches to colored coins and are not compatible.  Colored coins created in one system cannot be seen or used in the other system.
      + An Open Assets- compatible wallet application and blockexplorer can be found at coinprism (https://www.coinprism.info)
      + A Colu Colored Coins-compatible wallet application and blockexplorer can be found at Blockchain Explorer (http://coloredcoins.org/explorer).
      + A Copay wallet plug-in can be found at Colored Coins Copay Addon (http://coloredcoins.org/colored-coins-copay-addon/).
   + Counterparty - Counterparty is a protocol layer built on top of bitcoin.
      + The Counterparty protocol, similar to colored coins, offers the ability to create and trade virtual assets and tokens. In addition, Counterparty offers a decentralized exchange for assets. Counterparty is also implementing smart contracts, based on the Ethereum Virtual Machine (EVM).
      + Like the colored coins protocols, Counterparty embeds metadata in bitcoin transactions, using the OP_RETURN opcode or 1-of-N multisignature addresses that encode metadata in the place of public keys. Using these mechanisms, Counterparty implements a protocol layer encoded in bitcoin transactions. The additional protocol layer can be interpreted by applications that are Counterparty-aware, such as wallets and blockchain explorers, or any application built using the Counterparty libraries.
      + Counterparty can be used as a platform for other applications and services, in turn. For example, Tokenly is a platform built on top of Counterparty that allows content creators, artists, and companies to issue tokens that express digital ownership and can be used to rent, access, trade, or shop for content, products, and services. Other applications leveraging Counterparty include games (Spells of Genesis) and grid computing projects (Folding Coin).
      + More details about Counterparty can be found at https://counterparty.io. The open source project can be found at https://github.com/CounterpartyXCP.
   + Payment Channels and State Channels - Payment channels are a trustless mechanism for exchanging bitcoin transactions between two parties, outside of the bitcoin blockchain. 
      + These transactions, which would be valid if settled on the bitcoin blockchain, are held off-chain instead, acting as promissory notes for eventual batch settlement. Because the transactions are not settled, they can be exchanged without the usual settlement latency, allowing extremely high transaction throughput, low (submillisecond) latency, and fine (satoshi-level) granularity.
      + Actually, the term channel is a metaphor. State channels are virtual constructs represented by the exchange of state between two parties, outside of the blockchain. There are no "channels" per se and the underlying data transport mechanism is not the channel. We use the term channel to represent the relationship and shared state between two parties, outside of the blockchain.
      + To further explain this concept, think of a TCP stream. From the perspective of higher-level protocols it is a "socket" connecting two applications across the internet. But if you look at the network traffic, a TCP stream is just a virtual channel over IP packets. Each endpoint of the TCP stream sequences and assembles IP packets to create the illusion of a stream of bytes. Underneath, it’s all disconnected packets. Similarly, a payment channel is just a series of transactions. If properly sequenced and connected, they create redeemable obligations that you can trust even though you don’t trust the other side of the channel.
      + In this section we will look at various forms of payment channels. First, we will examine the mechanisms used to construct a one-way (unidirectional) payment channel for a metered micropayment service, such as streaming video. Then, we will expand on this mechanism and introduce bidirectional payment channels. Finally, we will look at how bidirectional channels can be connected end-to-end to form multihop channels in a routed network, first proposed under the name Lightning Network.
      + Payment channels are part of the broader concept of a state channel, which represents an off-chain alteration of state, secured by eventual settlement in a blockchain. A payment channel is a state channel where the state being altered is the balance of a virtual currency.
      + State Channels—Basic Concepts and Terminology
         + A state channel is established between two parties, through a transaction that locks a shared state on the blockchain. This is called the funding transaction or anchor transaction. This single transaction must be transmitted to the network and mined to establish the channel. In the example of a payment channel, the locked state is the initial balance (in currency) of the channel.
         + The two parties then exchange signed transactions, called commitment transactions, that alter the initial state. These transactions are valid transactions in that they could be submitted for settlement by either party, but instead are held off-chain by each party pending the channel closure. State updates can be created as fast as each party can create, sign, and transmit a transaction to the other party. In practice this means that thousands of transactions per second can be exchanged.
         + When exchanging commitment transactions the two parties also invalidate the previous states, so that the most up-to-date commitment transaction is always the only one that can be redeemed. This prevents either party from cheating by unilaterally closing the channel with an expired prior state that is more favorable to them than the current state. We will examine the various mechanisms that can be used to invalidate prior state in the rest of this chapter.
         + Finally, the channel can be closed either cooperatively, by submitting a final settlement transaction to the blockchain, or unilaterally, by either party submitting the last commitment transaction to the blockchain. A unilateral close option is needed in case one of the parties unexpectedly disconnects. The settlement transaction represents the final state of the channel and is settled on the blockchain.
         + In the entire lifetime of the channel, only two transactions need to be submitted for mining on the blockchain: the funding and settlement transactions. In between these two states, the two parties can exchange any number of commitment transactions that are never seen by anyone else, nor submitted to the blockchain.
      + Simple Payment Channel Example
         + To explain state channels, we start with a very simple example. We demonstrate a one-way channel, meaning that value is flowing in one direction only. We will also start with the naive assumption that no one is trying to cheat, to keep things simple. Once we have the basic channel idea explained, we will then look at what it takes to make it trustless so that neither party can cheat, even if they are trying to.
         + For this example we will assume two participants: Emma and Fabian. Fabian offers a video streaming service that is billed by the second using a micropayment channel. Fabian charges 0.01 millibit (0.00001 BTC) per second of video, equivalent to 36 millibits (0.036 BTC) per hour of video. Emma is a user who purchases this streaming video service from Fabian. Emma purchases streaming video from Fabian with a payment channel, paying for each second of video shows Emma buying the video streaming service from Fabian using a payment channel.
         + In this example, Fabian and Emma are using special software that handles both the payment channel and the video streaming. Emma is running the software in her browser, Fabian is running it on a server. The software includes basic bitcoin wallet functionality and can create and sign bitcoin transactions. Both the concept and the term "payment channel" are completely hidden from the users. What they see is video that is paid for by the second.
         + To set up the payment channel, Emma and Fabian establish a 2-of-2 multisignature address, with each of them holding one of the keys. From Emma’s perspective, the software in her browser presents a QR code with a P2SH address (starting with "3"), and asks her to submit a "deposit" for up to 1 hour of video. The address is then funded by Emma. Emma’s transaction, paying to the multisignature address, is the funding or anchor transaction for the payment channel.
         + For this example, let’s say that Emma funds the channel with 36 millibits (0.036 BTC). This will allow Emma to consume up to 1 hour of streaming video. The funding transaction in this case sets the maximum amount that can be transmitted in this channel, setting the channel capacity.
         + The funding transaction consumes one or more inputs from Emma’s wallet, sourcing the funds. It creates one output with a value of 36 millibits paid to the multisignature 2-of-2 address controlled jointly between Emma and Fabian. It may have additional outputs for change back to Emma’s wallet.
         + Once the funding transaction is confirmed, Emma can start streaming video. Emma’s software creates and signs a commitment transaction that changes the channel balance to credit 0.01 millibit to Fabian’s address and refund 35.99 millibits back to Emma. The transaction signed by Emma consumes the 36 millibits output created by the funding transaction and creates two outputs: one for her refund, the other for Fabian’s payment. The transaction is only partially signed—it requires two signatures (2-of-2), but only has Emma’s signature. When Fabian’s server receives this transaction, it adds the second signature (for the 2-of-2 input) and returns it to Emma together with 1 second worth of video. Now both parties have a fully signed commitment transaction that either can redeem, representing the correct up-to-date balance of the channel. Neither party broadcasts this transaction to the network.
         + In the next round, Emma’s software creates and signs another commitment transaction (commitment #2) that consumes the same 2-of-2 output from the funding transaction. The second commitment transaction allocates one output of 0.02 millibits to Fabian’s address and one output of 35.98 millibits back to Emma’s address. This new transaction is payment for two cumulative seconds of video. Fabian’s software signs and returns the second commitment transaction, together with another second of video.
         + In this way, Emma’s software continues to send commitment transactions to Fabian’s server in exchange for streaming video. The balance of the channel gradually accumulates in favor of Fabian, as Emma consumes more seconds of video. Let’s say Emma watches 600 seconds (10 minutes) of video, creating and signing 600 commitment transactions. The last commitment transaction (#600) will have two outputs, splitting the balance of the channel, 6 millibits to Fabian and 30 millibits to Emma.
         + Finally, Emma clicks "Stop" to stop streaming video. Either Fabian or Emma can now transmit the final state transaction for settlement. This last transaction is the settlement transaction and pays Fabian for all the video Emma consumed, refunding the remainder of the funding transaction to Emma.
         + Emma’s payment channel with Fabian, showing the commitment transactions that update the balance of the channel shows the channel between Emma and Fabian and the commitment transactions that update the balance of the channel.
         + In the end, only two transactions are recorded on the blockchain: the funding transaction that established the channel and a settlement transaction that allocated the final balance correctly between the two participants.
      + Making Trustless Channels
         + The channel we just described works, but only if both parties cooperate, without any failures or attempts to cheat. Let’s look at some of the scenarios that break this channel and see what is needed to fix those:
            + Once the funding transaction happens, Emma needs Fabian’s signature to get any money back. If Fabian disappears, Emma’s funds are locked in a 2-of-2 and effectively lost. This channel, as constructed, leads to a loss of funds if one of the parties disconnects before there is at least one commitment transaction signed by both parties.
            + While the channel is running, Emma can take any of the commitment transactions Fabian has countersigned and transmit one to the blockchain. Why pay for 600 seconds of video, if she can transmit commitment transaction #1 and only pay for 1 second of video? The channel fails because Emma can cheat by broadcasting a prior commitment that is in her favor.
         + Both of these problems can be solved with timelocks—let’s look at how we could use transaction-level timelocks (nLocktime).
         + Emma cannot risk funding a 2-of-2 multisig unless she has a guaranteed refund. To solve this problem, Emma constructs the funding and refund transaction at the same time. She signs the funding transaction but doesn’t transmit it to anyone. Emma transmits only the refund transaction to Fabian and obtains his signature.
         + The refund transaction acts as the first commitment transaction and its timelock establishes the upper bound for the channel’s life. In this case, Emma could set the nLocktime to 30 days or 4320 blocks into the future. All subsequent commitment transactions must have a shorter timelock, so that they can be redeemed before the refund transaction.
         + Now that Emma has a fully signed refund transaction, she can confidently transmit the signed funding transaction knowing that she can eventually, after the timelock expires, redeem the refund transaction even if Fabian disappears.
         + Every commitment transaction the parties exchange during the life of the channel will be timelocked into the future. But the delay will be slightly shorter for each commitment so the most recent commitment can be redeemed before the prior commitment it invalidates. Because of the nLockTime, neither party can successfully propagate any of the commitment transactions until their timelock expires. If all goes well, they will cooperate and close the channel gracefully with a settlement transaction, making it unnecessary to transmit an intermediate commitment transaction. If not, the most recent commitment transaction can be propagated to settle the account and invalidate all prior commitment transactions.
         + For example, if commitment transaction #1 is timelocked to 4320 blocks in the future, then commitment transaction #2 is timelocked to 4319 blocks in the future. Commitment transaction #600 can be spent 600 blocks before commitment transaction #1 becomes valid.
         + Each commitment sets a shorter timelock, allowing it to be spent before the previous commitments become valid shows each commitment transaction setting a shorter timelock, allowing it to be spent before the previous commitments become valid.
         + Each subsequent commitment transaction must have a shorter timelock so that it may be broadcast before its predecessors and before the refund transaction. The ability to broadcast a commitment earlier ensures it will be able to spend the funding output and preclude any other commitment transaction from being redeemed by spending the output. The guarantees offered by the bitcoin blockchain, preventing double-spends and enforcing timelocks, effectively allow each commitment transaction to invalidate its predecessors.
         + State channels use timelocks to enforce smart contracts across a time dimension. In this example we saw how the time dimension guarantees that the most recent commitment transaction becomes valid before any earlier commitments. Thus, the most recent commitment transaction can be transmitted, spending the inputs and invalidating prior commitment transactions. The enforcement of smart contracts with absolute timelocks protects against cheating by one of the parties. This implementation needs nothing more than absolute transaction-level timelocks (nLocktime). Next, we will see how script-level timelocks, CHECKLOCKTIMEVERIFY and CHECKSEQUENCEVERIFY, can be used to construct more flexible, useful, and sophisticated state channels.
         + The first form of unidirectional payment channel was demonstrated as a prototype video streaming application in 2015 by an Argentinian team of developers. You can still see it at streamium.io.
         + Timelocks are not the only way to invalidate prior commitment transactions. In the next sections we will see how a revocation key can be used to achieve the same result. Timelocks are effective but they have two distinct disadvantages. By establishing a maximum timelock when the channel is first opened, they limit the lifetime of the channel. Worse, they force channel implementations to strike a balance between allowing long-lived channels and forcing one of the participants to wait a very long time for a refund in case of premature closure. For example, if you allow the channel to remain open for 30 days, by setting the refund timelock to 30 days, if one of the parties disappears immediately the other party must wait 30 days for a refund. The more distant the endpoint, the more distant the refund.
         + The second problem is that since each subsequent commitment transaction must decrement the timelock, there is an explicit limit on the number of commitment transactions that can be exchanged between the parties. For example, a 30-day channel, setting a timelock of 4320 blocks into the future, can only accommodate 4320 intermediate commitment transactions before it must be closed. There is a danger in setting the timelock commitment transaction interval at 1 block. By setting the timelock interval between commitment transactions to 1 block, a developer is creating a very high burden for the channel participants who have to be vigilant, remain online and watching, and be ready to transmit the right commitment transaction at any time.
         + Now that we understand how timelocks can be used to invalidate prior commitments, we can see the difference between closing the channel cooperatively and closing it unilaterally by broadcasting a commitment transaction. All commitment transactions are timelocked, therefore broadcasting a commitment transaction will always involve waiting until the timelock has expired. But if the two parties agree on what the final balance is and know they both hold commitment transactions that will eventually make that balance a reality, they can construct a settlement transaction without a timelock representing that same balance. In a cooperative close, either party takes the most recent commitment transaction and builds a settlement transaction that is identical in every way except that it omits the timelock. Both parties can sign this settlement transaction knowing there is no way to cheat and get a more favorable balance. By cooperatively signing and transmitting the settlement transaction they can close the channel and redeem their balance immediately. Worst case, one of the parties can be petty, refuse to cooperate, and force the other party to do a unilateral close with the most recent commitment transaction. But if they do that, they have to wait for their funds too.
      + Asymmetric Revocable Commitments - A better way to handle the prior commitment states is to explicitly revoke them. However, this is not easy to achieve.
         + A key characteristic of bitcoin is that once a transaction is valid, it remains valid and does not expire. The only way to cancel a transaction is by double-spending its inputs with another transaction before it is mined. That’s why we used timelocks in the simple payment channel example above to ensure that more recent commitments could be spent before older commitments were valid. However, sequencing commitments in time creates a number of constraints that make payment channels difficult to use.
         + Even though a transaction cannot be canceled, it can be constructed in such a way as to make it undesirable to use. The way we do that is by giving each party a revocation key that can be used to punish the other party if they try to cheat. This mechanism for revoking prior commitment transactions was first proposed as part of the Lightning Network.
         + To explain revocation keys, we will construct a more complex payment channel between two exchanges run by Hitesh and Irene. Hitesh and Irene run bitcoin exchanges in India and the USA, respectively. Customers of Hitesh’s Indian exchange often send payments to customers of Irene’s USA exchange and vice versa. Currently, these transactions occur on the bitcoin blockchain, but this means paying fees and waiting several blocks for confirmations. Setting up a payment channel between the exchanges will significantly reduce the cost and accelerate the transaction flow.
         + Hitesh and Irene start the channel by collaboratively constructing a funding transaction, each funding the channel with 5 bitcoin. The initial balance is 5 bitcoin for Hitesh and 5 bitcoin for Irene. The funding transaction locks the channel state in a 2-of-2 multisig, just like in the example of a simple channel.
         + The funding transaction may have one or more inputs from Hitesh (adding up to 5 bitcoin or more), and one or more inputs from Irene (adding up to 5 bitcoin or more). The inputs have to slightly exceed the channel capacity in order to cover the transaction fees. The transaction has one output that locks the 10 total bitcoin to a 2-of-2 multisig address controlled by both Hitesh and Irene. The funding transaction may also have one or more outputs returning change to Hitesh and Irene if their inputs exceeded their intended channel contribution. This is a single transaction with inputs offered and signed by two parties. It has to be constructed in collaboration and signed by each party before it is transmitted.
         + Now, instead of creating a single commitment transaction that both parties sign, Hitesh and Irene create two different commitment transactions that are asymmetric.
         + Hitesh has a commitment transaction with two outputs. The first output pays Irene the 5 bitcoin she is owed immediately. The second output pays Hitesh the 5 bitcoin he is owed, but only after a timelock of 1000 blocks. The transaction outputs look like this:
             Input: 2-of-2 funding output, signed by Irene
             
                  Output 0 <5 bitcoin>:
                  <Irene's Public Key> CHECKSIG

            Output 1:
            
                  <1000 blocks>
                  CHECKSEQUENCEVERIFY
                  DROP
                  <Hitesh's Public Key> CHECKSIG
    
         + Irene has a different commitment transaction with two outputs. The first output pays Hitesh the 5 bitcoin he is owed immediately. The second output pays Irene the 5 bitcoin she is owed but only after a timelock of 1000 blocks. The commitment transaction Irene holds (signed by Hitesh) looks like this:

            Input: 2-of-2 funding output, signed by Hitesh

               Output 0 <5 bitcoin>:
                  <Hitesh's Public Key> CHECKSIG

               Output 1:
                  <1000 blocks>
                  CHECKSEQUENCEVERIFY
                  DROP
                  <Irene's Public Key> CHECKSIG
    
         + This way, each party has a commitment transaction, spending the 2-of-2 funding output. This input is signed by the other party. At any time the party holding the transaction can also sign (completing the 2-of-2) and broadcast. However, if they broadcast the commitment transaction, it pays the other party immediately whereas they have to wait for a short timelock to expire. By imposing a delay on the redemption of one of the outputs, we put each party at a slight disadvantage when they choose to unilaterally broadcast a commitment transaction. But a time delay alone isn’t enough to encourage fair conduct.



      
   
__ An excellent reference for Bitcoin is Mastering Bitcoin by Andreas Antonopoulos (Chp 3 provides programmatic API interface)
   + Link for 2nd endition of this book can be found here https://bitcoinbook.info/
   
   + The latest text for this book is here https://github.com/bitcoinbook/bitcoinbook
     
   + The book site includes a table of contents which is included below
     
       1. Introduction
        
            What Is Bitcoin?            
            History of Bitcoin            
            Bitcoin Uses, Users, and Their Stories
            Getting Started
            
       2. How Bitcoin Works
        
            Transactions, Blocks, Mining, and the Blockchain
            Bitcoin Transactions
            Constructing a Transaction
            Bitcoin Mining
            Mining Transactions in Blocks
            Spending the Transaction
            
       3. Bitcoin Core: The Reference Implementation
        
            Bitcoin Development Environment
            Compiling Bitcoin Core from the Source Code
            Running a Bitcoin Core Node
            Bitcoin Core Application Programming Interface (API)
            Alternative Clients, Libraries, and Toolkits
            
       4. Keys, Addresses
        
            Introduction
            Bitcoin Addresses
            Implementing Keys and Addresses in Python
            Advanced Keys and Addresses
            
       5. Wallets
        
            Wallet Technology Overview
            Wallet Technology Details
            
       6. Transactions
        
            Introduction
            Transactions in Detail
            Transaction Outputs and Inputs
            Transaction Scripts and Script Language
            Digital Signatures (ECDSA)
            Bitcoin Addresses, Balances and other abstractions
            
       7. Advanced Transactions and Scripting
        
            Introduction
            Multi-Signature
            Pay-to-Script-Hash (P2SH)
            Data Recording Output (RETURN)
            Timelocks
            Scripts with Flow Control (Conditional Clauses)
            Complex Script Example
            
       8. The Bitcoin Network
        
            Peer-to-Peer Network Architecture
            Nodes Types and Roles
            The Extended Bitcoin Network
            Bitcoin Relay Networks
            Network Discovery
            Full Nodes
            Exchanging “Inventory”
            Simplified Payment Verification (SPV) Nodes
            Bloom filters
            How SPV nodes use bloom filters
            SPV nodes and privacy
            Encrypted and Authenticated Connections
            Transaction Pools
            
       9. The Blockchain
        
            Introduction
            Structure of a Block
            Block Header
            Block Identifiers: Block Header Hash and Block Height
            The Genesis Block
            Linking Blocks in the Blockchain
            Merkle Trees
            Merkle Trees and Simplified Payment Verification (SPV)
            Bitcoin’s Test Blockchains
            Segnet – The Segregated Witness Testnet
            Regtest – The local blockchain
            Using test blockchains for development
            
       10. Mining and Consensus
        
            Introduction
            Decentralized Consensus
            Independent Verification of Transactions
            Mining Nodes
            Aggregating Transactions into Blocks
            Constructing the Block Header
            Mining the Block
            Successfully Mining the Block
            Validating a New Block
            Assembling and Selecting Chains of Blocks
            Mining and the Hashing Race
            Consensus Attacks
            Changing the Consensus Rules
            Soft Fork Signaling with Block Version
            Consensus Software Development
            
       11. Bitcoin Security
        
            Security Principles
            User Security Best Practices
            Conclusion
            
       12. Blockchain Applications
        
            Introduction
            Building Blocks (Primitives)
            Applications from Building Blocks
            Colored Coins
            Counterparty
            Payment Channels and State Channels
            Routed Payment Channels (Lightning Network)
            Conclusion
            
      Appendix A: The Bitcoin Whitepaper by Satoshi Nakamoto

            Introduction
            Transactions
            Timestamp Server
            Proof-of-Work
            Network
            Incentive
            Reclaiming Disk Space
            Simplified Payment Verification
            Combining and Splitting Value
            Privacy
            Calculations
            Conclusion
            References
            License
            
      Appendix B: Transaction Script Language Operators, Constants, and Symbols

      Appendix C: Bitcoin Improvement Proposals
      
      Appendix D: Segregated Witness      

      Appendix E: Bitcore
      
            Bitcore’s Feature List
            Bitcore Library Examples
            
      Appendix F: pycoin, ku, and tx
      
            Key Utility (KU)
            
      Appendix F: Bitcoin Explorer (bx) Commands
      
            Examples of bx command use
