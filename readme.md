# OpenAI API Usage Guide

The OpenAI API provides access to various product offerings through its API endpoints. You can interact with the API using either curl commands or the OpenAI Python library.

## Products and Capabilities

1. **Text Generation with GPT Models:**
   - OpenAI refers to text generation as completions, where you can complete or generate text using GPT models.
   - Chat completions are optimized GPT models designed for conversational text.

2. **Models Available:**
   - GPT-4
   - GPT-3.5-turbo
   - text-davinci-003, text-davinci-002, davinci, curie, babbage, ada

## Installation

```bash
pip install openai
```

## API Key Setup

```python
import openai
openai.api_key = "your_api_key_here"
```

## List Available Models

```python
openai.models.list()
```

## Chatbot Interaction Example

```python
import os
import openai

# Initialize the chat messages history
messages = [{"role": "assistant", "content": "How can I help?"}]

# Display chat history
def display_chat_history(messages):
    for message in messages:
        print(f"{message['role'].capitalize()}: {message['content']}")

# Get assistant's response
def get_assistant_response(messages, temperature=0.7, top_p=0.5):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": m["role"], "content": m["content"]} for m in messages],
        temperature=temperature,
        max_tokens=150,
        top_p=top_p,
    )
    return response.choices[0].message.content

# Main chat loop
while True:
    display_chat_history(messages)

    # Get user input
    prompt = input("User: ")
    messages.append({"role": "user", "content": prompt})

    # Get assistant response with adjusted temperature and top_p
    response = get_assistant_response(messages, temperature=0.8, top_p=0.8)
    messages.append({"role": "assistant", "content": response})
```

## Tips for Spice up Responses

To add creativity and variety:

- Experiment with the `temperature` parameter (controls randomness).
  - **Temperature:** A higher value (e.g., 0.8) increases randomness and creativity.
  - **Temperature:** A lower value (e.g., 0.1) makes responses more focused and deterministic.

- Adjust the `top_p` parameter to focus on a subset of tokens.

Remember:
- Higher temperature increases variety.
- Lower top_p values reduce diversity.

