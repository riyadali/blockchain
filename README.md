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
