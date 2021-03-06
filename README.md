# Gathering Usernames from Google LinkedIn Results using Burp Suite Pro

As part of reconnaissance when performing a penetration test, it is often useful to gather usernames. The usernames may come in handy for performing a [password spraying attack](http://www.blackhillsinfosec.com/?p=4694) for example. One easy way to gather employee names is to use a Burp Suite Pro extension with a little Python script as described below. You can then massage these employee names into any username format. You may be able to discover the username format by analyzing the metadata of documents posted to a company's public web sites as described [here](https://github.com/dafthack/PowerMeta).
To collect employee names with Burp, you'll need to do the following steps.

## Step 1
Install the Python Scripter extension from the **Extender-->BApp** Store tab in Burp Suite Pro

![Python Scripter Extension](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/python-scripter.png)


## Step 2
You may need to download the Jython standalone JAR file and point Burp to it if you have not done that before.

![Jython](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/jython.png)

## Step 3
Copy and paste code from this repo (scrape-google-linkedin.txt) into the newly available "Script" tab. Be sure to copy code from the “Raw” view in BitBucket so that the carriage returns and indentation copy correctly.

![Script Tab](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/pastecode.png)


## Step 4
Configure the Extension to save output to a file. This is where your usernames will be written. You can optionally select the "Show in UI" option, but the output window truncates items when the list gets too long.

![Save Output](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/set-filename.png)


## Step 5
Configure your browser to use Burp as a proxy as you normally would. From the browser, do a Google search of the following form (don't forget the "/in" on the end of "linkedin.com":

site:linkedin.com/in "Company Name"

![Example](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/example2.png)

The script will write the name that shows up before the text " | LinkedIn" or "| Professional Profile - LinkedIn" in the search results to the output file. In this example, it would write "James Lee - Hacker - Black Hills Information Security" and "Derek Banks". Google limits the results to 10 per page. You can click on additional pages of results to get more employee names written to the file.

![Google](https://github.com/clr2of8/Gather-Usernames-From-Google-LinkedIn-Results/raw/master/images/google.png)

You can gather a large list of employee names quickly and easily with this method. Try importing the list to Microsoft Excel where you can use formulas to turn employee names into the appropriate username format such as first initial followed by last name. It is also a good idea to use the "Remove Duplicates" functionality in Excel since the script may export the same employee name multiple times.

## Step 6
When you are done, unload the Python Scripter or erase the script code so you don't burden Burp with inspecting all responses.

