# Streamlit Tutorial
A tutorial repo for creating Streamlit UI for projects

## Dependencies

For this tutorial, you will need:

- a HuggingFace account
- a HuggingFace API Token with WRITE access
- an OpenAI API key (to use the app you create)

## Instructions

### HuggingFace: Create your Space

1. Go to https://huggingface.co/spaces and select "Create new Space"
![image](https://github.com/user-attachments/assets/f4bfa634-42df-491b-b583-83425786947e)

2. Name your space, and select "Streamlit" as the Space SDK
![image](https://github.com/user-attachments/assets/95a0ad6f-7801-4d2b-a5c4-52082b6733ee)

In this tutorial, I'll name the space "my-chat-app"

Your space has been created! Now we can use Git to edit our app and upload it to our space. 

### Local Computer: Create app.py

1. Clone your Space's repo onto your local computer using the below command in a terminal. Be sure to replace USERNAME and SPACENAME with your username and the name of your space.

`git clone https://huggingface.co/spaces/USERNAME/SPACENAME`

2. Create a new .py file and name it `app.py`. This will be the file that controls our user interface.

3. Add in Streamlit code - see the example below for a ChatGPT-like interface (from [Streamlit's docs](https://docs.streamlit.io/develop/tutorials/llms/llm-quickstart))

 ```
import streamlit as st
from langchain_openai.chat_models import ChatOpenAI

st.title("🦜🔗 Quickstart App")

openai_api_key = st.sidebar.text_input("OpenAI API Key", type="password")


def generate_response(input_text):
    model = ChatOpenAI(temperature=0.7, api_key=openai_api_key)
    st.info(model.invoke(input_text))


with st.form("my_form"):
    text = st.text_area(
        "Enter text:",
        "What are the three key pieces of advice for learning how to code?",
    )
    submitted = st.form_submit_button("Submit")
    if not openai_api_key.startswith("sk-"):
        st.warning("Please enter your OpenAI API key!", icon="⚠")
    if submitted and openai_api_key.startswith("sk-"):
        generate_response(text)
```

4. Create a new text file and name it `requirements.txt`. This will be where we keep our dependencies (anything we import in our .py file, besides streamlit itself and basic Python modules)

Inside `requirements.txt`, add the line:
`langchain_openai`

5. Now we're ready to upload our model to the hub! Use git to add, commit, and push your changes.

`git add app.py requirements.txt`

`git commit -m "create our app and requirements file"`

`git pull`

`git push`

## More Information

See this tutorial for managing secrets (API keys, passwords, etc) on HuggingFace Spaces: https://huggingface.co/docs/hub/en/spaces-overview#managing-secrets-and-environment-variables




6. Demo your new app on your HuggingFace Space: https://huggingface.co/spaces/USERNAME/SPACENAME
