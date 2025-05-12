# Solana Transaction

This article by Blockchain at Yonsei analyzes Solana's transaction mechanism in 6 stages based on Helius's Solana report.  
Helius Solana Report: https://report.helius.dev

**1\. Introduction**

Solana is a **high-performance, high-throughput blockchain** capable of processing thousands of transactions per second (TPS). Unlike traditional blockchains with slow processing speeds and high fees, Solana provides **extremely fast transaction processing and low fees**.

One of the main factors slowing down traditional blockchains is the **mempool**, a 'transaction waiting room'. Solana has completely eliminated this mempool and introduced a more efficient network protocol to maximize speed and efficiency.

This article explains Solana's **transaction processing workflow** using **Helius's** 6-stage framework, detailing how transactions are **captured, prioritized, and transmitted**.

# **2\. Six Stages of Solana's Transaction Lifecycle**

**![][image1]**

## **2.1 Users & Transaction Submission**

Solana transactions start with **users**, who generate and sign them using wallets or applications. In this process, users interact with **Solana's RPC (Remote Procedure Call) nodes**. RPC nodes act as intermediary servers that bridge communication between users and the Solana blockchain. When users perform activities like creating transactions through wallets or applications, these nodes receive the requests, forward them to the blockchain network, and return the results back to users.

## **How Transactions Are Created**

**![][image2]**

Users sign transactions with their **Ed25519 private keys**.

Each transaction includes:

* **Header**: Specifies which accounts (signers) must sign the transaction.  
* **Account Addresses**: Lists the accounts that will be read from or modified by the transaction.  
* **Recent Blockhash**: Includes the hash of a recent block to prevent replay attacks (where the same transaction could be executed multiple times).  
* **Instructions**: Calls on-chain programs to specify what actions to perform.

## **Submitting Transactions via RPC Nodes**

* Users create transactions using a wallet or application and send them to RPC nodes. RPC nodes act as a bridge, forwarding the transactions to the Solana blockchain network.  
* Users can pay additional **Priority Fees** to request faster processing of their transactions.  
* RPC nodes **simulate** transactions to verify their validity before sending them to the actual network. This allows users to check whether the transaction would succeed and detect any errors in advance. (This feature is enabled by default and runs when the *skipPreflight* option is set to **false**.)

## **2.2 Gulf Stream: Mempool-less Transaction Forwarding**

## **What is Mempool?**

A mempool (memory pool) is a temporary storage area in traditional blockchains (Bitcoin, Ethereum) where transactions wait before being processed. When a user initiates a transaction, it is stored in the mempool in an "unconfirmed" state until it is included in a block and confirmed. Each node maintains its own mempool, and miners/validators select transactions from their mempool to include in the next block.

If transactions remain in the mempool for a long time, network congestion occurs, and users often compete by offering higher fees to get their transactions processed faster.

**Solana's Gulf Stream![][image3]**

Solana has completely eliminated this waiting room (mempool). Instead, it introduced a system called "Gulf Stream." Gulf Stream refers to the process from when a node receives a transaction on the network until it reaches the leader of the current slot and arrives at the Fetch stage of the TPU (Transaction Processing Unit).

This system **directly sends transactions to predetermined future block producers (slot leaders)** to process transactions "without waiting," quickly and safely. This significantly reduces network congestion and transaction confirmation times.

## **Role of the Leader Node**

A leader is a validator with authority to produce blocks for a specific time period (about 0.4 seconds, called a 'slot'). The leader schedule is determined in advance for 2-day units (epochs) and is shared among all validators. The leader processes transactions and creates blocks during its slot time, then passes the turn to the next leader.

## **Eliminating the Mempool - Transaction Processing Method**

* **Direct Forwarding System**: Without waiting for transactions in a mempool, Gulf Stream immediately sends transactions to the next slot's leader. This eliminates the need for validators to store large volumes of transactions long-term, reducing memory usage and effectively suppressing front-running and spam attacks.  
* **Automatic Expiration System**: All transaction messages must include a recent blockhash, which is only valid for about 150 slots (roughly one minute). After 150 slots, the blockhash expires and expired transactions are automatically deleted from the network, preventing old data accumulation.

## **Transaction Forwarding Process (Example)**

1. Solana designates future block producers according to a predetermined leader schedule.  
2. When a user creates a transaction, it is sent to an RPC node (or validator node).  
3. The RPC node checks the next slot leader and **directly forwards** the transaction.  
4. The leader validates the transaction and includes it in a block.  
5. Transactions not processed within one minute are automatically deleted.

