---
title: "[Dev] Lechat - Relational vs NoSQL Databases"
date: 2024-03-30
categories: [Dev, Development]
tags: [Development]
---

## Introduction:

As I embarked on building a chat system, one critical decision awaited me: selecting the right type of database. Relational databases and NoSQL databases were the two contenders. To make an informed choice, I delved into the data types and examined the read/write patterns. In this blog post, I'll share my insights and explain why I ultimately opted for NoSQL databases, specifically key-value stores, when it came to storing chat messages.

## Understanding the Data Types and Read/Write Patterns:

In a chat system, two types of data coexist. The first type encompasses generic data such as user profiles, settings, and user friends lists. These robust and reliable relational databases excel at storing and managing such data. Techniques like replication and sharding ensure availability and scalability.

The second type of data is unique to chat systems: chat history. To make an informed decision, I needed to delve deeper into the specific read/write patterns associated with chat history.

## Enormous Data Volume and Recent Chat Access:

Chat systems handle an enormous amount of data. Facebook Messenger and WhatsApp process a staggering 60 billion messages per day. However, it's important to note that users typically access only recent chats, rarely seeking out older conversations.

## Supporting Random Access and Data Retrieval:

While most users primarily view very recent chat history, they might engage with features that require random access to data, such as search functionality, viewing mentions, or jumping to specific messages. Thus, the chosen data access layer needed to efficiently support these use cases.

## Read-to-Write Ratio and Key-Value Stores:

For 1-on-1 chat apps, the read-to-write ratio stands at approximately 1:1. Considering this, key-value stores emerged as a suitable choice for storing chat messages. Here's why:

- Easy Horizontal Scaling:
    - Key-value stores excel at horizontal scaling, allowing for seamless expansion as the chat system grows. This scalability ensures the system can handle the enormous volume of chat messages without sacrificing performance.

- Low Latency and Swift Data Access:
  - Key-value stores offer exceptionally low latency when accessing data, enabling real-time chat experiences. By minimizing delays, key-value stores contribute to a smooth and responsive user interface.

- Long Tail Data Handling:
    - Relational databases struggle to efficiently handle the long tail of data. As indexes grow large, random access becomes increasingly expensive. Key-value stores, on the other hand, excel at handling such scenarios, ensuring efficient retrieval of data even as the chat history grows.

## Proven Reliability of Key-Value Stores in Chat Applications:

The adoption of key-value stores by reputable chat applications solidifies their credibility. For instance, both Facebook Messenger and Discord rely on key-value stores for their messaging platforms. Facebook Messenger utilizes HBase, while Discord leverages Cassandra. These successful implementations highlight the suitability of key-value stores for chat message storage.

## Conclusion:

After careful consideration of the data types, read/write patterns, and the specific requirements of my chat system, I made the decision to embrace NoSQL databases, particularly key-value stores, for storing chat messages. The scalability, low latency, efficient long tail data handling, and the proven reliability of key-value stores in renowned chat applications solidified my choice. By leveraging the power of NoSQL, I am confident in delivering a robust and performant chat system that meets the demands of modern users.

