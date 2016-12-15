---
layout: page
title: Information Security Guidelines
permalink: /information-security/
published: true
---

## Introduction

Information and processes managed within IT systems can be exposed to threats that would undermine confidentiality, integrity and availability. The guidance 
throughout this document highlights common pitfalls and strategies to minimise an IT systems vulnerability footprint and ensure reliable performance. 
A common problem with security controls is that they often make systems less convenient or more difficult to use.  When usability is an issue, 
many users will attempt to circumvent security controls; for example, if passwords must be long and complex, users may write them down. 
Balancing security, functionality, and usability is often a challenge.  The goal should be to strike a proper balance: provide a reasonably secure solution 
while offering the functionality and usability that users require.

## Scope

This document is targeted at technical specialists involved in the design, build or acquisition of IT systems for Parks and Wildlife. It aims to provide a 
collection of best practices that will help technical specialists implement reliable and secure systems.

## Confidentiality

Confidentiality refers to protecting information from being accessed by unauthorized parties. In other words, only the people who are authorized to do so can gain access to sensitive data.

### 1. Disallow eavesdropping

Encrypt information in transit and at rest (use SSL/RDP, AWS RDS, Bitlocker)

### 2. Prevent impersonation

Centralised identity management (SSO), multifactor for privileged access 

## Integrity

Integrity refers to ensuring the authenticity of information - that information is not altered or corrupted, and that the source of the information is genuine.

### 1. Take regular backups

Local block device snapshots, remote copies for DR, test

### 2. Tamper protection

Digitally sign important information and archives, use centralised data repositories (e.g. databases, file services)

## Availability

Availability means that information is accessible by authorized users from wherever they require it.

### 1. Reliability engineering

Quick restoration procedures from backups

### 2. Eliminate single points of failure

Design stateless systems (avoid storing state information on application servers) - best practice separate files and databases from your application code/environment.

### 3. Monitor and maintain

Ensure components of your system are continually monitored, and maintained when e.g. database tables get large or filesystems get full.

### 4. Keep systems updated

Make sure the hardware and software supporting a system are always up to date and have appropriate support.

## References

 * [Mozilla Information Security Basics - Confidentiality, Integrity and Availability](https://developer.mozilla.org/en-US/docs/Web/Security/Information_Security_Basics/Confidentiality,_Integrity,_and_Availability)
