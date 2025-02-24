---
title: How to registering a domain name and create a dns record
date: 2025-02-14 18:17:27
tags:
---

## Prerequisites: 
- A Vultr instance running (with a public IP address).
- Access to your domain registrar's control panel (In this example im using Hostinger).
- SSH or other access to your VULTR instance(ex putty, etc..)

## Step 1: Register a Domain Name
First you need to register a domain name if you haven't already done so. Here are the general steps:
1. Choose a Domain Registrar: Select a domain registrar (eg., Hostinger, goDaddy, etc ..).
2. Search for Available Domain Names: Use the registrar's search tool to find an available domain 
name.
3. Purchase the Domain: Once you've found an avlaiable domain, follow the registrar's checkout
process to purchase it.
4. Access Your Domain Management Console: After purchasing, you'll have access to your domain 
management console where you can configure your DNS settings.

## Step 2: Retrieve the IP Address of Your Vultr Instance 
You will need the public IP address of your Vultr instance to point your domain to it.
1. Log in to Vultr: Go to the Vultr Dashboard and log in.
2. Find Your Instance: Navigate to the "Instances" section, find your instance, and note the public
IPV4 address. 

## Step 3: Configure DNS Records for your Domain 
Now you need to configure the DNS records for your domain. Follow these steps based on your domain
registrar: 
1. login to Your Domain Registrar:
- For example, if you registered your domain on NameCheap, Log in to your Hostinger account.

2. Navigate to DNS Management:
find the section where you can manage DNS setting or DNS records.

3. Add a Record for Your Domain:
You Will add an "A" record to point your domain to your Vultr instance IP address. Here's how to do it:
- Host: @ (or leave it blank, depending on the registrar)
- Type: A
- Value: Your Vultr instance's public IP address(eg., 192.0.2.123)
- TTL: 3600 (Default is usually fine)
