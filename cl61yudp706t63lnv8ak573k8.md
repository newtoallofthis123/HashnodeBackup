# Coding Your First CLI

Just so you know, I love CLI's. I love the terminal and the experience it offers. Working in the Terminal might seem complex for beginners, but once you get the gist of it, you will not leave it, and I am here to help you not leave the terminal. There are many good terminal cli's already written and are quite popular in the community. The terminal community is actually quite good and helpful. If you are not interested in coding your own cli, but want some good ones, check out the awesome cli list on github, linked below.
[![agarrharr/awesome-cli-apps - GitHub](https://gh-card.dev/repos/agarrharr/awesome-cli-apps.svg)](https://github.com/agarrharr/awesome-cli-apps)

## Why Build One on your own
Okay, honestly, the only reason to build one on your own is the raw customization option it gives. You would also be building what you use. You can customize it the way you like, set up an installer the way you like and the possibilities are endless. Plus, it is quite easy. Check out the basic perquisites listed below.
- Basic Python,
- Interaction with Terminal,
- Usage of Libraries.

## A CLI URL Shortener
As an example, we will be building a very simple cli to implement the [shortpaw](https://shortpaw.herokuapp.com/about) api into the terminal and using requests to send a post request and rich to create a beautiful CLI. All using python. The final result would look something like this.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658823834729/mfmYlBf1n.png align="left")
I have also uploaded the cli to [pypi](https://pypi.org/project/shortpaw) so if you have python installed, you can easily install the cli with a one line command.
```shell
pip install shortpaw
```

## Setup

I recommend the following software.
- Text Editor: [Sublime Text](https://sublimetext.com), [VSCode](https://code.visualstudio.com).
- Terminal: [Windows Terminal](https://github.com/microsoft/terminal), [Kitty](https://sw.kovidgoyal.net/kitty/).
- Python: Version 3.6 or greater.

### Libraries we will be working with
- [Rich](https://rich.readthedocs.io/en/stable/introduction.html): Rich is a python library used to create beautiful cli's in python and is very useful. A must have. Install it with,
```shell
pip install rich
```
- [Requests](https://pypi.org/project/requests/): This is a must have. Requests is the most easy way to make web requests in python. Install it with,
```shell
pip install requests
```
- Argparse: We will be using argparse to parse the arguments passed by the user.

## Coding the CLI

- Open up the terminal and make a new directory and make a new python script __main__.py and also create  a __init__.py
```
mkdir shortpaw
touch __main__.py
touch __init__.py
```
- Open up the __main__.py in you favourite code editor. I will be using sublime text.
- Import all the modules and libraries we need. Just copy and paste if you like.
```python
from rich.console import Console
from rich.panel import Panel
from rich.progress import Progress
from rich.columns import Columns
from rich.markdown import Markdown
from rich.table import Table
from rich import print
from rich.text import Text
from rich.json import JSON
from rich.prompt import Prompt, Confirm
from rich.padding import Padding
import argparse
import requests
import time
import json
```
- Setting Up Argparse: 
In this, we use -c for custom url and -u for url. These two are optional arguments and -i is a store value. That means it doesn't need an argument content. It is just a flag.
```python
console = Console()
parser = argparse.ArgumentParser(prog='ShortPaw CLI')
parser.add_argument('-v','--version', action='version', version='%(prog)s 0.1.1')
parser.add_argument("-c", help="Custom URL")
parser.add_argument("-u", help="URL to Shorten")
parser.add_argument("-i", help="Interactive Mode", action="store_true")
args = parser.parse_args()
```
- Setting Up the Web Request Function: 
If you head on over to the [shortpaw api](https://shortpaw.herokuapp.com/about), you will see that there are two end points one for a normal url and the other for a custom url.
The /url accepts a argument url and the /custom_url needs url and custom_url.
We will be using the log module from rich to log the output from the function and rich also provides emoji support that can be accessed with :emoji:
The function would accept a data_dict where we will send the url and if the value of "custom" to true, it will accept the value for a custom_url as well. Sounds Simple Enough Right!
```python
def shorten(data_dict):
	if data_dict["custom"]:
		console.log(":green_circle: Detected to Use CUSTOM URLS")
		data = {"url": data_dict["url"], "custom_url": data_dict["custom_url"]}
		url_info_json = requests.post(f'https://shortpaw.herokuapp.com/custom_api', params=data).content
		console.log(":cookie:Successfully Retrived DATA from DATABASE")
		return url_info_json
	else:
		data = {"url": data_dict["url"]}
		console.log(":green_circle: Detected to NOT Use CUSTOM URLS")
		url_info_json = requests.post(f'https://shortpaw.herokuapp.com/api', params=data).content
		console.log(":cookie:Successfully Retrived DATA from DATABASE")
		return url_info_json
```
- Setting up interactive Mode: 
If the user doesn't know about argument and just opens the cli, the user should be redirected to a interactive mode with prompts. We will be creating a interactive function and use rich's prompts module for user prompts. The function just returns the dictionary we called data_dict.
```python
def interactive():
	url = Prompt.ask("Enter The URL You want to Shorten")
	custom_ask = Confirm.ask("Do You Want to Use a Custom URL?")
	if custom_ask:
		custom_url = Prompt.ask("Enter Your Custom URL and ShortPaw will use it if there are no copies")
		return {"url": url, "custom_url": custom_url, "custom": True}
	else:
		return {"url": url, "custom": False}
```
- Adding the Startup: Read the Comments
```python
  # Add a ruler
  console.rule("[bold violet]:dog: ShortPaw: Woof Woof")
  
  # If i flag is passed
  if args.i:
  	data_dict = interactive()
  else:
  	if args.u is None:
        # If URL is not provided open interactive Mode
  		console.print("[!] No Specification of URL Found...Opening User Prompt", style="bold red")
  		data_dict = interactive()
  	else:
  		url = args.u
        # If Custom URL is not provided
  		if args.c is None:
  			data_dict = {"url": url, "custom": False}
  		else:
  			data_dict = {"url": url, "custom_url": args.c, "custom": True}
  
  # Use Rich to make a spinner while the web request is taking place
  with console.status("Working On That", spinner="clock"):
  	url_info = shorten(data_dict)
  
  # Print json with rich json 
  console.rule("[bold red]JSON Results")
  console.print(JSON(url_info))
  console.rule("[bold green]Readable Results")
  
  # Print Clickable Link With Rich Console
  url_info_json = json.loads(url_info)
  console.print(f'Visit your shortened url here [link=https://shortpaw.herokuapp.com/{url_info_json["hash"]}]/{url_info_json["hash"]}[/link]')
  
  # Add Credits
  panel_1 = Panel(Text("By NoobScience", justify="center", style="bold green"))
  print(panel_1)
```

## Full Working Code
https://shortpaw.herokuapp.com/source

```python
from rich.console import Console
from rich.panel import Panel
from rich.progress import Progress
from rich.columns import Columns
from rich.markdown import Markdown
from rich.table import Table
from rich import print
from rich.text import Text
from rich.json import JSON
from rich.prompt import Prompt, Confirm
from rich.padding import Padding
import argparse
import requests
import time
import json

console = Console()
parser = argparse.ArgumentParser(prog='ShortPaw CLI')
parser.add_argument('-v','--version', action='version', version='%(prog)s 0.1.1')
parser.add_argument("-c", help="Custom URL")
parser.add_argument("-u", help="URL to Shorten")
parser.add_argument("-i", help="Interactive Mode", action="store_true")
args = parser.parse_args()

def interactive():
	url = Prompt.ask("Enter The URL You want to Shorten")
	custom_ask = Confirm.ask("Do You Want to Use a Custom URL?")
	if custom_ask:
		custom_url = Prompt.ask("Enter Your Custom URL and ShortPaw will use it if there are no copies")
		return {"url": url, "custom_url": custom_url, "custom": True}
	else:
		return {"url": url, "custom": False}

def shorten(data_dict):
	if data_dict["custom"]:
		console.log(":green_circle: Detected to Use CUSTOM URLS")
		data = {"url": data_dict["url"], "custom_url": data_dict["custom_url"]}
		url_info_json = requests.post(f'https://shortpaw.herokuapp.com/custom_api', params=data).content
		console.log(":cookie:Successfully Retrived DATA from DATABASE")
		return url_info_json
	else:
		data = {"url": data_dict["url"]}
		console.log(":green_circle: Detected to NOT Use CUSTOM URLS")
		url_info_json = requests.post(f'https://shortpaw.herokuapp.com/api', params=data).content
		console.log(":cookie:Successfully Retrived DATA from DATABASE")
		return url_info_json

console.rule("[bold violet]:dog: ShortPaw: Woof Woof")

if args.i:
	data_dict = interactive()
else:
	if args.u is None:
		console.print("[!] No Specification of URL Found...Opening User Prompt", style="bold red")
		data_dict = interactive()
	else:
		url = args.u
		if args.c is None:
			data_dict = {"url": url, "custom": False}
		else:
			data_dict = {"url": url, "custom_url": args.c, "custom": True}

with console.status("Working On That", spinner="clock"):
	url_info = shorten(data_dict)
console.rule("[bold red]JSON Results")
console.print(JSON(url_info))
console.rule("[bold green]Readable Results")
url_info_json = json.loads(url_info)
console.print(f'Visit your shortened url here [link=https://shortpaw.herokuapp.com/{url_info_json["hash"]}]/{url_info_json["hash"]}[/link]')
panel_1 = Panel(Text("By NoobScience", justify="center", style="bold green"))
print(panel_1)
```
- Save the file and run it:
```shell
python __main__.py -u "https://youtube.com"
```

## Conclusion
So As you saw, it is quite easy to create a beautiful cli easily with python. This is just one example and the possibilities are endless. Hope you enjoyed it. If you have any queries or issues, please feel free to reach out. I am always available on twitter and mail. Feel free to check out my projects on GitHub and check this article out on my own blogging platform I made [here](http://thenooblog.herokuapp.com/articles/fNmlUsOg).

## Stats:
- Time Spent Writing: 52minutes
- Music Playing: [Lofi Girl](https://www.youtube.com/watch?v=jfKfPfyJRdk)
- Platform Used: [Hashnode](https://hashnode.com), [TheNooblog](https://thenooblog.herokuapp.com/)
- Level: Beginner to Moderate