## **Transition from UDP to QUIC**

Initially, Solana used **UDP** as its network protocol. UDP transmits data without establishing a connection between sender and receiver, offering the advantage of speed but experiencing the following issues:

![][image4]

* It is not connection-oriented and lacks flow control or packet receipt confirmation. In other words, it doesn't verify whether data arrived properly and can't adjust transmission speeds when the network is congested.  
* There is no effective way to limit how much data someone sends or prevent/mitigate malicious behavior (Candy Machine spam attacks).

After switching to **QUIC**, developed by **Google**, Solana gained the following improvements:

* **Congestion Control**: Minimizes transaction loss.  
* **Reliability**: Reduces packet loss, improving communication quality.  
* **Security**: Encrypted channels lower the possibility of attacks.

The adoption of QUIC has **improved the stability and reliability of the Solana network**. However, despite these improvements, there is still ongoing discussion about how effective the QUIC implementation is in Solana.

## **Stake-Weighted Quality of Service (SWQoS)**

**![][image5]**

## **How SWQoS Works on Solana**

Stake-Weighted Quality of Service (SWQoS) is a system that gives higher transaction processing priority to validators who stake more (SOL). Validators who stake more SOL secure more concurrent connections (streams), ensuring that important transactions aren't dropped during network congestion.

The Solana network has a total of 2,500 connection channels:

* 500 connections: Available for all RPC nodes to use (general channels).  
* 2,000 connections: Only available to staked validators (stake-weighted connections).

Each validator receives a portion of these connections based on their staked proportion.  
In other words, validators with higher stake can open more streams, allowing them to handle a higher transaction load.

Additionally, in the TPU system, each connection (stream) limits the Packets Per Second (PPS) according to stake ratio (rate limiting). Therefore, nodes without stake have very low PPS limits applied, minimizing their impact on the network.

**Pros and Cons**

* **Enhanced User Experience (UX)**: Thanks to SWQoS, from a user's perspective, transactions are processed quickly even when the network is congested.  
* **Barriers to Entry**: Since SWQoS provides more bandwidth and concurrency to high-stake validators, smaller or independent validators may face higher barriers to network participation.  
* **Trust-Based Assumptions**: RPC nodes are not staked, have no voting rights, and don't participate in consensus, so they cannot directly benefit from SWQoS. Therefore, a trust relationship must be formed between validators and RPC nodes to maximize the benefits of SWQoS.

In Solana, how well transactions enter the network and how quickly they are included in blocks are determined by different mechanisms. These two aspects are managed through Stake-Weighted Quality of Service (SWQoS) and Priority Fees, respectively. Below is a summary of the differences between these two systems:

**Difference: SWQoS vs Priority Fees**

* **SWQoS:** A system that provides fast dedicated channels (like VIP-only entrances) allowing validators with more stake to send transactions to the network more easily and in greater volume when the network is congested. In other words, it guarantees 'priority at the network entrance' so transactions enter the network successfully. SWQoS does not determine when transactions will actually be included in blocks.  
* **Priority Fees:** A system that determines the order of processing after transactions have already entered the leader's queue, prioritizing transactions that pay higher fees. This determines which transactions enter the block first.

## **2.3 Block-Building: TPU & Execution**

**![][image6]**

The **Transaction Processing Unit (TPU)** is Solana's **block production engine**. To efficiently process tens of thousands of transactions per second, it operates in parallel across several stages:

**1\. Fetch Stage/QUIC Streamer: Collecting Transaction Packets from the Network**

* Packet memory allocation: Transaction packets received through the QUIC protocol are temporarily stored in memory.  
* Packet merging: Several packets that arrive simultaneously are merged into a single transaction.  
* PPS limit application: According to SWQoS, the Packets Per Second (PPS) is restricted. Validators with higher stakes can transmit more packets.

**2\. SigVerify Stage: Transaction Validation**

* Deduplication: Removes duplicate transactions.  
* Load-Shedding: When the network is overloaded, some excessive packets are removed to reduce network load.  
* Signature Verification: Verifies the authenticity of transaction signatures, discarding packets with invalid signatures.

**3\. Banking Stage: Transaction Execution and Block Construction**

* Transaction processing decision: Determines whether to forward, hold, or process transactions.  
* If the validator is the current leader, it processes waiting or newly arrived transactions in the current slot.  
* Forms a candidate block.

**4\. Broadcast Stage: Propagating the Completed Block to the Network**

