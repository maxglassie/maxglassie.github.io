---
layout: post
title:  "80/20 Blockchain: The Key Concepts"
date:   2017-09-11 10:35 -0600
tags:
    -blockchain
    -blockchain as infrastructure
    -blockchain key concepts
---

What is blockchain? Why are so many people talking about it?

There's a lot of hype about this technology right now. It makes it difficult to cut through the noise and figure out what really matters.

I'm not an expert, but I've been researching this technology in order to distill the key concepts. I am simplifying things quite a bit here.

My general strategy is to provide a model for understanding blockchain and then layer on a new model that helps us get closer to the reality.  


## The Wild West
First, a few disclaimers. It's clear that much of the hype is because there's a "get rich quick" vibe in this space. I'm not going to address cryptocurrency or "initial coin offering" speculation except to say that it is exactly that -- speculation. Investing in a volatile space means both high risk and high reward. Speculate at your own risk. Beware of FOMO, that trickster driver of stock bubbles and lost fortunes.  

Blockchain is the Wild West right now. The analogy is apt. It's difficult to say definitively where this technology is heading. It's difficult to say where it is now. In the spirit of Kevin Kelly, _it is possible_ to identify potentialities.

[image]

## Definition: A Blockchain is a Distributed Ledger

In that spirit, let's start with a definition: a blockchain is a distributed ledger.

![Distributed Ledger](/static/img/blockchain_plain.jpg)

Basically, it's a distributed Excel spreadsheet. Each node keeps a full copy of the spreadsheet.

![Distributed Ledger](/static/img/blockchain_excel_spreadsheet.png)

There are three key distinguishing characteristics of blockchain.

1. Consensus: Each node in the network maintains the same spreadsheet. All the nodes are in sync, responsible for storing the same data. In other words, it's intentionally repetitive.  

2. Distributed: The blockchain is distributed across many nodes, which are all running the blockchain protocols.

3. Trustless: This means that the network requires little trust between actors. It's a confusing term, but the key idea is that "trustless" means it requires zero or little trust is required between users of the blockchain.

All things come in threes but there's one more to highlight:

**Data stored on the blockchain is immutable**. This means it cannot be changed or over written. Once a transaction is recorded on the blockchain it cannot be changed and it is stored forever.

## Who Cares About A Ledger?
I'm not an economics guy. I don't know much about accounting but it's in this realm where blockchain has important implications.

It took me a little while to wrap my head around this piece. A ledger is a way of storing data about transactions.

![ledger](/static/img/ledger.jpg)

Say I transfer $100 from my bank account to my friend's bank account. My bank says, "We will subtract $100 from your balance and tell the your friend's bank to add $100 to their balance. The books will record that money moved from this account to the other account." This is recorded as a transaction.

The key point is here is that the ledger is the fundamental tool that we use to store and transfer value. In the previous example, ownership of $100 is transferred by updating the records about who owns that money. The distinction with blockchain is that it does not require a centralized authority, like a bank, to validate the transfer of value. It can maintain an accurate ledger without needing to trust an institution.


## Blockchain As Infrastructure: A Protocol That Transfers Value

