---
title: XML for PowerShell Configs
header:
  teaser: /assets/images/powershell.jpg
  thumbnail: /assets/images/powershell.jpg
excerpt_separator: <!--more-->
categories:
  - Coding
  - PowerShell
tags:
  - powershell
  - xml
  - example-code
---

{% raw %}![XML for PowerShell Configs]({{ site.url }}{{ site.baseurl }}/assets/images/powershell.jpg){% endraw %}

I've really taken a liking recently to using XML files for storing configuration values for my PowerShell scripts.  Most times, I do it to make it a "one-stop shop" for updating config values.
<!--more-->

I create a lot of scripts for people who may not have the most experience when it comes to reading code.  It's definitely easier to say, "Update config.xml and don't worry about changing anything in the PowerShell script."  Most people will look at a PowerShell script and go cross-eyed... _this_ prevents _that_.

I decided since I like it so much, I'm going to show you how it's done.  It's a lot easier than I was expecting it to be... check this out:

1. Create a new XML file called `config.xml`.
2. Add the following information to it:
   ```xml
   <?xml version="1.0"?>
   <Settings>
       <Name>Joe Garcia, CISSP</Name>
       <Website>https://joeco.de</Website>
   </Settings>
   ```
3. Create a new PowerShell script in the same directory called `XMLConfig.ps1`.
4. Add the following information to it:
   ```powershell
   # Import XML Configuration Settings
   [xml]$ConfigFile = Get-Content "config.xml"
   
   # Write to host the stored Name and Website
   Write-Host $ConfigFile.Settings.Name
   Write-Host $ConfigFile.Settings.Website
   ```
   
   In the above script, we're importing `config.xml` into the variable `$ConfigFile`.  Afterwards, we're sending the values of the `Name` and `Website` sections of the XML file to the PowerShell Console host.

In just 4 easy steps, you've created your own XML Configuration file to use along side your favorite PowerShell scripts going forward!
