# Welcome to the Khronus Protocol 

# What is the Khronus Protocol

It is very common for computer systems to execute actions not only as a response to user interactions, but also upon specific events. One of the events that very often triggers actions in computer systems is the passage of time. 
Virtually all subscriptions, the flesh and blood of Software as a Service (SaaS) companies, run thanks to the very reliable Linux Job Scheduler, cronjobs.

Blockchain systems lack access to native job schedulers. Each block has a timestamp, assigned by the miner and validated by the protocol, however, it is not the role of the Blockchain protocol to provide a job scheduler based in such timestamps. Smart Contracts then, by design, cannot self execute. 

Without relaying on external parties smart contracts can only be designed to implement time bound constraints, but not schedulers, limiting their flexibility. Since the early days of Ethereum there have been attempts to provide a decentralized technique to implement Job Schedulers, such as the Ethereum Alarm Clock project. This type of projects often required certain effort to customize them to the user's needs, and, also, often involved the deployment of helper contracts, alongside the main contract, to allow customization of alerts at different time intervals for the same contract. 

To put this in context, this would involve in the case of a subscription service, for example, having a master contract to manage subscriptions, but also separate helper contracts, per user, to manage the different subscriptions intervals. 

The Khronus project was born from the need of a reliable, easy to use, decentralized set of tools for the management of time in smart contracts, specially the serving of time related alerts. 

The Khronus Protocol is a set of smart contracts, scheduler servers, and incentives that allows the serving of time related alerts to smart contracts in a decentralized and trustless fashion.

## The Alpha Version

The Khronus Protocol is available in its Alpha Testnet Version in the Mumbai testnet of Polygon starting August 2022.

The purpose of the Alpha version is to refine the Khronus Protocol and interact with the community in order to establish what features are needed the most and prioritize development accordingly.

## What is available

During the Public Alpha the Krhonus Protocol is open to provide client contracts in the Polygon Mumbai testnet with alerts. Use cases for these types of services are contracts such as, parametric insurance, escrow agreements, lending, etc. 

The main characteristic of this type of smart contracts if that they support many parametric insurance policies, escrow agreements, or lending agreements. The Khronus Protocol can provide alerts to expiry each of them, once the original Smart Contract is registered in the protocol. 

Periodic alerts at different timeframes will be available soon to power decentralized cron tabs, such as the ones that are needed to automate applications related to staking and subscription payments. 

During the alpha version all scheduler servers (Khronus Nodes) are operated by the Khronus Project, in the near future the protocol might receive request for joining as an scheduler server operator.

Getting Started 



