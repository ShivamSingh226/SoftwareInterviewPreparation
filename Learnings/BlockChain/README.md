# BlockChain Fundamentals

## What is a BlockChain?

- A constantly growing ledger storing the continuously happening transactions of bitcoins in a chronological, permanent and immutable way.

- Creator of Bitcoin - Satoshi Nakamoto first ever transaction recorded in 2009.

- Blockchain keeps decentralized record of all the transactions of Bitcoin and prevent double-spend problem.

- Secured by math and cryptography over the decentralized network of blockchain and mining solve the cryptography math functions

- Cryptographic Hash functions are being processed in the crypotgraphic block

- There is a block, nonce(Number used once), data and Hash(SHA 256). We can suppose that if it is starting with four leading zeros, it's a valid hash and block is storing the hash of a preceeding block.

- For every unique combination of Block, nonce and data, there will be a unique hash of SHA 256.

- If a single block of data's unique combination gets modified every next block of data becomes invalid.(Like a Domino Effect)

- Even if a miner, mine the block to receive correct nonce and four leading zeroes, rest of the decentralized blockchain copy would reject the modified one.

- First purchase from Bitcoin: Laszlo Haniyez: 2 pizzas - 10,000 bitcoins - 25 USD. 

## Components of Blockchain

1. Software- Every 10 minutes issues a crypotgraphy challenge to find a nonce makes hash for specific block valid
2. Cryptography
3. Hardware - Thousands of computers all around the world
4. Gaming Theory- Miners race to find the solution to challenge. At stage 1 miner wins and at the stage 2, nonce is verified.(**Proof of Work**).
And for that work, Miner are getting reward of 3.125 Bitcoin

## Coinbase Transaction

1. Every single block has a coinbase Transaction, where miner receives the reward for creating that block. It gives the miner the permisssion to reward itself. 

2. And the user gets all the transaction fees of the particular block which he created. So, a transaction reward plus some of the transaction fees.

## Key Concepts

1. P2P while recording transaction (Disintermediated)

2. Distributed( Across multiple computers )

3. Decentralized (No Central point of failure )

4. Trustless - Distributed Trustless Consensus - All nodes should agree that a transaction took place

5.Value - Digital Unique Asset shared P2P without middlemen

6. Trust - Secure and unalterable record of who owns what

7. Reliability - Decentralized network with no single point of failure

## Cryptocurrency

1. Digital Asset encompassed in Cryptography used to exchange value between the parties

2. Cryptography to secure how it's transferred and to control the creation of new units of that currency

- Impossible to counterfeit

- Impervious to manipulation. Only 21 million Bitcoins. In Venezuela, money printed so much - zero value

- Fast Settlement 

- Can help over 2 billion underbanked economy

- Billion of dollars getting exchanged every day

- No physical currency so no pandemic , lol!


## Smart Contract

1. No Third party. handles conflict, written in code and front-loaded(With every possible scenarios)

2. Two or more parties

3. More than sending virtual currency

4. Automated and disintermediated

5. Immutable

6. Trustless

## Digital Token

1. Steemit - Rewards platform for content publishers

2. Golem - Shared economy computing power

3. Filecoin - Shared economy cloud storage

4. MANA - Decentraland(Metaverse)Cryptocurrency

5. Cryptokitties - NFT

## DAO (Decentralized Autonomous Organization)

1. Collection of Smart Contracts

2. Distributed networks on Blockchain

3. IoT

4. AI

## Business use cases

1. Supply-Chain (Walmart with IBM)

2. Reduced the time to track food from days to minutes. Tracking pork products across China.

3. **Real Estate**: ANZ and Westpac with IBM, digitized commercial property transaction

4. Maersk ( with Microsoft): 20 week proof of concept, make auditing aspects of shipping supply chain easier

5. Improve the tamper-resistance and sharing of data in real-time

6. **Authenticity**: DNV in partnership with Deloitte

7. Humanitarian Aid: Use ethereum to aid Syrian Refugees in **Azraq Camp** in Jordan, through UN World food programme: Increased Transparency and Reduction in Costs.

## Cons of Blockchain

1. Very early stage

2. Lack of Awareness

3. Limited Available Technical Talent

4. Immutable

5. No reversal or modification

6. Key management

7. Scalability

8. Time to process

## Bitcoin

1. Pseudonymous: Your bitcoin address is recorded whenever you move money around(Silk Road Scandal)

2. Not good for laundering money

3. Blockchain is a ledger

4. Blockchain is not Bitcoin: It is being used in Supply Chain management, Real estate and UN WFP.

5. No need to buy a full bitcoin to get a bitcoin

## Bitcoin Cash

1. Developed from Hard Fork increases block size to 8 MB. 

2. Due to limit being crossed 1.9 MB, the Bitcoin cash got split from traditional blockchain.

## Fork (Hard Fork vs Soft Fork)

1. Blockchain split

2. Introduces change force everyone to upgrade: Hard Fork

3. Introduces change which is backwards compatible
. Doesn't need upgrade.

4. Forks happen on regular basis-when miners solve at the same time

5. Eventually one of the chains wins over the other

6. Orphan Block

7. Most blocks are pushed back to Mempool (Awaiting status transaction)

8. Transactions (Input, Amount, Output) should be digitally signed using the owner's private key(A secret which is never shared)

9. SegWit separates Digital Signature with encrypted Input, AMount and Output in it

## Transactions and Block Weight

1. Limited by how many transactions fit within the maximum "block weight"

2. Current Block weight limit is 4 million "Weight Units"

3. Measured in Bytes

4. Fees are also set based on number of bytes in transaction

5. Miners try to maximize their profits by getting as many high fee transactions as will fit

## Controlled Supply of Bitcoin

1. 21 million BTC

2. Halving- 50 NEW BT*10 min=7200 nEW BTC per day

3. Halving-Every 210,000 blocks, rewards are halved.

4. As of 2020, 6.25 NEW BTC * 10 minutes=  900 BTC/day

5. Another halving in the pipeline

6. 100 million Satoshis in One BTC

7. So , 2140 would be the year of last bitcoin ever mined

## When no Bitcoins to mine?

1. When new Block is created, miner gets 6.25 BTC

2. He also gets the transaction fees for all the transaction done in that Block

## Merkle Tree

- Foundation of Blockchain

- Composed of different hashes of blocks of data containing summary of transactions like Hash tree, Ralph Merkle.

- Merkle Trees consist of all hashes of that block of transactions

- Merkle Root single cryptographic hash serving a summary of all the transactions in that block. 

- Private key secured wallet -> Bitcoin Address has a hash of the public key
