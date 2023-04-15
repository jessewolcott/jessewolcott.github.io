---
layout: post
title: Everyone else is doing it!!
author: jesse.wolcott
date: 2023-04-15 11:00:00 -04:00

---

One of my weightlifting coaches is a super interesting guy (all of my coaches are, but this project wasn't their idea). While we were lifting the other night, he brought up the idea of making a bot using ChatGPT, and how that probably speaks louder on a GitHub project page than another powershell script. He's right! I don't know what I'd use one for, but the idea of cloud appliance that does something relevant to my life is neat. I also don't have a ton of experience with AWS, since I spend my days (and the occasional night) mired in Azure.

I will list a collection of sites at the end of this article that I used to assist me in building this thing. 

### Presumptions
- This build is largely OS independent, but I am using Windows 11 and VSCode
- Python will be used, 3.11.3 at time of writing
- I will be avoiding Azure in favor of AWS at all costs!

1. Create a new repo on GitHub or wherever you store your code projects. Clone it onto your computer, and open VSCode in that folder.
2. Install Python however you'd like. Windows Store works well, and ```winget install python``` works too. You can also head over to https://www.python.org and find your download if you'd like to do a system install.
3. Open your terminal (as admin if windows) and run ```python --version``` and verify that your version matches what you just installed.
4. Install the python package manager (PIP) by running the following: ```python -m pip install -U pip```
5. Install the openai package by running the following: ```pip install openai```
6. Install the gradio package by running the following: ```pip install gradio```. Gradio is a front-end for demos, check it out here: https://gradio.app/
7. Head over to https://platform.openai.com/signup and sign up for a free account. 
8. Navigate to the API keys page, here: https://platform.openai.com/account/api-keys, and create a new secret key. Create a text file in your folder called "keys.py" and put your secret in there like so (take note of the single quotes): ```apptoken = 'yourkeygoesinhere'```.
9. Create a file in your folder called ".gitignore". Inside of that file, put your keyfile in there(just put keys.py on the first line and hit save), so that it won't be uploaded to GitHub for the world to see. 
10. Create a file in VSCode and call it "app.py". Put the following code in that file (this is lifted directly from beebom.com, fully recognized, we are adding more content later- All i did was move the keys). 

```python
import openai
import gradio
import keys

openai.api_key = keys.apptoken

messages = [
    {"role": "system", "content": "You are a helpful and kind AI Assistant."},
]

def chatbot(input):
    if input:
        messages.append({"role": "user", "content": input})
        chat = openai.ChatCompletion.create(
            model="gpt-3.5-turbo", messages=messages
        )
        reply = chat.choices[0].message.content
        messages.append({"role": "assistant", "content": reply})
        return reply

inputs = gradio.inputs.Textbox(lines=7, label="Chat with AI")
outputs = gradio.outputs.Textbox(label="Reply")

gradio.Interface(fn=chatbot, inputs=inputs, outputs=outputs, title="AI Bot",
             description="Ask anything you want",
             theme="compact").launch(share=True)
```

11. Back in your terminal, run your fancy new python script by running ```python "Path\to\app.py```
12. When that runs, you'll see some URLs. You can play with your bot by going to one of those sites, like this one: http://127.0.0.1:7860. Its done! Woo! Lets dig in!
![Chatbot Lives!](/assets/img/2023/04/aichatbot1.png)
13. Commit and push your GitHub repo (and make sure that it sees your .gitignore, you don't want the internet using your key!)

In your ```app.py```, you can change a couple of things, but the neat and easy one is the first prompt. In the example, you can see that we set the tone of the convo with "You are a helpful and kind AI Assistant.". Play around with that sentence and see if you can get it to do other things. Additionally, pay attention to the terminal. If you hit your limit on AI calls, it will tell you. 

I had fun building this, and it didn't take too long. I need to find something cool to do with it!

https://github.com/jessewolcott/ChatBot

### Resources
- https://beebom.com/how-build-own-ai-chatbot-with-chatgpt-api/
- https://github.com/amrrs/chatgpt-api-python/blob/main/ChatGPT_API_in_Python.ipynb


