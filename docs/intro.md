---
sidebar_position: 1
sidebar_label: Introduction
description: Intro to Rollkit, a modular framework for rollups.
---

# Introduction to Rollkit

Welcome to Rollkit docs. We're happy you made it here!

Our mission is to empower developers to quickly innovate and create entire new classes of rollups with minimal tradeoffs.

We're setting the bar high for developers' flexibility and ability to customize rollups however they see fit.

:::tip Tip
If you're familiar with Rollkit, you may want to skip to the [tutorials section](../category/tutorials)
:::

## What is Rollkit?

Rollkit is a rollup framework that gives developers the freedom to deploy rollups throughout the modular stack, opening new possibilities for rapid experimentation and innovation.

The Rollkit framework features a modular node that can run rollups and expose an **[ABCI](https://github.com/informalsystems/tendermint/tree/main/abci)**-compatible client interface, which can be used as a substitute for Tendermint in any ABCI-compatible blockchain application.
By default, the node utilizes Celestia as the Data Availability (DA) layer. In the future, the node will be able to connect to any DA layer of choice.

In addition to deploying sovereign app-rollups, Rollkit can also be used to deploy rollups on existing settlement and execution layers, or even to create a new settlement layer.
The framework's strength lies in its flexibility, allowing developers to customize their rollups as per their requirements.

Rollkit is built as an open-source framework, so that developers could easily import existing modules into their applications.
We encourage developers to contribute to the development of Rollkit modules by adding new ones or improving existing ones.

Our goal is to empower developers to quickly innovate and create new classes of rollups with minimal trade-offs.

Our goal is to make deploying a new chain as easy as deploying a smart contract!

## What problems is Rollkit solving?

### 1. Scalability and Customizability

Deploying your decentralized application as a smart contract on a shared blockchain has many limitations. Your smart contract has to share computational resources with every other application, so scalability is limited.

Plus, you’re restricted to the execution environment that shared blockchain uses, so developer flexibility is limited.

### 2. Security and Time to Market

App-chains might sound like the perfect solution for the problems listed above. While it’s somehow true, deploying a new layer 1 chain presents a complex set of challenges and trade-offs for developers looking to build blockchain products.

Deploying a new layer 1 requires significant resources, including time, capital, and expertise, which can be a barrier to entry for some developers.

In order to secure the network, developers must bootstrap a sufficiently secure set of validators, incurring the overhead of managing a full consensus network. This requires paying validators with inflationary tokens, putting the business sustainability of the network at risk. A strong community and network effect are also critical for success, but can be challenging to achieve as the network must gain widespread adoption to be secure and valuable.

Also, in a potential future with millions of app-chains, it’s highly unlikely all of those chains will be able to sustainably attract a sufficiently secure and decentralized validator set.

## Why Rollkit?

Rollkit solves the challenges encountered during the deployment of a smart contract or a new layer 1, by minimizing these tradeoffs through the implementation of rollups.

With Rollkit, developers can benefit from:

- **Security**:
Rollups inherit security by posting blocks on a secure DA layer. Rollkit reduces the trust assumptions placed on sequencers by allowing full nodes to fetch and compare the blocks posted by the sequencer to the blocks gossiped by the sequencer. In case of fraudulent blocks, full nodes can generate fraud proofs, which they can share with the rest of the network, including light nodes. Our roadmap includes the ability for light clients to receive and verify fraud proofs, so that everyday users can enjoy high security guarantees.

- **Scalability:**
Rollkit rollups are deployed on specialized data availability layers like Celestia, which directly leverages the scalability of the DA layer. As more users join the network and run light nodes, modular blockchains like Celestia become more scalable, eliminating the risk of decreased scalability with increased adoption.

- **Customizability:**
Rollkit is built as an open-source, modular framework, to make it easier for developers to use existing modules and customize their rollups. There are no constraints on the type of virtual machine that can be used, the programming language for creating applications, the state proof type (zk- vs. fraud-proofs), or any other part of the stack. Making Rollkit rollups fully customizable. We're currently working on further abstractions and enhancing the ABCI compatibilities.

- **Faster Time to Market:**
Rollkit eliminates the need to bootstrap a validator set, manage a consensus network, incur high economic costs, and face other trade-offs that come with deploying a new layer 1. Rollkit's goal is to make deploying a rollup as easy as it is to deploy a smart contract, cutting the time it takes to bring blockchain products to market from months or even years to just minutes.

- **Sovereignty**: Rollkit also enables developers to build sovereign app-rollups for cases where communities require sovereignty. This possibility is provided to meet these needs.

## How can you use Rollkit?

As briefly mentioned above, Rollkit could be used in many different ways. From sovereign app-rollups, to settlement layers, and even to L3!  

### Roll with Any Virtual Machine

Rollkit gives developers the flexibility to use pre-existing ABCI-compatible state machines or create a custom virtual machine tailored to their rollup needs. Rollkit does not restrict the use of any specific virtual machine, allowing developers to experiment and bring innovative dapps to life.

### App-Specific Rollup with Cosmos-SDK

Similarly to how developers utilize the Cosmos-SDK to build a sovereign L1, the Cosmos-SDK could be utilized to create a Rollkit-compatible app-rollup.
Cosmos-SDK has great [documentation](https://docs.cosmos.network/main) and tooling that developers can leverage to learn.

Another possibility is taking an existing L1 built with the Cosmos-SDK and deploying it as a Rollkit rollup. This can provide a great opportunity for experimentation and growth.

### Build a Settlement Layer

Settlement layers are ideal for developers who want to avoid deploying sovereign app-rollups. They provide a platform for rollups to verify proofs and resolve disputes.
Additionally, they act as a hub for rollups to facilitate token transfers and liquidity sharing between rollups that share the same settlement layer.
Think of settlement layers as a special type of execution layer.

For more information on how they work, check out this [page](https://celestia.org/learn/modular-settlement-layers/settlement-in-the-modular-stack) on settlement layers by Celestia Labs.

## When can you use Rollkit?

As of today, Rollkit is still in the MVP stages. The framework currently provides a centralized sequencer, an execution VM (ABCI and Cosmos SDK) and a connection to a data availability layer (Celestia).

We’re currently working on implementing many new and exciting features like light nodes and state fraud proofs.

Head down to the next section ([Rollkit Stack](./rollkit-stack.md)) to learn more about what’s coming for Rollkit. If you're ready to start building, you can skip to the [Tutorials](../category/tutorials) section.

Spoiler alert, whichever you choose, it’s going to be a great rabbit hole!
