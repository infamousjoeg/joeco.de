---
title: Automating Cloudflare DNS Record Updates with AWS Lambda & Python
thumbnail: /assets/images/cdemoupdatecloudflare-screenshot.png
category: Serverless
tags: 'aws, aws-lambda, python, cloudflare, dns, rest-api'
---
![AWS Lambda Function](/assets/images/cdemoupdatecloudflare-screenshot.png)

# Use Case Explanation

I like to use a very specific domain name when I demo CyberArk Conjur because it's easier for me to remember and it also looks better to the customer.  Even so, if it doesn't -- it still looks better to me!

I noticed that when I'd set the public IPv4 address of my EC2 instance that I demo from to an A record for cdemo.cybr.rocks, it be good for that session.  However, after I stopped the EC2 instance and, eventually, restarted it again it boots with a different public IPv4 address.

Now, I'm sure I could just use an Elastic IP and assign it and call it a day... but that costs money -- even when it's not being used!  I can save money, even over the Elastic IP lease, running the AWS Lambda only when my Instance State changes.
