# Running the Application

### Understanding the application

Before you run [claive\_getting\_started.py](https://github.com/SecretFoundation/claive-getting-started/blob/main/claive_getting_started.py), let's examine the code.&#x20;

1\. **Importing the Required Modules**

```python
from claive_sdk.claive import ChatClaive
from claive_sdk.secret import SecretClaive
```

* **`ChatClaive`**: Handles communication with the LLM, such as sending messages and receiving responses.
* **`SecretClaive`**: Manages secure access to LLM models and provides metadata about available models.

2\. **Initializing the Secret Client**

```python
secret_client = SecretClaive()
```

* Creates an instance of `SecretClaive`, which is used to interact with the Secret backend to fetch available LLM models and their connection details.

3\. **Fetching Models and URLs**

```python
models = secret_client.get_models()
urls = secret_client.get_urls(model=models[0])
```

* **`get_models()`**: Retrieves a list of all LLM models registered with the backend.
* **`get_urls(model=models[0])`**: For the first model in the list (`models[0]`), fetches a list of instance URLs where the model can be accessed.

This code demonstrates how to interact with a confidential LLM (Large Language Model) using the `claive_sdk` Python library. Here's a breakdown of what each section does:

***

#### 1. **Importing the Required Modules**

```python
pythonCopyEditfrom claive_sdk.claive import ChatClaive
from claive_sdk.secret import SecretClaive
```

* **`ChatClaive`**: Handles communication with the LLM, such as sending messages and receiving responses.
* **`SecretClaive`**: Manages secure access to LLM models and provides metadata about available models.

***

#### 2. **Initializing the Secret Client**

```python
pythonCopyEditsecret_client = SecretClaive()
```

* Creates an instance of `SecretClaive`, which is used to interact with the secret backend to fetch available LLM models and their connection details.

***

#### 3. **Fetching Models and URLs**

```python
pythonCopyEditmodels = secret_client.get_models()
urls = secret_client.get_urls(model=models[0])
```

* **`get_models()`**: Retrieves a list of all LLM models registered with the backend.
* **`get_urls(model=models[0])`**: For the first model in the list (`models[0]`), fetches a list of instance URLs where the model can be accessed.

***

#### 4. **Setting Up the LLM Client**

```python
claive_llm = ChatClaive(
    base_url=urls[0], 
    model='llama3.1:70b', 
    temperature=1.0
)
```

* **`base_url=urls[0]`**: Specifies the first URL in the list as the endpoint to connect to the LLM.
* **`model='llama3.1:70b'`**: Specifies the model to use (e.g., Llama 3.1 with 70 billion parameters).
* **`temperature=1.0`**: Configures the "creativity" of the model's responses. Higher values produce more varied outputs, while lower values make responses more deterministic.

#### 5. **Defining the Chat Messages**

```python
messages = [
    ("system", "You are my therapist. Help me with my issues."),
    ("human", "I miss my cat."),
]
```

* Messages are defined as a list of tuples:
  * **`("system", ...)`**: Instructions for the model about its role (e.g., "therapist").
  * **`("human", ...)`**: A message from the user (e.g., expressing sadness about missing their cat).

#### 6. **Invoking the Model**

```python
response = claive_llm.invoke(messages, stream=False)
```

* **`invoke(messages, stream=False)`**: Sends the messages to the LLM for processing.
* **`messages`**: The list of chat messages.
* **`stream=False`**: Indicates that the response should be returned all at once rather than streamed in parts.

### Run the application

To run the sample application:

```bash
python claive_getting_started.py
```

Upon successful installation, you should see a response:&#x20;

{% code overflow="wrap" %}
```
It's completely normal to feel a deep sense of loss and longing when we're separated from our beloved pets, especially ones as special as cats.

Was it a recent separation, or is this a lingering feeling you've been carrying around for a while?
```
{% endcode %}

### Conclusion

Congrats on your first integration with Claive SDK! :tada:

The Claive SDK provides developers with an early glimpse into integrating confidential LLMs, enabling secure and innovative applications. As a developer preview, it is designed for testing and exploration, not production use. Feedback is encouraged to help refine the SDK for future releases.&#x20;

Join the [Secret Network Community Developers](../../overview-ecosystem-and-technology/secret-network-overview/) group on Telegram to share feedback and get code assistance :smile:
