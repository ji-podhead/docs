# Agent505

Agent505 is a platform for building and managing AI agents that can interact with users through websockets. It uses FastAPI, Pydantic, Uvicorn, and other libraries to provide a flexible and scalable environment for developing and deploying AI-powered applications.

With Agent505, you can:

- Create and manage AI agents with custom personalities and capabilities.
- Define workflows and interactions between agents and users.
- Connect agents to various data sources and tools.
- Build AI-powered applications that can automate tasks, provide information, and assist users in various domains.




## Overview
```
Agent505/
├── .env.sample
├── main.py
├── pyproject.toml
├── requirements.txt
├── setup.py
├── src/
│   ├── __init__.py
│   ├── server.py
│   └── session.py
└── stylegenie.egg-info/
    ├── dependency_links.txt
    ├── PKG-INFO
    ├── requires.txt
    ├── SOURCES.txt
    └── top_level.txt
```
The project is structured as follows:

- `Agent505/main.py`: This file contains the main application logic, including the Agent505 class, which manages sessions and agents.
- `Agent505/src/session.py`: This file defines the Session class, which manages the context and state of a conversation between a user and a model. It also defines the Agent class, which represents an autonomous entity that interacts with a session and a model to process messages and provide responses.
- `Agent505/src/server.py`: This file defines the FastAPI server and the ConnectionManager class, which manages the websocket connections.
- `Agent505/pyproject.toml`: This file contains the project's metadata, including its dependencies.

## Feedback Loop
```mermaid
   graph LR
   subgraph Me["<h1>Incoming Message</h1><align left>- the update() method of the ContextRegistry gets triggered for on of those reasons: <br/>- The user sends a Message<br/>- A toolcall has finished</align>"]
    end
   subgraph A["<h2>Agent waits for Event or continues Feedback Loop</h2>"]
    end
   subgraph AC["<h3>Agent is not working and is neither awaiting response from tools, crews, or user</h3>"]
    end
 subgraph Wa["<h3>Agent is waiting for the ContextRegistry to get updated</h3>- agent is busy, or waiting for userinput/crews/tools "]
    end
 subgraph Ru["<h3>Agent proceeds running the feedback loop</h3>- agent requirements to continue are met<br/>- run() method gets called<br/>- agent uses the contextRegistry for completion conext(messages) <br/>- agent can call tools<br/> - agent can send message to user"]
    end




 subgraph To["<h2>Tool Call</h2>- agent decided to call a tool<br> - tool will update the contextRegistry which also triggers the agent update method again"]
    end


 subgraph U["<h1>User</h1>"]
    end

Me --> | agent gets updated | A
A --> | agent proceeds | AC
A--> |Agent waits | Wa
To--> |Tool updates ContextRegistry | Me
Ru--> |Agent responds to user | U
U --> | User sends a message | Me
Wa --> Ru
AC --> Ru
Ru-->To
```

```mermaid
  graph LR
    subgraph U[" <h1>User</h1> <br/>- The User entity represents the person interacting with the system. <br/> - They create a session and send messages to the session."]
    end

    subgraph  S["<h1>Session</h1><br/>- The Session entity represents a conversation or interaction between a user and a model.<br/>- It manages the context and state of the conversation, including agents, crews, models, and messages."]
    end

    subgraph Ma["<h1>MessageManager</h1><br/>- The MessageManager entity manages the flow of messages between agents and the session.<br/>- It registers agents and updates the session context."]
    end

    subgraph A["<h1>Agent</h1><br/>-  The Agent entity represents an autonomous entity that interacts with a session and a model.<br/>- It manages its own state and uses the model to generate responses to input messages."]
    end

    subgraph M["<h1>ModelContextProtocol</h1><br/>- The ModelContextProtocol entity provides a protocol for interacting with models in a session.<br/>- It manages the registration of models, providers, and hosts, and completion/chat functtions."]
    end

    subgraph W["<h1>Workflow</h1><br/>- The Workflow entity registers agents, starts the feedback loop, can call agent based on custom logic, provides tools, crews and data"]
    end
    subgraph C["<h1>ContextRegistry</h1><br/>-  All the information for the session, agents, and crews are stored here. </br>- it also provides functions to update Agent States. <br/> - can inform agent that required response was delivered to agent message stack. <br/> - Agent can continue the feeback loop based on those informations"]
    end

    U--> | creates a Session |S
    U--> | sends msg via websocket |Ma
    S--> | Initializes Model Context Protocol class | M
    S-->| Initializes context registry | C
    S-->| Initializes Message Manager | Ma
    A-->|  request completion | M
    W --> | Request model | M   
    A-->| updates context registry with response |M
    Ma--> |  Updates context |C
   W --> | interacts with agent | A
    C-->| updates the agent status and triggers agent feedback loop, or triggers async wait for further actions loop | A

```




## Dependencies

The project uses the following dependencies:

- python-dotenv
- fastapi
- pydantic
- uvicorn
- python-multipart
- openai
- litellm
- fastapi-sessions
- crewai
- mysql-connector-python

## Usage

To run the project, you need to install the dependencies and then run the main.py file.

```bash
pip install -r Agent505/requirements.txt
python Agent505/main.py
