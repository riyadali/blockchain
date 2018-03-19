# blockchain
Information on blockchains and cryptocurrencies as well as the programming language Solidity

__ A tutorial for Solidity can be found here https://ethereumbuilders.gitbooks.io/guide/content/en/solidity_tutorials.html

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
