
# Introduction

**Celer Intent** is a next-generation omnichain liquidity protocol designed to deliver seamless trading experiences for users and optimize capital efficiency for institutional market makers. Traditional cross-chain trading can be costly or even impractical, especially when handling large volumes, due to AMM-induced slippage and shallow liquidity in bridge-based pools. Celer Intent changes this by enabling “just-in-time” liquidity, allowing users to execute cross-chain swaps with **zero slippage**.

At its core, Celer Intent introduces an **xRFQ (cross-chain Request For Quote)** system. Instead of routing trades through a series of decentralized exchanges and bridges, user intents are broadcast directly to a network of professional market makers. The market maker offering the most competitive quote responds with a verifiable signature, and the transaction is settled atomically through smart contracts and Celer’s inter-chain messaging framework.

The **Celer Intent** protocol offers the following key benefits:

**Low fees.**\
Since trades are executed directly between users and market makers on separate chains, Celer Intent eliminates the need for intermediate bridges and DEXes—reducing multi-hop fees that typically compound during cross-chain transactions.

**Superior capital efficiency.**\
Unlike AMMs that require liquidity to be locked in pools regardless of activity, Celer Intent only requires capital at the moment of a confirmed user request. This “on-demand” model allows market makers to keep funds productive elsewhere when not in use, resulting in significantly better capital utilization than traditional bridges or DEXes.

**Large cross-chain swaps with zero slippage.**\
Because trades are matched directly with market makers at a locked-in price, Celer Intent avoids the slippage typically seen with intermediate on-chain swaps—particularly when large transaction sizes are involved.

**MEV resistance.**\
By operating outside the bounds of on-chain AMMs, Celer Intent prevents common MEV exploits such as sandwich attacks. All quotes are locked off-chain before execution, preserving pricing integrity.

**Celer Intent** is already live on mainnet and fully integrated with Celer cBridge. Developers of omnichain dApps—including bridges, DEXes, and aggregators—can easily plug in via the [Celer Intent Open API](developer/open-api/). Market makers can connect through the [Celer Intent SDK](broken-reference) to start handling quotes and fulfilling cross-chain orders.

Most importantly, Celer Intent is a **trustless protocol**. Trades are executed only when all conditions are cryptographically verified and met. Neither the user nor the market maker can claim funds from the other without completing the full cross-chain transaction.

