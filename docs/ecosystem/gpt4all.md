# GPT4All

This page covers how to use the `GPT4All` wrapper within LangChain. The tutorial is divided into two parts: installation and setup, followed by usage with an example.

## Installation and Setup
- Install the Python package with `pip install pyllamacpp`
- Download a [GPT4All model](https://github.com/nomic-ai/pyllamacpp#supported-model) and place it in your desired directory

## Usage

### GPT4All

To use the GPT4All wrapper, you need to provide the path to the pre-trained model file and the model's configuration.

```python
from langchain.llms import GPT4All

# Instantiate the model. Callbacks support token-wise streaming
model = GPT4All(model="./models/gpt4all-model.bin", n_ctx=512, n_threads=8)

# Generate text
response = model("Once upon a time, ")
```

You can also customize the generation parameters, such as n_predict, temp, top_p, top_k, and others.

To stream the model's predictions, add in a CallbackManager.

```python
from langchain.llms import GPT4All
from langchain.callbacks.base import CallbackManager
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler
# There are many CallbackHandlers supported, such as
# from langchain.callbacks.streamlit import StreamlitCallbackHandler

callback_manager = CallbackManager([StreamingStdOutCallbackHandler()])
model = GPT4All(model="./models/gpt4all-model.bin", n_ctx=512, n_threads=8, callback_handler=callback_handler, verbose=True)

# Generate text. Tokens are streamed throught the callback manager.
model("Once upon a time, ")
```

## Model File

You can find links to model file downloads in the [pyllamacpp](https://github.com/nomic-ai/pyllamacpp) repository.

For a more detailed walkthrough of this, see [this notebook](../modules/models/llms/integrations/gpt4all.ipynb)