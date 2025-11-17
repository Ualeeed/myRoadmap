---
DATE: 2025-10-22T00:09:00
DONE: true
Name: Foundation 2
---


# **URL (Uniform Resource Locator)

## Definition

A <span style="color:rgb(20, 192, 255)">URL</span> (<span style="color:rgb(20, 192, 255)">U</span>niform <span style="color:rgb(20, 192, 255)">R</span>esource <span style="color:rgb(20, 192, 255)">L</span>ocator) is the complete web address you type in your browser to visit a website. It's like a street address for websites - it tells your browser exactly where to find a specific page or file on the internet.

## URL Structure

A typical URL looks like this:
https://www.example.com:443/blog/article.html?id=123#section2

Let's break down each part:

### 1. Protocol (https://)
- Tells the browser HOW to retrieve the information
- Common protocols:
  - **HTTP** - Standard web protocol
  - **HTTPS** - Secure version (encrypted)
  - **FTP** - For file transfers
  - **mailto** - For email links

### 2. Subdomain (www)
- Optional section before the main domain
- Can be: www, blog, shop, mail, etc.

### 3. Domain Name (example.com)
- The unique name of the website
- Consists of:
  - **Second-level domain**: example
  - **Top-level domain (TLD)**: `.com, .org, .net, .edu`

### 4. Port (:443)
- Usually hidden from view
- Default ports: 80 for HTTP, 443 for HTTPS

### 5. Path (/blog/article.html)
- Points to a specific page or file on the website
- Like folders and files on the server

### 6. Query Parameters (?id=123)
- Extra information sent to the page
- Used for searches, filters, or tracking
- Starts with `?` and uses `&` to separate multiple parameters

### 7. Fragment (#section2)
- Points to a specific section within a page
- Like jumping to a bookmark on the page

## Simple Examples

1. **https://google.com - Just protocol and domain
2. **https://www.wikipedia.org/wiki/Computer - With subdomain and path
3. **https://youtube.com/watch?v=abc123 - With query parameters
4. **https://example.com/page#contact - With fragment

## How URLs Work

1. You type a URL in your browser
2. DNS translates the domain name to an IP address
3. Your browser connects to that server
4. The server finds and sends back the requested page
5. Your browser displays the page

## Absolute vs Relative URLs

**Absolute URL**: https://example.com/blog/post1.html (full address)
**Relative URL**: /blog/post1.html (assumes you're already on example.com)

## Key Points

- *URLs are the complete addresses for web resources
- *Each part of a URL has a specific purpose
- *Protocol defines how data is transferred
- *Domain name identifies the website
- *Path specifies which page or file to load
- *URLs make it easy to share and access web content
