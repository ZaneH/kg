---
title: DeepSeek Coder (6.7B Instruct Q5_1)
date: 03-16-2024
tags: ai, benchmarking, code
---

## deepseek/deepseek-coder

So many variations of this model, it's nice to see. I'm going to start with
something I know will run on my machine: `deepseek-coder:6.7b-instruct-q5_1`.

The most promising thing about this model is that it is trained on instruction
data. This means you can use natural language to prompt the model to write code
for you. With some fine tuning, I expect this model (and its successors) to be
quite useful.

## Setup

```bash
ollama run deepseek-coder:6.7b-instruct-q5_1
>>>
```

## Control Questions

```
>>> Hello, how are you today?
Hello! As an artificial intelligence, I don't have feelings or emotions, but I'm here and ready to assist you with your computer science related queries. How can I help you today?
```

## Task: Complete JSON array

````
>>> """{
...    "houses": [
...      {
...        "address": "123 Wisdom Ln.",
...        "vacant": false,
...        "value": 1250000,
...        "state": "TN"
...      },
...      {"""
It seems like you've started a JSON object for an array of house data. However, your message is cut off prematurely. Could you please complete the details? I'd be happy to help with any 
computer science-related questions you may have about this topic or anything else!


>>> Please finish the JSON object by adding 4 more example houses for my unit test.
Absolutely, here are four additional examples of house objects in a JSON array format:

```json
{
    "houses": [
        {
            "address": "123 Wisdom Ln.",
            "vacant": false,
            "value": 1250000,
            "state": "TN"
        },
        {
            "address": "456 Bravery St.",
            "vacant": true,
            "value": 750000,
            "state": "NC"
        },
        {
            "address": "789 Valor Ave.",
            "vacant": false,
            "value": 1500000,
            "state": "VA"
        },
        {
            "address": "246 Honor Ct.",
            "vacant": true,
            "value": 800000,
            "state": "PA"
        }
    ]
}
```

Each house object in the array contains four properties: `address` (a string), `vacant` (a boolean indicating whether or not the property is vacant), `value` (an integer representing the 
estimated value of the property), and `state` (another string indicating the state where the house is located).
````

I had to re-prompt the model to get the desired output, which in hindsight, makes sense.
The model added only three houses, I guess it thought I wanted four total. It still has
excellent performance compared to [[/code/topics/ai/models/starcoder2|StarCoder2]].

## Task: Complete Python Code

````
>>> """from bs4 import BeautifulSoup as bs
... def scrape_all_links(url) -> list[str]:"""
It seems like your function definition is incomplete. Can you provide more information about what this function should do? For example, how does it request the HTML page and parse it with
Beautiful Soup? Also, can you specify the expected input and output types for your function? This would make it easier to understand the purpose of your function as well as its 
functionality.


>>> Expected input: URL for any website, Expected output: A list of URLs that were found from anchor elements. 
Here is a basic implementation using BeautifulSoup and requests. This scraper will get the HTML content of the page at the given url, parse it with BeautifulSoup to find all `<a>` tags 
(which are used for hyperlinks in HTML), extract the URLs from these tags, and return them as a list:

```python
import requests
from bs4 import BeautifulSoup

def scrape_all_links(url):
    # Send a GET request to the url
    response = requests.get(url)
    
    # If the GET request is successful, the status code will be 200
    if response.status_code == 200:
        # Get the content of the response
        page_content = response.content
        
        # Create a BeautifulSoup object and specify the parser
        soup = BeautifulSoup(page_content, 'html.parser')
        
        # Find all <a> tags in the parsed HTML
        links = soup.find_all('a')
        
        # Extract the href attribute from each link and return them as a list
        urls = [link.get('href') for link in links]
    
        return urls
    else:
        print(f"Failed to get URL {url}. Status code: {response.status_code}")
```
Please note that this is a simple scraper and might not work on all websites due to the different ways they structure their HTML. For more complex tasks, you may need to use other 
libraries or tools such as Scrapy. Also, please ensure that your web scraping activities comply with the website's robots.txt file (found at https://www.example.com/robots.txt) and terms 
of service.
````

Once again, compared to [[/code/topics/ai/models/starcoder2|StarCoder2]], this model is
100% more useful. It's not perfect, but it's a much better starting point. From the
task above, you can see that it asked for more implementation details. This is a good
sign that it's trying to understand the task at hand instead of just generating gibberish.

Out of curiosity, I'm going to test if this code will run as expected...

```bash
$ python ./scrape-href.py
['https://www.google.com/imghp?hl=en&tab=wi', 'https://maps.google.com/maps?hl=en&tab=wl', 'https://play.google.com/?hl=en&tab=w8', 'https://www.youtube.com/?tab=w1', 'https://news.google.com/?tab=wn', 'https://mail.google.com/mail/?tab=wm', 'https://drive.google.com/?tab=wo', 'https://www.google.com/intl/en/about/products?tab=wh', 'http://www.google.com/history/optout?hl=en', '/preferences?hl=en', 'https://accounts.google.com/ServiceLogin?hl=en&passive=true&continue=https://www.google.com/&ec=GAZAAQ', '/advanced_search?hl=en&authuser=0', '/intl/en/ads/', '/services/', '/intl/en/about.html', '/intl/en/policies/privacy/', '/intl/en/policies/terms/']
```

I had to add one line of code to actually execute the function-- but it worked!

## Task: Move files from one directory to another

````
>>> Write me a simple script to move all the files in my current directory to a ~/.hidden-files. Use Python only, be sure to include plenty of comments.
Here's a python script that should do what you asked for. It uses shutil and os modules which are part of standard library so no need to install any additional packages:

```python
import os
import shutil  # shutil module has functions for copying and removing directories, moving files around.

# The directory where we will move the hidden files (~/.hidden-files)
destination_directory = os.path.expanduser("~") + '/.hidden-files'  

# Check if destination directory exists, if not create one
if not os.path.exists(destination_directory):
    os.makedirs(destination_directory)

for filename in os.listdir():  # Loop through each file in the current directory
    if filename.startswith('.'):   # If the filename starts with . it is a hidden file
        shutil.move(filename, destination_directory + '/' + filename)  # Move the file to ~/.hidden-files
```
Please note that this script will not move directories or files that start with `~` (tilde), as these are usually temporary and user specific. Be careful when running scripts like this on
your entire filesystem! Also, make sure you know what you're doing before executing such a script to avoid moving important files accidentally.
````

Bingo, this is a great answer. It creates the destination directory if it doesn't exist.
One flaw is that it's only moving hidden files. Not a big deal. My prompt could
have been better. Not interested in executing this locally.