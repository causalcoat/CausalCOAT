
## Prepare to Use API

### Interact with OpenAI

1. Go through [the OpenAI Quickstart Tutorial](https://platform.openai.com/docs/quickstart?context=python)
2. In this project, we `LLM_openai()` to contorl the interaction with OpenAI
    ```python
    import sys
    sys.path.insert(0, '/project/root/path') # set project root path

    from utils import Logger
    from openai_utils import LLM_openai

    # check the conversation log at 'logs/{exp_name}'
    logger = Logger(
        root = '/project/root/path', 
        exp_name = 'set_exp_name'
    )

    llm = LLM_openai(logger)

    response = llm.chat(
        model="gpt-4-1106-preview",
        content= "Hello GPT4!",
        system_instruct = "You are a helpful assistant."
    )
    ``` 

### Interact with Poe

1. Go through [the Poe FastAPI Tutorial](https://creator.poe.com/docs/accessing-other-bots-on-poe)
2. In this project, we `chat()` to contorl the interaction with Poe
    ```python
    import fastapi_poe as fp
    import asyncio

    async def chat(content, bot_name="GPT-3.5-Turbo" ):
        poe_api_key = "your api key" # set your api key
        message = fp.ProtocolMessage(role="user", content=content)
        responce = ""
        async for partial in fp.get_bot_response(messages=[message], bot_name=bot_name, api_key=poe_api_key): 
            responce = responce + partial.text

        return responce

    response = await chat("Hello world!", bot_name="GPT-3.5-Turbo" )
    ``` 


## The AppleGastronome Benchmark

### Files

- **Apple_Gastronome_AG7_v20240201.ipynb** This is the notebook to generate the AppleGastronome Benchmark dataset. "AG7" means there are 7 variables considered in the data-generating process.
- **Apple_Gastronome_AG7_v20240201.xlsx** This is the generated AppleGastronome Benchmark dataset. It consists of 8 columns: 7 variables plus one column for the review texts.
- **Formal_exp_1 AG7_2024_02_01 6 MoEgraq 0206 release.ipynb** This is the notebook to test COAT method with different Foundation Models. "MoEgraq" means that "Mixtral-8x7b-Groq" is employed as annotation model as it is cheap and very fast for the annotation task.

##  The Neuropathic Benchmark

Source of the causal graph: [here](https://observablehq.com/@turuibo/the-complete-causal-graph-of-neuropathic-pain-diagnosis)

### Files

- **SimulatedData_SampleSize100.csv** and **neuro_addition_1000_0126.csv** Generated from [Neuropathic Pain Diagnosis Simulator](https://github.com/TURuibo/Neuropathic-Pain-Diagnosis-Simulator). Simulation of the real-life diagnosis with three levels of variables, including the symptom-level, radiculopathy-level and the pathophysiology-level.
- **id_name.txt** From [Neuropathic Pain Diagnosis Simulator](https://github.com/TURuibo/Neuropathic-Pain-Diagnosis-Simulator). It stores variable names.
- **Neuropathic_Pain_Diagnosis_v20240119.ipynb** This is the notebook to generate clinical notes from tabular data *SimulatedData_SampleSize100.csv*. *Only symptom-level vairables are used.*
- **neuro_R_shoulder_impingement.xlsx** This is the generated clinical notes.
- **Formal_exp_1_Neuro_RSI symptom_only release.ipynb** This is the notebook to test COAT method with different Foundation Models. 

# CausalCOAT