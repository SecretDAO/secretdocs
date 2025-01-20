---
description: >-
  This page introduces Claive SDK and provides guidance and examples of how to
  use Claive SDK.
---

# 👩‍💻 Claive SDK

Claive SDK is an advanced security layer designed to integrate seamlessly with [Langchaine's ChatOllama](https://python.langchain.com/docs/integrations/chat/ollama/), ensuring a secure and efficient API interaction. By requiring an API Key for access, it provides an additional layer of authentication and data protection, safeguarding sensitive communications.&#x20;

This security protocol enhances the reliability and safety of ChatOllama's operations, offering developers confidence in managing and deploying their applications within secure boundaries. With Claive SDK, users can ensure that their interactions remain private and protected against unauthorized access.

Claive SDK caters to diverse application needs by supporting two types of clients: Synchronous and Asynchronous. Each client type is designed to check for the environment variable `CLAIVE_AI_API_KEY`, which must be correctly set to facilitate secure communication with the confidential LLM.&#x20;

{% hint style="info" %}
An API master key is available for developer preview; later on developers will be able to request individual API keys through the developer portal.
{% endhint %}

This configuration ensures that all interactions are authorized and protected, offering a robust framework for developing secure, reliable AI-driven applications.
