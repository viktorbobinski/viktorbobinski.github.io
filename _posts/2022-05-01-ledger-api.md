---
title: "LedgerAPI"
layout: post
categories: media
---

![LedgerAPI usage](/assets/ledger.JPG)

A very small SpringBoot application using Spring Data, Spring Web, Thymeleaf & H2 Database dependencies. 

[LedgerAPI on Github](https://github.com/viktorbobinski/Ledger-API)


## Stack

A very small SpringBoot application using Spring Data, Spring Web, Thymeleaf & H2 Database dependencies. 

## What is it

The ledger is an API + DB which keeps track of transactions between 2 people and displays them. +/-value transactions are added by posting @RequestParam title and value, date gets added automatically.

## How it works

There are 2 endpoints: 
- /ledger get - read the whole ledger until now
- /ledger post - add a new transaction to the ledger

## What I've learned

- Create a SpringBoot application with different dependencies using Spring Initializr (start.spring.io)
- Use SpringBoot's Model-View-Controller structure pattern
- Create Get/Post endpoints using Spring Web and + receive html parameters
- Manipulate and show templates in Thymeleaf
- Use annotations and repository class to persist an instance of Ledger class in a H2 database using Spring Data (Hibernate)

## Pictures

A Thymeleaf html template is displayed on /ledger:

![LedgerAPI app](/assets/ledger-html.JPG)
