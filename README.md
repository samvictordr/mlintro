### Section 1: **Setting Up the Basic Chat Interface**

```python
# Section 1: Basic Chat Interface

def chatbot_greet():
    print("Chatbot: Hello! How can I assist you today?")

def get_user_input():
    return input("You: ")

def respond_to_user(input_text):
    print(f"Chatbot: I'm still learning. You said: {input_text}")

# Main loop
if __name__ == "__main__":
    chatbot_greet()
    while True:
        user_input = get_user_input()
        if user_input.lower() == "bye":
            print("Chatbot: Goodbye!")
            break
        respond_to_user(user_input)
```

### Section 2: **Adding Simple Predefined Responses**

Now, let’s add some predefined responses to common questions using basic conditionals.

```python
# Section 2: Predefined Responses

def respond_to_user(input_text):
    input_text = input_text.lower()
    
    if "hello" in input_text:
        print("Chatbot: Hi there!")
    elif "how are you" in input_text:
        print("Chatbot: I'm just a program, but I'm doing great! How about you?")
    elif "weather" in input_text:
        print("Chatbot: I can't check the weather, but I hope it's sunny!")
    elif "joke" in input_text:
        print("Chatbot: Why don't scientists trust atoms? Because they make up everything!")
    else:
        print(f"Chatbot: Sorry, I don't know how to respond to '{input_text}'.")

# Main loop (same as before)
if __name__ == "__main__":
    chatbot_greet()
    while True:
        user_input = get_user_input()
        if user_input.lower() == "bye":
            print("Chatbot: Goodbye!")
            break
        respond_to_user(user_input)
```

### Section 3: **Improving Responses Using NLP with spaCy**

We’ll improve the chatbot by using spaCy to tokenize and understand user input better. Install `spaCy` and download a model with:
```bash
pip install spacy
python -m spacy download en_core_web_sm
```

Here’s how you can integrate spaCy for better language understanding:

```python
import spacy

# Section 3: Using spaCy for NLP
nlp = spacy.load("en_core_web_sm")

def respond_to_user(input_text):
    doc = nlp(input_text.lower())
    
    if any(token.lemma_ == "hello" for token in doc):
        print("Chatbot: Hi there!")
    elif any(token.lemma_ == "how" for token in doc) and any(token.lemma_ == "be" for token in doc):
        print("Chatbot: I'm just a program, but I'm doing great! How about you?")
    elif any(token.lemma_ == "weather" for token in doc):
        print("Chatbot: I can't check the weather, but I hope it's sunny!")
    elif any(token.lemma_ == "joke" for token in doc):
        print("Chatbot: Why don't scientists trust atoms? Because they make up everything!")
    else:
        print(f"Chatbot: Sorry, I don't know how to respond to '{input_text}'.")

# Main loop (same as before)
if __name__ == "__main__":
    chatbot_greet()
    while True:
        user_input = get_user_input()
        if user_input.lower() == "bye":
            print("Chatbot: Goodbye!")
            break
        respond_to_user(user_input)
```

### Section 4: **Adding More Dynamic Responses Using GPT (Hugging Face)**

To make the chatbot more dynamic, we can integrate a pre-trained transformer model (like GPT-2) using the `transformers` library by Hugging Face.

First, install the necessary library:
```bash
pip install transformers
```

Then modify the chatbot to use GPT-2 for generating responses:

```python
from transformers import pipeline

# Section 4: Using GPT-2 for Generating Responses
gpt_model = pipeline('text-generation', model='gpt2')

def respond_to_user(input_text):
    if "bye" in input_text.lower():
        print("Chatbot: Goodbye!")
    else:
        response = gpt_model(input_text, max_length=50, num_return_sequences=1)
        print(f"Chatbot: {response[0]['generated_text']}")

# Main loop (same as before)
if __name__ == "__main__":
    chatbot_greet()
    while True:
        user_input = get_user_input()
        if user_input.lower() == "bye":
            print("Chatbot: Goodbye!")
            break
        respond_to_user(user_input)
```
