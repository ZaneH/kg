---
title: StarCoder2 (15B)
date: 03-16-2024
tags: ai, benchmarking, code
---

## bigcode/starcoder2

> Intended use: The model was trained on GitHub code as well as additional selected data sources such as Arxiv and Wikipedia. As such it is not an instruction model and commands like "Write a function that computes the square root." do not work well.

This immediately caught my attention and makes this model a lot less appealing for many
of the tasks I initially had in mind. I'll still give it a try and see how it performs.

The 15B model is the largest model available and it was trained on "600+ programming
languages and 4+ trillion tokens." It also mentions that the 3B model performs as well
as the 15B model. Might be worth comparing the two in the future.

## Setup

```bash
ollama run starcoder2:15b
>>>
```

## Control Questions

```
>>> Hello, how are you today?
".split()
print(words)

# + [markdown] id="v45c2_iV310w" colab_type="text"
# **Joining** a list of words with a *separator* to make a string.

# + id="j-9p8bP6310x" colab_type="code" outputId="7147526c-e421-414f-cc62-09ef18c61bc9" colab={"base_uri": "https://localhost:8080/", "height": 34}
' '.join(words)

# + [markdown] id="hP016KZJ310z" colab_type="text"
# ### Tuples

# + [markdown] id="yM47p8x93102" colab_type="text"
# A **tuple** is a sequence of immutable Python objects. 
#
# Tuples are sequences, just like lists. The differences between tuples and lists are, the tuples cannot be changed unlike lists and tuples use parentheses, whereas lists use square 
brackets. Creating a tuple is as simple as putting different comma-separated values. Also, any type of object can be stored in a tuple.

# + id="yYd0pSjL3105" colab_type="code" outputId="4b87926f-cb4c-435a-ac9e-055059d0d2f6" colab={"base_uri": "https://localhost:8080/", "height": 34}
# A list of tuples
l = [
    ('a', 1),
    ('b', 2),
]
print(l)


# + id="04Q960n-3107" colab_type="code" outputId="8e1415c7-f27d-46a9-ff4c-f55efca65165" colab={"base_uri": "https://localhost:8080/", "height": 34}
# Let's define a function that returns a tuple
def sum_and_product(x, y):
    return (x + y),(x * y)
sp = sum_and_product(2, 3) # sp is (5, 6)
print(sp)


# + [markdown] id="g9nRZ2rU310-"
```

Went ahead and cut it short because it is clearly speaking gibberish. Next, let
me try to have it complete a JSON array. The lines prefixed with `...` are the
input and the lines without are the output.

## Task: Complete JSON Array

```
>>> """{
...   "houses": [
...     {
...       "address": "123 Wisdom Ln.",
...       "vacant": false,
...       "value": 1250000,
...       "state": "TN"
...     },
...     {"""

       "address": "89 Battery Ave",
       "vacant": true,
       "value": null,
       "state": "CA"
    }
   ]
}

# Introduction to JavaScript

JavaScript is the world's most popular programming language. It powers everything from the small, user-driven scripts that add a little flare and interactivity to your website to large, 
server-side applications that can make full use of thousands of open source libraries and frameworks.

Whether you're an experienced programmer looking for some new challenges or a complete beginner wanting to learn how to build web applications, this is the guide for you. Whether you 
write programs in JavaScript on your own time as a hobby or at work, we can help get you up to speed with all of the essential concepts and tools you'll need.

## What's new about JavaScript?
```

What I noticed is that it only added one new house and then started talking about
JavaScript in markdown syntax. Seems like this model is more than happy to switch
between languages with a preference for markdown. I suspect this is due to the
limited context I've provided for input.

## Task: Complete Python Code

```
>>> """from bs4 import BeautifulSoup as bs
... def scrape_all_links(url) -> list[str]:"""

    html_doc = requests.get(url).text
    soup = bs(html_doc, 'lxml')

    links = []
    for link in soup.find_all('a'):
        href = link.get('href')

        if href is not None:
            try:
                if 'wikipedia.org' not in urlparse(href).netloc:
                    continue
                if '#' == urlparse(href).fragment:
                    continue

                links.append(urljoin(url, href))

            except Exception as ex:
                print('Error with link:', ex)

    return links


def get_links(url):
    html_doc = requests.get(url).text
    soup = bs(html_doc, 'lxml')
    for link in soup.find_all('a'):
        href = link.get('href')

        if href is not None:
            try:
                if 'wikipedia.org' not in urlparse(href).netloc:
                    continue
                if '#' == urlparse(href).fragment:
                    continue

                yield urljoin(url, href)

            except Exception as ex:
                print('Error with link:', ex)

[!! snipped out the rest !!]

    return min(numbers)



if __name__ == '__main__':
    print('1:', get_min("test"))
    print('2:', get_min(None))
    print('3:', get_min([]))
    print('4:', get_min(['test']))
import sys


def main():
    print('Hello world')



if __name__ == '__main__':
    main()# https://www.youtube.com/watch?v=w87j4806&list=PLA00FEB1470CDE8D2&index=23
from typing import List


def sum_array(numbers: List[int]) -> int:
    if not numbers:
        return 0

    # print('Numbers:', numbers)
    return numbers.pop() + sum_array(numbers)




def main():
    result = sum_array([1,2,3])^C
```

Once again, I just had to Ctrl+C out of it. From my experience so far, it doesn't
seem to use stop tokens either. In the output above, it tried to create lots of
main functions as if it were writing multiple programs. Not really sure what this
model is good for at the moment. Maybe it would do better once fine-tuned.
Moving on for now.