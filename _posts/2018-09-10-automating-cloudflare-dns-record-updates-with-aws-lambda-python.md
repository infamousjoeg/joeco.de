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

Finally, to the use case: upon Instance State changing to "Running", grab the Instance's public IPv4 address and update a specific A record in Cloudflare's DNS.  

# My Engineered Solution

* Language should be Python. _(My most comfortable language currently.)_
* Any custom functions should be put in a Python module package format for easy distribution later.
* The AWS Lambda function's execution policy should have the following permissions:
  * CloudWatch Logs
  * SNS (_Publish_)
  * EC2 (_EC2ReadOnlyAccess_ IAM Role)
* The Instance State change should be a CloudWatch Event trigger in the function.
* The function should be universally adoptable.  It should make the following variables available to the Python script as Environment Variables:
  * `EC2_INSTANCE_NAME`
  * `CLOUDFLARE_EMAIL`
  * `CLOUDFLARE_API_KEY`
  * `CLOUDFLARE_A_NAME`
  * `CLOUDFLARE_DNS_ID`
  * `CLOUDFLARE_ZONE_ID`
* The function should use the AWS SDK to describe the EC2 instance provided and retrieve the public IPv4 address assigned.
* The function should use Cloudflare's RESTful API to update the specified A record in the DNS & Zone given using the E-Mail and API Key provided for authentication to do so.
