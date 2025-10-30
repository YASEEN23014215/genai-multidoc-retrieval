## Design and Implementation of a Multidocument Retrieval Agent Using LlamaIndex
### NAME : YASEEN F
### REGISTER NUMBER :212223220126

### AIM:
To design and implement a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles, and to evaluate its performance by testing it with diverse queries, analyzing its ability to deliver concise, relevant, and accurate responses.

### PROBLEM STATEMENT:
The goal is to develop an intelligent agent capable of managing multiple research papers or documents and retrieving relevant information in response to user queries. Using LlamaIndex, the system will efficiently access various documents, extract key data, and generate coherent, informative answers — enhancing both the speed and accuracy of information retrieval.
### DESIGN STEPS:

#### STEP 1:
Import Dependencies

#### STEP 2:
Configure OpenAI API Key
#### STEP 3:
Enable Async Compatibility
### STEP 4:
Prepare Data Sources
### STEP 5:
Create Document Tools for Each Paper
### STEP 6:
Combine All Tools and Initialize the Language Model
### STEP 7:
Create the Agent Worker then,Instantiate the Agent Runner
### STEP 8:
Query the Agent
### PROGRAM:
```
from helper import get_openai_api_key
OPENAI_API_KEY = get_openai_api_key()
import nest_asyncio
nest_asyncio.apply()
urls = [
    "https://openreview.net/forum?id=dV1TBpMwtl",
    "https://openreview.net/forum?id=hYSykGiFtI",
    "https://openreview.net/forum?id=acOdYRy9lk",
]

papers = [
    "model1.pdf",
    "model2.pdf",
    "model3.pdf",
]
from utils import get_doc_tools
from pathlib import Path

paper_to_tools_dict = {}
for paper in papers:
    print(f"Getting tools for paper: {paper}")
    vector_tool, summary_tool = get_doc_tools(paper, Path(paper).stem)
    paper_to_tools_dict[paper] = [vector_tool, summary_tool]
initial_tools = [t for paper in papers for t in paper_to_tools_dict[paper]]
from llama_index.llms.openai import OpenAI

llm = OpenAI(model="gpt-3.5-turbo")
len(initial_tools)
from llama_index.core.agent import FunctionCallingAgentWorker
from llama_index.core.agent import AgentRunner

agent_worker = FunctionCallingAgentWorker.from_tools(
    initial_tools, 
    llm=llm, 
    verbose=True
)
agent = AgentRunner(agent_worker)
response = agent.query(
    "What are the key findings regarding the use of multimodal pragmatic markers in Japanese, English, and Czech digital communication, particularly concerning the functions of mitigation, emphasis, and epistemic stance-taking?"
    
)
response = agent.query("What is the primary focus of the research, and which three languages are analyzed?")
print(str(response))

```
### OUTPUT:
<img width="1330" height="633" alt="image" src="https://github.com/user-attachments/assets/6afc86df-6331-4bb9-87f5-ee235f5ae786" />
<img width="1341" height="679" alt="image" src="https://github.com/user-attachments/assets/3bfbe088-a146-4b23-b9dc-99f0bcb2dbe3" />
<img width="1353" height="818" alt="image" src="https://github.com/user-attachments/assets/6d248e41-e98a-4f61-ad20-f85e9cb4dc0e" />





### RESULT:
Thus the program to design and implement of a Multidocument Retrieval Agent Using LlamaIndex was executed successfully.

