---
description: >-
  This page introduces Claive SDK, provides guidance and examples how to use
  Claive SDK
---

# 👩‍💻 Claive SDK

Claive SDK is an advanced security layer designed to integrate seamlessly with Langchaine's ChatOllama, ensuring a secure and efficient API interaction. By requiring an API Key for access, it provides an additional layer of authentication and data protection, safeguarding sensitive communications. This security protocol enhances the reliability and safety of ChatOllama's operations, offering developers confidence in managing and deploying their applications within secure boundaries. With Claive SDK, users can ensure that their interactions remain private and protected against unauthorized access.

Claive SDK caters to diverse application needs by supporting two types of clients: Synchronous and Asynchronous. Each client type is designed to check for the environment variable `CLAIVE_AI_API_KEY`, which must be correctly set to facilitate secure communication with the confidential LLM. This configuration ensures that all interactions are authorized and protected, offering a robust framework for developing secure, reliable AI-driven applications.

#### Setting Up Claive SDK

To begin utilizing Claive SDK with Langchaine's ChatOllama, follow these installation and configuration steps:

1.  **Install Claive SDK**: Ensure you have the necessary development environment and install the SDK through your preferred package manager.

    ```bash
    pip insall python-claive-sdk
    ```
2. **API Key Configuration**:
   * Obtain your `CLAIVE_AI_API_KEY` from your platform account.
   * Set the environment variable using the command line or within your application settings:
     *   For Linux/macOS:

         ```bash
         export CLAIVE_AI_API_KEY='your_api_key_here'
         ```
     *   For Windows:

         ```cmd
         set CLAIVE_AI_API_KEY='your_api_key_here'
         ```
3. **Use ChatClaive**:
   * Follow the provided SDK documentation to integrate the client of with ChatClaive, ensuring you handle API interactions securely.

By adhering to these steps, you can ensure a secure and efficient setup, leveraging Claive SDK's robust authentication to protect your application's data integrity.

Sample Code:

```python
from claive_sdk.secret import SecretClaive
from claive_sdk.claive import ChatClaive

# Initialize the secret client
secret_client = SecretClaive()

# Retrieve available models
models = secret_client.get_models()
assert len(models) >= 1, "No models found, ensure API key is set correctly."

# Retrieve model URLs
urls = secret_client.get_urls(model=TEST_KNOWN_MODEL)
assert len(urls) >= 1, "No URLs available for the specified model."

# Initialize the ChatClaive client with retrieved URL and model
claive_llm = ChatClaive(
    base_url=urls[0],
    model=TEST_KNOWN_MODEL,
    temperature=1.0
)

# Define messages for translation
messages = [
    (
        "system",
        "You are a helpful assistant that translates English to French. Translate the user sentence.",
    ),
    ("human", "I love programming."),
]

# Invoke the API to translate the message
response = claive_llm.invoke(messages, stream=False)

print(response.content)

response = claive_llm.invoke(messages, stream=False)
```



