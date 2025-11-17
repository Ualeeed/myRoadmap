---
DATE: 2025-10-22T00:00:00
DONE: true
Name: Foundation 2
---


# What is DNS

## **Definition**
<mark style="background: #FF5582A6;">DNS</mark> (<mark style="background: #FF5582A6;">D</mark>omain <mark style="background: #FF5582A6;">N</mark>ame <mark style="background: #FF5582A6;">S</mark>ystem) is like the internet's phonebook. It translates human-readable website names (like google.com) into computer-readable IP addresses (like 172.217.14.142) that computers use to find and connect to websites.

## **Why We Need DNS**
Without DNS, you would have to memorize long strings of numbers to visit every website. DNS makes the internet user-friendly by allowing us to type easy-to-remember names instead of complex IP addresses.

## **How DNS Works**

When you type a website address in your browser:

1. **Your Request**: You type "example.com" in your browser
2. **DNS Query**: Your computer asks a DNS server "What's the IP address for example.com?"
3. **DNS Lookup**: The DNS server searches through its records (like looking up a phone number in a phonebook)
4. **Response**: The DNS server returns the IP address (like 192.0.2.1)
5. **Connection**: Your browser uses this IP address to connect to the website's server
6. **Page Loads**: The website appears on your screen

## **DNS Hierarchy**

DNS works through multiple levels of servers:

- **Root DNS Servers**: The highest level - they know where to find all TLD servers
- **TLD Servers**: Manage domain extensions like `.com, .org, .net, .edu`
- **Authoritative DNS Servers**: Store the actual IP addresses for specific domain names

## DNS Caching

To make things faster, DNS information is temporarily stored (cached) on your computer and by your Internet Service Provider. This way, if you visit the same website again, your computer doesn't need to search through all the DNS servers - it already remembers the IP address.

## Key Points

- **DNS translates domain names to IP addresses
- **It works in a hierarchical system with multiple server levels
- **DNS makes browsing the internet much easier and faster
- **The entire lookup process happens in milliseconds
- **Caching helps speed up repeat visits to websites
