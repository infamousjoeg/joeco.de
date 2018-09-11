---
title: Automating Cloudflare DNS Record Updates with AWS Lambda & Python
thumbnail: /assets/images/cdemoupdatecloudflare-screenshot.png
category: Serverless
tags: 'aws, aws-lambda, python, cloudflare, dns, rest-api'
---
![AWS Lambda Function](/assets/images/cdemoupdatecloudflare-screenshot.png)

I like to use a very specific domain name when I demo CyberArk Conjur because it's easier for me to remember and it also looks better to the customer.  Even so, if it doesn't -- it still looks better to me!

I noticed that when I'd set the public IPv4 address of my EC2 instance to an A record for cdemo.cybr.rocks, it be great for that session.  However, the second I stopped the EC2 instance -- when I started it again, it boots with a different public IPv4 address.  Now, I'm sure I could just use an Elastic IP and assign it and call it a day... but that costs money!  I can still save money running the AWS Lambda instead of ponying up for an Elastic IP even if I don't use the instance that month.
