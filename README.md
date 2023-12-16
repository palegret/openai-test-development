# OpenAI API developer quickstart

## Step 1: Set up Python

### Install Python
To use the OpenAI Python library, you need at least Python 3.7.1 or newer.
* https://www.python.org/downloads/
* https://wiki.python.org/moin/BeginnersGuide/Download

Type `python` and then press Enter. If you get the interpreter, Python is installed.

### Set up a virtual environment
It is a good practice to create a virtual python environment to install the OpenAI Python library. 
Virtual environments provide a clean working space for your Python packages to be installed.
This means that you do not have conflicts with other libraries you install for other projects. 
To create a virtual environment, Python supplies a built-in venv module.
* https://docs.python.org/3/tutorial/venv.html#creating-virtual-environments

This command creates a virtual environment named `openai-env` in the current directory.

`python -m venv openai-env`

Activate the virtual environment once created (Windows).

`openai-env\Scripts\activate`

The terminal cursor should change after activation, showing an `(openai-env)` prefix.

### Install the OpenAI Python library

Run `pip list` to verify that the OpenAI Python library was successfully installed.

`pip install --upgrade openai`

## Step 2: Setup your API key

### Set up your API key for all projects (recommended)
Main advantage: Python library automatically uses it without having to write any code.

Set environment variable in the current session (Windows).

`setx OPENAI_API_KEY "`*key value*`"`

### Permanent setup (Windows)
1. Open **File Explorer** > Right-click on **This PC** > **Properties**
2. Click on **Advanced system settings** > **Environment Variables**,
**System variables**  section > **New...**: 
    * Variable name: `OPENAI_API_KEY` 
    * Variable value: *key value*
3. Run `echo %OPENAI_API_KEY%` from a new terminal to verify setup.

### Setup your API key for a single project
Create a local `.env` file containing the API key in the project root, then use that API key in code:

`OPENAI_API_KEY=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`

*Add* `.env` *to* `.gitignore` *in the project root to exclude it from source control, along with the* `openai-env` *Python virtual environment created above:*

<pre>
openai-env/
.env
</pre>

To read environment variables from a `.env` file, you must install the `dotenv` package:

`pip install --upgrade dotenv`

Use `dotenv` in your script as follows:

<pre>
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
...
</pre>

The `OpenAI` client defaults to using `os.environ.get("OPENAI_API_KEY")`. If you saved the key under a different name, you can do the following in your `openai-test.py` script:

<pre>
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.environ.get("CUSTOM_ENV_NAME")
)
...
</pre>

## Step 3: Sending your first API request

<pre>
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "system", "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."},
    {"role": "user", "content": "Compose a poem that explains the concept of recursion in programming."}
  ]
)

print(completion.choices[0].message)
</pre>
