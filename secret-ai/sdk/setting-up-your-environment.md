---
description: >-
  This page introduces Secret AI SDK, provides guidance and examples how to use
  Secret AI SDK.
---

# Setting Up Your Environment

{% hint style="danger" %}
Secret AI SDK is a developer preview and is not intended for production use.&#x20;
{% endhint %}

Secret AI SDK is an advanced security layer designed to integrate seamlessly with Langchaine's ChatOllama, ensuring a secure and efficient API interaction. To begin utilizing Secret AI SDK with Langchaine's ChatOllama, follow these installation and configuration steps:

### Install Requirements

To follow along with the guide, we will be using `Anaconda` and `Python 3.12`.&#x20;

1. [Install Anaconda](https://www.anaconda.com/download/success) for Windows, Mac, or Linux.
2. Clone the Secret AI getting started repository here:

```bash
git clone https://github.com/SecretFoundation/claive-getting-started
```

### Create Anaconda virtual environment

In your text editor, create an Anaconda virtual environment with `Python 3.12`:

```bash
conda create -n menv python=3.12
```

Activate the virtual environment:&#x20;

```bash
conda activate menv
```

### Install Secret AI dependencies

{% code overflow="wrap" %}
```bash
pip install -r requirements.txt && pip install git+https://github.com/scrtlabs/secret-sdk-python.git@main && pip install git+https://github.com/scrtlabs/claive-sdk.git
```
{% endcode %}

### Set developer key

```bash
export SECRET_AI_API_KEY=bWFzdGVyQHNjcnRsYWJzLmNvbTpTZWNyZXROZXR3b3JrTWFzdGVyS2V5X18yMDI1
```

{% hint style="danger" %}
Master key is available for developer preview; later on developers will be able to request individual API keys through the developer portal.
{% endhint %}