Kirk Dameron gave a [presentation](https://www.meetup.com/Ethereum-Denver/events/239018434/) at a Denver blockchain MeetUp where he said that a good way of understanding this technology is "blockchain as infrastructure."

![ledger](/static/img/infrastructure.jpg)

As a distributed ledger, blockchain is a protocol that can transfer and store value. We can think of blockchain like roads. Roads are not inherently interesting. They're a means for moving things around. But without this infrastructure, many interesting things cannot happen as easily, like going to my friend's house or shipping a package from a business to their customer.  


## Another Boring Protocol: Hyper Text Transfer Protocol

If you're thinking that a protocol that can transfer value is boring, then I'm on the right track with this article. There's another boring protocol that serves as infrastructure and we're using it right now. Hyper Text Transfer Protocol - HTTP - is the foundation of the internet. All it does is transfer text around.

![http](/static/img/http.jpg)

Blockchain is a new layer of infrastructure that can work with and augment the existing HTTP infrastructure but with one mind bending difference - it can transfer value, not just text.

## Okay Dude But What About Being A Bitcoin Bajillionaire?
Right, so I haven't talked about cryptocurrency at all, except to say that investing in it is speculative. Blockchain as a technology enables and implements a cryptocurrency. A cryptocurrency in turn is worth value because there is a system in place that cryptographically ensures that the currency will be scarce.

![cryptocurrency](/static/img/cryptocurrency.jpg)

As an economist will tell you, scarcity is the basis for value. The classic example is that if suddenly the market is flooded with billions more diamonds, they will no longer be nearly as valuable. The price will drop dramatically. The same is true of the U.S. dollar or gold or Bitcoin.  

I won't go into the details here, but currently blockchain enforces scarcity in cryptocurrency through a system called "proof of work." The key idea is that it is not possible to simply create new unit of a cryptocurrency at will, like I might copy a PDF or a computer program, because to "generate" new units of currency requires significant computational resources that cannot be faked.

## Smart Contracts: Programming The Blockchain

The most famous blockchain implements and enables a cryptocurrency called Bitcoin. This blockchain has limited ability to do anything else beyond recording transactions of Bitcoin. It's a tremendously valuable function to serve, but the design is limited. Those limitations are a good thing for Bitcoin.

But there is another blockchain technology called Ethereum which enables a programming language that can interact with and execute computations on the blockchain. This enables programmers to write "smart contracts."

![ethereum](/static/img/ethereum.png)

A good example of a smart contract is an old school soda machine. It represents a contract that the machine executes automatically, something like this.

"If I put 10 cents into the machine and press the button, it will dispense a soda."

"If I put 5 cents into the machine and press the button, it will not dispense a soda."

![soda machine](/static/img/soda_machine.jpg)

Programmers can write "smart contracts" that can execute similar and more complex contractual relationships between entities automatically. For example, automatically buying and selling energy on a power grid.

Pillsbury law wrote an interesting piece on [smart contracts](https://www.pillsburylaw.com/en/news-and-insights/recognition-of-smart-contracts.html)

## The Key Take Away of Smart Contracts: We Can Build Apps!

Roads may not be especially interesting. But they enable the development of economic ecosystems. Think about a building downtown. It is a hub of economic activity - money and people flow into and out of the space. It might provide an office for a company or a cool space for a restaurant. Without roads, it would be much more difficult to create that ecosystem.   

The exciting part about smart contracts is that like traditional programming languages enable us to build applications on top of the infrastructure of the internet, programming languages on the blockchain enable us to build applications on top of the blockchain infrastructure.


#### if blockchain = infrastructure then apps = buildings

![infrastructure](/static/img/infrastructure.jpg)

Looking at the picture, we can see the flow of cars and traffic around buildings, which are hubs of activity. Like these roads enable the flow of goods, people, and materials into and out of cities, smart contracts enable the flow of value into and out of applications.

## Vision and Philosophy: Power to the People

![power to the people](/static/img/power_to_people.jpg)

If you start getting involved in the technology and exploring the community, it's good to know that there is a philosophy driving the space.

That philosophy is tends to be libertarian in nature and distrustful of centralized authorities. Many believe that peer-to-peer distributed databases that are immutable and able to transfer value hold the promise to limit the power of these centralized systems.

For example, the goal to create a new form of ["digital gold"](https://en.wikipedia.org/wiki/Nick_Szabo) which did not require, like fiat currency does, the backing of a centralized authority like the Federal Reserve Bank was a driving force behind the development of cryptocurrencies.

There are broad uses for blockchain beyond these and there are many people who think blockchain technologies can have a great positive [social impact](https://www.blockchainforsocialimpact.com/).

##### Additional Resources

[McKinsey - How Blockchain Could Change the World](http://www.mckinsey.com/industries/high-tech/our-insights/how-blockchains-could-change-the-world)

[Ethereum Denver Meetup](https://www.meetup.com/Ethereum-Denver/)

[How Blockchain Could Help Emerging Markets Leap Ahead](https://hbr.org/2017/05/how-blockchain-could-help-emerging-markets-leap-ahead)

[Blockchain for Social Impact](https://www.blockchainforsocialimpact.com/)

[Blockchain Basics: Introduction to Distributed Ledgers](https://www.ibm.com/developerworks/cloud/library/cl-blockchain-basics-intro-bluemix-trs/index.html)