* Shred creation: Converts validated transactions into **entries**, then packages them into **shreds**. This is similar to compressing a large file with ZIP for split transmission.  
* After serializing, signing, and encoding the shreds, they are quickly propagated to all validators through the **Turbine protocol**.

In this way, Solana's TPU manages high transaction loads through the stages of packet collection > validation > execution > propagation, verifies the authenticity of transactions, and creates blocks according to the schedule. Through parallel processing, the stake-weighting system, and QUIC protocol, it consistently delivers high performance.

## **Banking Stage in Detail**

The **Banking Stage** is the core stage of the TPU that turns transactions into actual blocks. It determines how validators process received transactions and constructs candidate blocks.

**1\. Determining Packet Treatment**

* **Forward**: If the validator is not the current leader, it forwards the transaction to the leader for the next slot.  
* **Hold**: If the validator is scheduled to be the leader for the next slot, it temporarily keeps the transaction in a waiting state.  
* **Process**: If the validator is the leader for the current slot, it executes this transaction to update the Bank state.

**2\. Bank Integration**

* A "Bank" is a kind of snapshot in the Solana blockchain that represents the ledger state of the current slot. It acts as a "real-time ledger" showing the current state of all accounts' balances, statuses, and data.  
* Successfully processed transactions update the Bank state (balances, account data, etc.), forming the foundation for the next block.

**3\. Parallel Execution**

* Parallel execution means processing multiple transactions simultaneously rather than one by one.  
* Non-conflicting transactions: Bundles up to 64 non-conflicting transactions into one entry and processes them simultaneously.  
* Conflicting transactions: Separated into distinct entries and executed sequentially.

**4\. Validation and Block Assembly**

* Invalid transactions (signature errors, insufficient funds, etc.) are discarded.  
* Verified transactions are recorded in the Accounts DB.  
* When the leader slot ends, the generated block is finalized and propagated to the network.

Through this process, Solana efficiently processes many transactions in parallel and accurately manages account-based state.

## **2.4 Turbine Block Propagation**

After a block is built, it's ready to be transmitted to all participants in the network via Turbine. This process is called **block propagation**.

![][image7]

## **Core Principles of Turbine**

Turbine is Solana's **block propagation protocol**. Instead of sending the entire block to all nodes at once, it uses a more efficient method.

![][image8]

**1. Shredding: Breaking Blocks into Pieces**  
The leader node splits the block data into MTU-sized data shreds (the maximum amount of data that can be transmitted from one node to another without further splitting) and creates 32 data shreds. It also creates 32 recovery shreds to prepare for potential data loss and corruption.  

**2. Erasure Coding: Data Recovery Insurance**
* Using the Reed-Solomon erasure coding method, 32 recovery shreds are generated. Recovery shreds are redundant packets containing parity information (recovery data).  
* Even if packets are lost or arrive late, validators can recover the lost data through parity information.  
* Solana uses 32:32 FEC (Forward Error Correction). This means that even if up to 32 of the 64 packets are lost, they can be recovered without retransmission, providing about 99% transmission success rate. Leaders have the authority to increase the FEC ratio to improve the probability of successful block transmission.  

**3. Turbine Tree Structure: Efficient Propagation**  
Turbine uses a tree-based protocol for efficient data transfer between validators.

![][image9]

The forwarding process is as follows:

* **List Creation**: All validators in the network are sorted by stake (amount of staked SOL). Higher-stake validators are prioritized to receive data faster.  
* **List Shuffling**: The sorted validator list is deterministically shuffled using a seed based on the slot leader's ID, slot number, shred index, etc., making data transmission more efficient. Here, "deterministically shuffled" means that the shuffling method is not completely random but always produces the same result based on predetermined rules and input values (e.g., seed value, slot leader ID, slot number, shred index). This ensures that all nodes in the network can obtain the same shuffled result if they know the same input values.  
* **Layer Formation**: The shuffled list is organized into a hierarchical tree structure based on a parameter called DATA_PLANE_FANOUT (currently set at 200). Through a method where one node forwards data to lower nodes, rapid propagation is ensured, typically requiring only 2-3 hops (Leader → Root → Layer 1 → Layer 2) to reach all validators.

Currently, Turbine uses the UDP protocol for block propagation, providing very low latency.

## **Advantages Over Traditional Gossip**

The gossip protocol is a block propagation mechanism widely used in traditional blockchains, where each node passes received information to randomly selected neighboring nodes. This has the characteristic of information gradually spreading throughout the network, but scalability issues arise as the number of nodes increases.

Turbine overcomes these limitations of the gossip method, providing the following advantages:

