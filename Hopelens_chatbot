import json
import openai

# Replace with your actual API key
openai.api_key = "API"

# Load the dataset
with open("data.json", "r") as file:
    data = json.load(file)
intents = data["intents"]

# Build system prompt from dataset
system_prompt = "You are a helpful assistant trained on the following intents:\n\n"
for intent in intents:
    system_prompt += f"Intent: {intent['tag']}\nPatterns: {', '.join(intent['patterns'])}\nResponses: {', '.join(intent['responses'])}\n\n"

# Function to get GPT-3.5 Turbo response
def get_completion(user_input):
    response = openai.chat.completions.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": system_prompt},
            {"role": "user", "content": user_input}
        ]
    )
    return response.choices[0].message.content.strip()


def chatbot():
    print("\nChatbot ready! Type 'quit' to exit.")
    while True:
        user_input = input("You: ")
        if user_input.lower() == "quit":
            break
        reply = get_completion(user_input)
        print("Bot:", reply)


if __name__ == "__main__":
    chatbot()
