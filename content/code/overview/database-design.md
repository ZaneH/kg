---
title: Database Design
tags: database, orm, relational
date: 08-26-2023
---

Database design is the process of producing a detailed data model of a database. This data model contains all the necessary data structures and constraints required to store, manage and access the data in the database. This data is typically accessed from the [[code/overview/backend-web-development|backend]] of an application.

When designing a database, the first question is what type of database to use. There are two main types of databases: relational and non-relational.

## Relational Databases

Relational databases are the most common type of database. They store data in tables that are linked to each other using relationships. Each table contains a set of columns and rows. The columns represent the attributes of the data and the rows represent the data itself.

Designing an effective relational database requires a good understanding of the data and how it will be used. The process of designing a relational database is called database normalization. This process involves breaking down the data into its smallest logical parts and then organizing it into tables that are linked together using relationships.

A well designed relational database is designed both to protect the data and to make the database more flexible by eliminating redundancy and inconsistent dependency.

>[!note]
>Examples of relational databases include PostgreSQL, MySQL, Oracle, Microsoft SQL Server, etc.

## NoSQL Databases

NoSQL databases are a type of database that does not use the relational model. They are designed to store large amounts of data in a flexible way. They are often used for storing unstructured data such as documents, images, videos, etc. They are also used for storing data that is not easily represented in a relational database such as graphs, trees, etc.

>[!note]
>Examples of NoSQL databases include MongoDB, CouchDB, Redis, etc.

## Object Relational Mapping (ORM)

ORMs are an extremely helpful tool for interacting with databases. They aren't required, but they make it much easier to work with databases. They allow you to interact with the database using objects instead of SQL queries. This makes it much easier to write code that is easy to read and maintain.

ORMs are also useful for abstracting away the differences between different database systems. This allows you to write code that works with multiple database systems without having to worry about the differences between them.

## Honorable Mentions

These are some tools that have made my life easier when working with databases. Prisma has its drawbacks, but it's still a great tool and continues to improve.

- [Prisma](https://www.prisma.io/) - Popular ORM for Node.js and TypeScript.
- [Postico](https://eggerapps.at/postico/) - PostgreSQL client for macOS.
- [Ecto](https://hexdocs.pm/ecto/Ecto.html) - ORM for Elixir and PostgreSQL.
- [Redis](https://redis.io/) - In-memory data structure store.