1. **Scalability**: Tree-based data distribution prevents excessive load.  
2. **Reduced Latency:** Parallel data forwarding enables quick block data propagation and confirmation.  
3. **Integrity Guarantee:** Even when packets are lost, data can be efficiently recovered using erasure coding and retransmission mechanisms, ensuring data integrity.  
4. **Bandwidth Savings:** Each node processes only the minimum required data without duplication, efficiently using network bandwidth.

## **Turbine's Role in High-Throughput Architecture**

* **Fast block distribution** enables quick block verification among global validators.  
* Supports **rapid leader transition**, allowing the next slot's leader to efficiently receive data.

In conclusion, Turbine plays an essential role in enabling Solana to function as a high-performance and scalable blockchain.

## **2.5 Transaction Validation Unit (TVU)**

**![][image10]**

After blocks are propagated through Turbine, the **Transaction Validation Unit (TVU)** verifies the accuracy of the blocks through the following procedures:

1. **Shred Reconstruction**: Blocks are split into data fragments called shreds for network propagation. The TVU combines these fragments to restore the original block.  
2. **State Verification**: Verifies that the information in the reconstructed block (account balances, smart contract states, etc.) is correct and consistent with the previous state.  
3. **Execution Replay**: Independently re-executes the transactions included in the block to confirm that the results match the results recorded in the block.  
4. **Voting Mechanism**: Uses the **Tower BFT** mechanism to vote on validated blocks, cryptographically signs them, and participates in network consensus.

Through these validation steps, the TVU ensures the accuracy and consistency of each block, maintaining the integrity of the ledger.

## **2.6 Consensus: Voting & Fork Resolution**

Solana achieves **fast finality** through **Proof of Stake (PoS)** and **Tower BFT**:

**1\. Tower BFT & Block Finalization**

* **PoS-based:** Tower BFT is Solana's consensus algorithm, where validators receive voting power proportional to their staked amount.  
* A block is finalized when more than 66% of the network stake agrees (supermajority).  
* **Lockout mechanism:** This mechanism restricts validators from voting on different forks for a certain period after voting for a specific block, limiting validators' ability to change fork choices and increasing network stability. This lockout **gets longer with each subsequent vote**, preventing validators from easily changing forks and naturally guiding the network to **converge on a single chain**.

## **Tower BFT & Block Finalization Process**

1. **Validators propose or vote on blocks for each slot according to the predetermined leader schedule.**  
    In Solana, block producers (leaders) are predetermined through PoH (Proof of History), and the designated leader generates a block in their slot.

2. **Validators judge whether newly created blocks are valid and send votes for that slot.**  
    These votes are recorded on the Solana blockchain as transactions, serving as validators' trust records.

3. **With each vote, the 'lockout' period for previous slots is extended.**  
    When a validator votes for a specific slot, a restriction is created that prevents voting on other forks for a certain number of slots. The lockout doubles with each subsequent vote, making it increasingly difficult to switch forks.

4. **As votes accumulate, more than 66% of the total network stake supports a specific block, and that block is finalized.**  
    This stake-based voting prevents chain forking and stably converges to a single chain.

5. **Validators can only vote on the next slot if the blocks they previously voted for are included in the new chain.**  
    If not included, the vote is rejected due to lockout violation, and the validator cannot follow that chain. This strongly maintains network finality.

**2\. Fork Handling & Chain Selection**

**![][image11]**

* When conflicting blocks are proposed, the blockchain can branch into multiple forks.  
* Validators select the heaviest chain based on **PoH timestamps** (selecting the oldest fork based on the time information recorded in each block) and **stake-weighted voting** (giving higher weight to votes from validators with more stake).  
* Unselected forks are discarded, and transactions included only in rejected forks must be resubmitted.

By combining Proof of Stake with Tower BFT, Solana allows **honest validator networks to quickly finalize blocks**, consistently maintaining high throughput.

# **3\. Reasons for Dropped Transactions**

The main reasons why transactions in Solana fail or get dropped (excluding custom program errors or incorrect instructions) are:

**1\. Network Drops**

* Transactions can be dropped due to UDP packet loss or network congestion.  
* Under heavy load, validators might exceed their transaction forwarding limits (10,000 per second). Transactions exceeding this limit are not forwarded to other validators and are dropped.

**2\. Stale or Incorrect Blockhash**

* Transactions include a **recent blockhash** to timestamp (record when the transaction was created) and determine processing order.  
* Validators reject transactions if the provided blockhash is invalid or doesn't match the current state.

