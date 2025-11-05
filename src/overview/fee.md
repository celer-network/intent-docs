# Fee

Every RFQ order executed through Celer Intent includes two types of fees, both of which are paid in the source chain’s token:

**Base Fee**\
This flat fee covers network-related costs such as gas and cross-chain messaging expenses. It may be charged by either the market maker or the Celer Intent protocol, depending on the setup of the transaction.

**Percentage Fee**\
This fee is calculated as a proportion of the total swap amount. It is split into two parts:

* One portion is retained by the market maker, and may vary across different providers based on their pricing models.
* The remaining portion is collected by the Celer Intent protocol itself to support ongoing infrastructure and development.
