It is very common for computer systems to execute actions not only as a response to user interactions, but also when triggered by specific events. 
One of the events that very often triggers actions in computer systems is the passage of time. 
Virtually all subscriptions, the blood of Software as a Service (SaaS) companies, run thanks to the very reliable Linux Job Scheduler cron jobs.

Blockchain systems lack access to native job schedulers. Each block has a timestamp, assigned by the miner and validated by the protocol, however, it is not the role of the Blockchain protocol to provide a job scheduler based in such timestamps. Smart Contracts then, by design, cannot self execute. 

Without relaying on external parties, smart contracts can only be designed to implement time boanded constraints, not triggers, limiting their flexibility.
Since the early days of Ethereum there have been attempts to provide a decentralized technique to implement Job Schedulers, such as the Ethereum Alarm Clock project. This type of projects often required certain effort to customize them to the user's needs, and, also, often involved the deployment of helper contracts, alongside the main contract, to allow customization of alerts at different time intervals for the same contract. 

To put this in context, this would involve in the case of a subscription service, for example, having a master contract to manage subscriptions, but also a separate helper contract, per client, to manage the different subscriptions intervals. 

The Khronus project was born from the need of a reliable, easy to use, decentralized set of tools for the management of time in smart contracts, specially the serving of time related alerts. 