**3\. Expired Blockhash**

* Blockhashes expire after approximately **151 slots** (about 1 minute 19 seconds).  
* Transactions referencing expired blockhashes are automatically rejected by validators.

**4\. Lagging RPC Nodes**

* RPC node pools might be temporarily out of sync with the latest state.  
* Transactions using blockhashes obtained from up-to-date nodes may be rejected if sent to lagging nodes.

**5\. Temporary Network Forks**

* Temporary forks can occur due to slow validators.  
* Transactions using blockhashes from a fork recognized by only a few validators may be dropped when the network selects a different fork.

Understanding these scenarios helps diagnose and resolve transaction issues in the Solana network.

## **Workarounds**

**1\. Resubmit Transactions**

* Strategically resubmitting transactions can increase their chances of being included in a block.

**2\. Stake-Weighted Quality of Service (SWQoS)**

* Using staked RPC connections (e.g., **Helius**, **Triton**) can process transactions with higher priority and success rates.

**3\. Jito**

* Utilizing the Jito Block Engine and paying appropriate Jito tips not only prioritizes transaction processing but also provides MEV protection, prevents transaction cancellation, and ensures optimized transaction processing through bundling in the Solana network.

**4\. Jito Alternatives**

* You can modify Jito to use your own clients or use services that have optimized the network to transmit data quickly on the blockchain (e.g., **bloXroute**, **Temporal/Nozomi**, **NextBlock**).

# **4\. Jito**

Jito is a **modified version of the Solana validator client**, developed to effectively capture and fairly distribute **Maximal Extractable Value (MEV)**. MEV refers to **additional profits that validators can earn by adjusting or selecting the order of transactions**. Jito enhances Solana's standard validator by adding specialized on-chain and off-chain components to improve profitability, optimize block space, and fairly redistribute MEV profits between validators and stakers.

Jito's main components are:

* **Off-chain components**: Relayer, Block Engine  
* **On-chain programs**: Tip Payment Program, Tip Distribution Program  
* Specialized validator pipeline (**BundleStage**)

## **Key Components and Architecture**

**1\. Jito-Solana** Validator

* Runs additional stages to handle MEV bundles: **RelayerStage**, **BlockEngineStage**, **BundleStage.**  
* Responsible for validating, simulating, and atomically executing bundles.

**2\. Relayer**

* Acts as a transaction entry point gateway.  
* Delays transactions by about 200ms for MEV bundle formation.  
* Communicates via gRPC protocol to prevent bottlenecks and support smooth load balancing.

**3\. Block Engine**

* Core decision-making layer for MEV bundle processing.  
* Receives transactions and bundles from searchers/traders.  
* **Simulates bundles off-chain, prioritizing them based on profitability (tips and computing efficiency).**  
* Selects the optimal bundles to atomically forward to validators.

**4\. BundleStage (Validator Pipeline)**

* Ensures atomic execution of bundles – all transactions within a bundle either succeed together or fail together.  
* Guarantees strict sequential execution of transactions within bundles.  
* Locks accounts associated with a bundle to prevent conflicts with other transactions.  
* Integrates directly into the validator's transaction processing pipeline alongside the standard BankingStage.

**5\. Tip Payment Program (On-chain)**

* Serves as a kind of "piggy bank" for storing MEV tips.  
* Searchers deposit tips (additional lamports) into predetermined PDAs (Program-Derived Accounts).  
* Facilitates the secure management and tracking of tips.

**6\. Tip Distribution Program (On-chain)**

* Distributes MEV tips to validators and stakers according to stake ratio.  
* Every epoch, tip rewards are distributed according to a validator reward list organized as a Merkle tree, with each validator proving their reward information is included in the list through a Merkle proof. Here, Merkle proof is a lightweight verification method proving that a validator's reward information is included in the Merkle tree.

## **Detailed Transaction Flow**

**1\. Transaction Submission & Relayer Delay**

* User transactions enter through the **Relayer** and are held for about 200ms to form MEV bundles.

**2\. Bundle Formation & Simulation**

* MEV searchers submit bundles (up to 5 transactions) to the **Block Engine.**  
* The Block Engine quickly simulates these bundles off-chain to analyze their profitability and feasibility.

**3\. Bundle Auction**

* The Block Engine conducts auctions every 200ms.  
* Bundles are prioritized based on two criteria: **size of the provided tip** and **computing efficiency (Tip per CU ratio)**.  
* Bundles with conflicting accounts are auctioned together, while non-conflicting bundles are processed in parallel auctions.

