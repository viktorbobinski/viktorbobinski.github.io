---
title: "LedgerAPI"
layout: post
categories: media
---

![LedgerAPI usage](/assets/ledger.JPG)

[LedgerAPI on Github](https://github.com/viktorbobinski/Ledger-API)


## Stack

A very small SpringBoot application with Spring Data, Spring Web, Thymeleaf & H2 Database dependencies. 

## What is it

The ledger keeps track of transactions between 2 people. +/-value transactions are added by posting @RequestParam title and value, date gets added automatically.

## How it works

There are 2 endpoints: 
- /ledger get - to get the whole ledger until now
- /ledger post

## What I've learned

- Create a SpringBoot application with different dependencies with Spring Initializr (start.spring.io)
- Model-View-Controller and how it works in Spring Web
- Get/Post endpoints in Spring Web and receiving html parameters
- Create templates in Thymeleaf
- Use annotations and repository class to persist an instance of Ledger class in a H2 database using Spring Data (Hibernate)

## Pictures

A Thymeleaf html template is displayed on /ledger:

![LedgerAPI app](/assets/ledger-html.JPG)
