---
layout: post
title: Python - Selenium vs Urllib
---
Recently, I started a project to scrape data from a web-based database using Python. I am a beginner to Python, with the enough knowledge to run Hello World though. Along with the development of this project, I have learned many things in Python, and One of them is the difference between using Selenium and using Urllib for website access.

When start to implement this project, the very first thing I need to figure out is how to access the website in code and retrieve the HTML codes contain the interested data. With a few clicks on Google, I saw the urllib library, which looks like exactly the one I am looking for. But after some play around, I found that I cannot really access the data sites and retrieve HTML codes with it. After some research, I figured out two things that stop me from making it through.
1. URL redirection. The data sites are not public, and the URL I can start with will actually be redirected at some point before entering into the actual data sites
2. Dynamic URL. When navigating among those data sites, the different URLs are generated programmatically in JavaScript code, they are not static URLs and I won't have them when I call urllib.open()

With these situations in mind, I continued to search and I found the Selenium library, which basically can simulate the web browser to navigate among websites and also take actions on websites, such as clicking on links, refreshing pages, opening or closing a new tab in the browser. So, by using Selenium, URL redirection and dynamic URLs won't be problems anymore.

From my understanding at this point, urllib is more like an HTTP tool for users to request and get response from the web page. If you are accessing pages with no redirection and you don't need to take actions on the page, then urllib would be a perfect tool to use, it's lightweight and simple to use. For selenium, it's not only used for web site access, it also has many other powerful features to help interact with web pages, such as extracting HTML elements, inserting javascript codes. And in order to use it, you also need to have browser driver on your machine.