**4\. Validator Execution**

* Selected bundles from the auction are sent to the validator's **BlockEngineStage** and then move to the **BundleStage pipeline**.  
* Transactions within a bundle are executed atomically in a strict order.  
* Related accounts are locked until execution is completed, making simultaneous changes impossible.

**5\. Tip Collection**

* Tips from executed bundles are deposited in PDAs managed by the **Tip Payment Program**.

**6\. Block Creation and Broadcast**

* The validator combines MEV bundles and regular transactions to construct a block.  
* The first 80% of the slot time prioritizes space for MEV bundles; if bundles are insufficient, the remaining slot time is allocated to regular transactions.  
* The finalized block is propagated to the network.

## **Atomicity and Bundle Constraints**

* Bundles must ensure atomicity where all transactions either succeed together or fail together.  
* Bundles cannot span multiple slots and must comply with cost and QoS constraints.  
* Conflicts with accounts essential to the consensus mechanism (such as voting accounts) are prohibited.

## **Tip Payment and Distribution Mechanism**

**Current Model (Centralized)**

* MEV tips collected during each epoch are aggregated in the **Tip Distribution Account (TDA)**.  
* Tip distribution is managed through a centrally calculated Merkle root, and stakers claim rewards through it.

**Future Model (Decentralized: Tip Rewards NCN)**

* Nodes independently calculate and vote on the Merkle root.  
* Tip distribution is finalized when 2/3 of nodes reach consensus.  
* Automatic deductions (3%) for the DAO and NCN operators are included.  
* Decentralization, transparency, and security are enhanced.

**Conclusion & Impact**

* Jito has become an important component of Solana, accounting for about 2/3 of fee revenue.  
* Over 90% of Solana's active stake uses Jito, playing a vital role in validator economics and network stability.  
* Understanding Jito's structure (Relayer, Block Engine, Bundle Stage, Tip management programs) is essential to understanding Solana's ecosystem.

# **5\. Yellowstone Geyser & Real-Time Data Streaming**

## **How Yellowstone Geyser Works**

* When validators process transactions and update account states, Geyser captures these events (e.g., token transfers, smart contract logs, slot completions) in near real-time.  
* Events are streamed to external subscribers through the Dragon's Mouth gRPC interface as granular data feeds.  
* Clients can set filters to receive updates only for specific accounts or programs, minimizing bandwidth usage.

## **Benefits for Developers & dApps**

* **Real-Time Analytics**: DeFi, NFT, and trading platforms can access immediate data.  
* **Event Filtering**: Subscribe only to relevant transactions.  
* **Lower Infrastructure Costs**: Minimize overhead by streaming only necessary data.

# **6\. Conclusion**

Solana's **transaction lifecycle** leverages innovative components — **Users → Gulf Stream → Block Production → PoH → Turbine → Block Verification & Consensus** — to enable **high-speed, high-throughput** block creation. By **eliminating mempools**, implementing **stake-weighted prioritization**, and utilizing **real-time data**, Solana minimizes latency, congestion, and bottlenecks.

By utilizing **Yellowstone Geyser** for transaction streaming and setting appropriate fees and tips via **SWQoS**, **Jito**, or **Jito alternatives**, users can quickly capitalize on market opportunities. Additionally, **distance to the Yellowstone Geyser node** and **internet latency to SWQoS and Jito services** significantly impact transaction speed and execution efficiency, making **network topology** a critical consideration for traders and dApp developers.

Several upcoming updates this year will further enhance Solana's performance and user experience. **Agave's major upgrade** will dramatically improve network processing efficiency and speed through the introduction of the Greedy Scheduler, CU limits, Turbine improvements, and more. Additionally, the **new consensus algorithm** scheduled for Q4 is expected to significantly reduce chain finality time, further accelerating transaction settlement.

Jump Crypto's upcoming **Firedancer client** aims to process up to **1 million transactions per second (TPS)**, significantly enhancing Solana's performance, while the introduction of **Doublezero**, a dedicated high-performance networking layer, will increase transaction throughput and reduce latency and jitter, improving validator performance. Furthermore, **Asynchronous Program Execution (APE)** will alleviate network transaction bottlenecks by processing program execution asynchronously, and **native support for Passkeys** scheduled for April will greatly improve the Web3 login UX through password-free authentication using fingerprint or Face ID.

Through continuous innovation and optimization, Solana is establishing itself as a leading blockchain for fast and scalable application development, setting new standards for Web3 as a premier infrastructure for decentralized systems.
