---
head:
  - - meta
    - name: title
      content: "Sovereign rollups on Bitcoin with Rollkit"
  - - meta
    - name: description
      content: Last week, we introduced Rollkit, a modular framework for rollups. Today, we are proud to announce that Rollkit is the first rollup framework to support sovereign rollups on Bitcoin. This allows Rollkit rollups to use Bitcoin for data availability. The implementation is in alpha, but we invite curious developers to experiment with it.
  - - meta
    - name: keywords
      content: Rollkit, Celestia
  - - meta
    - name: og:image
      content: /introducing-rollkit/rollkit-blog-cover.png
---

# Sovereign rollups on Bitcoin with Rollkit

By Rollkit

![rollkit-bitcoin](/bitcoin-rollkit/rollkit-bitcoin.png)
_Originally published on 5 March 2023_

Last week, we introduced Rollkit, a modular framework for rollups. Today, we are proud to announce that Rollkit is the first rollup framework to support sovereign rollups on Bitcoin. An early research implementation allows Rollkit rollups to use Bitcoin for data availability.

Rollkit is opening the door for developers to create rollups with arbitrary execution environments that inherit Bitcoin’s data availability guarantees and re-org resistance. With the new integration it is now possible to run the [EVM on Bitcoin as a Rollkit sovereign rollup](/docs/tutorials/bitcoin). Sovereign rollups on Bitcoin not only expand the possibilities for rollups, but also have the potential to help bootstrap a healthy blockspace fee market on Bitcoin, enabling a more sustainable security budget.

## Tl;dr

- Sovereign rollups using Bitcoin for data availability are now a reality with Rollkit’s new early research integration.
- Follow along with a [demo](#evm-on-bitcoin-demo) of the EVM running on Bitcoin as a sovereign Rollkit rollup.
- The implementation was possible due to Bitcoin's Taproot upgrade and Ordinals' usage of Bitcoin for publishing arbitrary data.

## Posting data on Bitcoin with Taproot

On Feb. 1, 2023, the Luxor mining pool mined the largest Bitcoin block (#774628) ever, approximately 4 MB. Most of the blockspace was used to inscribe a Taproot Wizards NFT with [Ordinals](https://ordinals.com/), a project that implements NFTs on Bitcoin by publishing the image data on-chain.

Bitcoin NFTs use Taproot witnesses to inscribe arbitrary data, enabled by Bitcoin's Taproot upgrade. Taproot witnesses provide a slightly better payload-to-data ratio than SegWit transactions. A standard transaction can include up to around 390kB of arbitrary data while still passing through the public mempool. A non-standard transaction, included by a miner directly without passing through the mempool, can include close to 4MB of arbitrary data. In short, with SegWit, it became viable to post big blobs of data to the Bitcoin blockchain.

Since then, the usage of Ordinals for NFT inscriptions and Taproot utilization has [kicked off](https://dune.com/dataalways/ordinals). Eric Wall found that at the time of [his tweet](https://twitter.com/ercwl/status/1619671451417862145), posting data on Bitcoin was 7x cheaper than Ethereum. Now that there are thousands of inscriptions on Bitcoin, it has become clear that sovereign rollups and an ecosystem of dapps on Bitcoin could become a reality. The missing piece: a rollup framework for easily integrating Bitcoin as a data availability layer.

## Integrating Bitcoin as a data availability layer into Rollkit

Rollkit is a modular framework for rollups, where developers can plug-in custom execution layers and data availability layers. Initially, Rollkit only supported Celestia as an option for data availability and consensus. Now, Bitcoin is an option, thanks to an early research implementation of a Bitcoin data availability module for Rollkit. In this case, sovereign rollups manage their own execution and settlement while offloading consensus and data availability to Bitcoin.

![rollkit-bitcoin-rollup](/bitcoin-rollkit/rollkit-bitcoin-1.png)

## How Rollkit posts data to Bitcoin

To write and read data on Bitcoin, we make use of Taproot transactions. To facilitate this, we implemented [a Go package called `bitcoin-da`](https://github.com/rollkit/bitcoin-da) that provides a reader/writer interface to Bitcoin. For details of how the interface works and how it uses Taproot, see [the specs](https://github.com/rollkit/rollkit-btc/blob/main/spec.md). The package can be re-used by any project that wants to read or write data on Bitcoin.

Rollkit was built with modularity at its core. It has a data availability interface so that developers can simply implement specific methods to add a new data availability layer. To add a data availability layer, implementers need to satisfy the `DataAvailabilityLayerClient` interface which defines the behavior of the data availability client, and the `BlockRetriever` interface which defines how blocks can be synced. These interfaces live in the [da package](https://github.com/rollkit/rollkit/tree/main/da). The most important methods in these interfaces are `SubmitBlock` and `RetrieveBlock` for reading and writing the blocks.

After implementing the Taproot reader/writer interface for Bitcoin (`bitcoin-da`), adding it as a data availability module for Rollkit took less than a day. We mostly only had to implement the `SubmitBlock` and `RetrieveBlocks` functions for Rollkit to call the `Read` and `Write` methods in `bitcoin-da`.

![rollkit-bitcoin-rollup-2](/bitcoin-rollkit/rollkit-bitcoin-2.png)

## EVM on Bitcoin demo

Rollkit supports custom execution layers, including EVM, CosmWasm, or the Cosmos SDK. To test the integration, we used Rollkit to run the EVM (using Ethermint) as a sovereign rollup on a local Bitcoin test network. See below for a demo.

<iframe
     title="Rollkit: Ethermint + Bitcoin DA demo"
     src="https://www.youtube.com/embed/qBKFEctzgT0"
     allowfullscreen
  >
</iframe>

## Conclusion

As we move towards a future where sovereign communities will form around different applications, asking them to incur the high cost and overhead of deploying a layer 1 blockchain to be sovereign is not sustainable. [Sovereign rollups](https://blog.celestia.org/sovereign-rollup-chains/) fix this by making it possible to deploy a sovereign chain that inherits the data availability and consensus of another layer 1 chain such as Bitcoin.

Our goal with Rollkit is to make it easy to build and customize rollups. We invite you to play around Rollkit and build sovereign rollups on Bitcoin, or customize Rollkit with different execution environments and data availability layers. For details on how to run Rollkit with the Bitcoin data availability module, see the instructions [here](/docs/tutorials/bitcoin). Keep in mind that the integration is an early research implementation and it is not yet production-ready!

Modularism, not maximalism.
