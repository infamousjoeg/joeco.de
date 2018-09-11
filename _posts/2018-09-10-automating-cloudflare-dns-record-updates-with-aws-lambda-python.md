---
title: Automating Cloudflare DNS Record Updates with AWS Lambda & Python
thumbnail: /assets/images/cdemoupdatecloudflare-screenshot.png
category: Serverless
tags: 'aws, aws-lambda, python, cloudflare, dns, rest-api'
---
![AWS Lambda Function](/assets/images/cdemoupdatecloudflare-screenshot.png)

# Use Case Explanation

I like to use a very specific domain name when I demo [CyberArk Conjur](https://conjur.org) because it's easier for me to remember and it also looks better to the customer.  Even so, if it doesn't look good to them -- it still looks better to me!

I noticed quickly that when I'd set the public IPv4 address of my [AWS](https://aws.amazon.com) [EC2](https://aws.amazon.com/ec2/) instance that I demo from to an A record for `cdemo.cybr.rocks` in [Cloudflare](https://cloudflare.com)'s DNS, it'd be good for that Instance running.  However, after I stopped the EC2 instance and, eventually, restarted it again, it boots with a different public IPv4 address.

Now, I'm sure I could just use an [Elastic IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) and assign it and call it a day... but that costs money -- even when it's not being used!  I can save money, even over the Elastic IP lease, triggering the [AWS Lambda](https://aws.amazon.com/lambda/) function only when my _Instance State_ changes.

Finally, to the use case: upon a defined Instance's _Instance State_ changing to "Running", grab the defined Instance's public IPv4 address and update a defined [A record](https://support.dnsimple.com/articles/a-record/) in Cloudflare's DNS.  

# My Engineered Solution

* Language should be [Python](https://www.python.org/). _(My most comfortable language currently.)_
* Any custom functions should be put in a [Python module package](https://docs.python.org/2/tutorial/modules.html) format for easy distribution later.
* The function's execution policy should have the following permissions:
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
* The function should use Cloudflare's RESTful API to update the specified A record in the DNS & Zone given using the E-Mail and API Key provided for authentication to do so.  Updating it to the retrieved public IPv4 address.

# How I Did It

## Decomposition

Coming into this phase, I already knew I was doing something that took _way_ too long too many times repeatedly.  Immediately, that triggered my "Automation Senses" -- like Spidey Senses... but less cool... and surprisingly dorkier.  Easily repeatable processes are the GOLDEN RULE when it comes to easy automation.  All that was left was decomposing that easily repeatable process:

* When I start an AWS EC2 Instance, I do the following:
  * Copy the EC2 Instance's public IPv4 address to my clipboard.
  * Browse to <https://cloudflare.com>.
  * Login to my Cloudflare account.
  * Select `cybr.rocks` from the list of domains managed.
  * Select the IP address value of the A record named `cdemo.cybr.rocks` and update it with the public IPv4 address on my clipboard.
