# Workflow

To illustrate the cross-chain trade process, let’s walk through a common use case: a user wants to swap **Token X on Chain A** for **Token Y on Chain B**. This transaction is handled as a **Request for Quote (RFQ)** order.

## Core Flow (cooperative case)

The diagram below outlines the typical RFQ execution process in Celer Intent, where both the user and the selected market maker act cooperatively. Note: The RFQ server operates as a centralized coordinator for communication and quote aggregation.

<img src="../.gitbook/assets/1 (1).png" alt=""><figcaption><p>Core Flow</p></figcaption>

**Step 1**

The user submits an RFQ to the RFQ server, specifying the following details:

* Source and destination chains
* Source and destination tokens
* Amount to be swapped
* Two key time constraints:

**Source Submission Deadline**: The user must confirm the quote and lock their tokens on the source chain before this deadline. If missed, the quote expires and the transaction will revert on-chain.

**Destination Fund Release Deadline**: The market maker must complete the transfer to the user on the destination chain before this deadline. Failure to do so makes the order eligible for refund.

**Step 2**

The RFQ server forwards the user’s request to a list of authorized market makers who are currently online and available to quote.

**Step 3**

Each market maker evaluates the RFQ and, if interested, submits a quote to the RFQ server. The server compares the received quotes and selects the most favorable one—typically the one offering the highest amount of destination tokens. The selected market maker then signs their quote and returns the signed version to the server.

**Step 4**

The RFQ server delivers the signed quote to the user for confirmation and submission.

***

**Step 5**

The user broadcasts the signed quote to the source chain contract, locking their source tokens into the Celer Intent smart contract. This action must occur before the **source submission deadline**. A delay past this deadline causes the transaction to fail.

This on-chain action also triggers **Cross-Chain Message #1**, which is dispatched through Celer Inter-chain Messaging to the destination chain. This message notifies the destination that the user has locked funds on the source chain and that the market maker is authorized to release the destination tokens.

***

**Step 6**

On the destination chain, the market maker executes a transaction that processes **Message #1** and transfers the agreed destination tokens to the user. This must occur before the **destination release deadline**. If delayed beyond the deadline, the RFQ order becomes refundable and the transaction will revert.

Once successful, this transaction emits **Cross-Chain Message #2**, which is sent back to the source chain. This message confirms that the user has received their tokens, and instructs the source chain contract to release the locked funds to the market maker.

***

**Step 7**

Back on the source chain, the market maker finalizes the process by calling a contract function that processes **Message #2**. This releases the user’s locked source tokens to the market maker, completing the transaction.

## Refund Flow (non-cooperative case)

If the market maker does not complete the transfer of destination tokens to the user before the designated **destination release deadline**, the RFQ order transitions into a refundable state on the destination chain.

To safeguard users in such cases, a monitoring component known as the **RFQ Sentinel** implemented using Brevis ZK Coprocessor continuously scans for expired or incomplete orders. When it detects an unfulfilled RFQ past the deadline, the sentinel generate a ZK proof of incomplete transaction and send a **Cross-Chain Message #3**, which is sent back to the source chain.

Upon receiving this message, the user is able to execute a transaction on the source chain to reclaim their originally locked tokens—ensuring that funds remain secure even when counterparties fail to cooperate.

<img src="../.gitbook/assets/2 (1) (1).png" alt=""><figcaption><p>Refund Flow</p></figcaption>
