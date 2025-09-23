# VoiceAssistant  [Demo Link](https://youtu.be/i7SzEbenx5w)

An AI-powered **real-time voice assistant** for automotive service centers, built with **React, Flask, LiveKit, and OpenAI GPT**. The system enables **natural language conversations**, integrates with backend services for **vehicle profile management**, and delivers **real-time audio streaming** for seamless customer support.  

---

## 🚀 Features  
### Intelligent Agent Capabilities
- **Database Interaction and Tool Use:** The assistant has agent capabilities allowing it to interact with a database and call custom Python functions (tools).
- **Dynamic Profile Management:** The system can handle conversational flow required to create a new car profile by collecting the necessary details (VIN, make, model, year) and saving them to the database.  
- **Vehicle Lookup** The agent is equipped to look up car information (profiles) for returning users based on the VIN.  
- **Context Preservation:** The agent maintains conversational context by internally storing the details of the vehicle the user is currently discussing, ensuring the LLM can use this information throughout the session.
### Conversational Flow and Logic
- **Goal-Oriented Routing and Transfer Logic:** Implements a tree-like flow that uses event handlers (specifically triggered when the user finishes speaking) to dynamically change the agent’s behavior based on the current state (e.g., whether car details are collected).
- **Department Transfer:** The agent can logically advance the conversation, such as by offering to forward the user to a "scheduling Department" once the profile creation or lookup is complete.
- **Multimodal Input Processing:** Includes logic to handle the possibility of multimodal messages by processing the content and stripping out image data before sending the remaining text to the LLM
- **Voice Activity Detection (VAD):** Integrates VAD (via livekit-plugins-solero) to accurately determine when the user has finished talking, facilitating natural, real-time conversational turn-taking

 ### Real-Time Performance and Scalability
- **Ultra-Low Latency Communication:** Built on LiveKit to ensure ultra-low latency transportation of voice, video, and audio data.
- **Real-Time LLM Responses:** Utilizes the OpenAI Real-time API to achieve extremely fast response times from the language model.
- **Concurrency and Session Isolation:** The architecture supports multiple agents running at the same time and joining multiple rooms. The backend enforces concurrency by generating a unique room name (using UUID) for each new connection, guaranteeing that users have their own separate conversational sessions.

### Security and Deployment
- **Token-Based Security:** Features a slim Flask backend server (server.py) responsible for dynamically generating and issuing secure, time-limited JSON Web Tokens (JWTs).
- **Granular Access Control:** Tokens provide the ability to specify permissions (e.g., joining, publishing, subscribing) and control which specific room the user can access.
- **Telephony Readiness:** The underlying LiveKit architecture allows for integration with SIP trunking (e.g., Twilio), providing the potential to convert the web agent into a true call center agent that can respond to phone calls.

### Custom Frontend Experience
- **Custom Web Interface:** Implemented using React and Vite to demonstrate integration into a custom environment (simulating a car service call center landing page).
- **Live Transcription:** Displays the live transcription of speech from both the user (local participant) and the AI agent on the screen.
- **Audio Visualization:** Includes a Bar Visualizer component to graphically display the agent’s audio waveform, enhancing the user experience.
- **Voice Controls:** Uses the Voice Assistant Control Bar component for standard audio controls.
---

## 🛠️ Tech Stack 
### Core Real-Time Platform & Protocol
- **LiveKit:** The central, open-source technology facilitating ultra-low latency transportation of voice and audio data. It handles the communication architecture and concurrency.
- **LiveKit Cloud/Self-Hosting:** The platform leverages the LiveKit Cloud environment, though the LiveKit server can also be self-hosted.
- **WebRTC:** The underlying protocol facilitated by LiveKit Cloud for communication between the client and the agent.
### AI Agent and LLM
- **OpenAI Real-time API:** Provides the core AI capabilities and is leveraged for extremely low latency responses.
- **LiveKit Agents:** Framework used to define the AI assistant's behavior.
- **Multimodal Agent:** The agent is built using the MultimodalAgent capability from LiveKit.
- **Function Calling (Tools):** The agent is equipped to utilize custom Python functions/tools (e.g., database lookup and creation) during its invocation.
- **Voice Activity Detection (VAD):** Integrated using the livekit-plugins-solero dependency to manage conversational turn-taking.
- **Alternative LLMs:** The architecture supports integration with other providers, such as Ollama, allowing models to run locally.
### Backend & Data Persistence
- **Python:** The primary language used for building the AI agent logic and the token server.
- **Flask:** Used to build the backend server (server.py).
- **Authorization Server:** A slim Flask server dynamically issues secure, time-limited JSON Web Tokens (JWTs) necessary for connecting to the LiveKit room.
- **Concurrency Dependencies:** Includes flask-async, flask-cores, and Uvicorn for running the Flask server.
- **SQLite 3:** A local database driver used for simple storage and management of vehicle profiles (VIN, make, model, year).
- **Environment Variables:** Handled by the python-dotenv library.
- **Unique Room Generation:** Utilizes UUID to generate unique room identifiers for session isolation.
### Frontend Development
- **React (with Vite):** Used to build the custom web interface.
- **LiveKit Web SDKs:** Includes React components and client libraries, such as ``` @livekit/components-react, @livekit/components-styles, and livekit-client ```, used for connecting and rendering media.
- **UI Components:** Includes pre-built LiveKit components like the Bar Visualizer (for audio waveform display) and the Voice Assistant Control Bar. 

---

## 📂 Project Structure  
```bash
VoiceAssistant/
│── backend/        # Flask API, DB, authentication
│── frontend/       # React 19 app, LiveKit integration
│── .gitignore
```

---
## ⚙️ Setup & Installation
### 1. Clone Repo
```
git clone https://github.com/SSravani14/VoiceAssistant.git
cd VoiceAssistant
```
### 2. Backend Setup
```
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app:app --reload
```

### 3. Frontend Setup
```
cd frontend
npm install
npm run dev
```

### 4. Environment Variables
Create a .env file in both backend/ and frontend/ with keys for:

- OPENAI_API_KEY

- LIVEKIT_API_KEY

- LIVEKIT_API_SECRET

- DATABASE_URL

## 📊 Impact

- Reduces wait times with instant 24/7 AI-driven customer support.

- Improves experience via natural speech interactions instead of complex menus.

- Scales easily with microservices + real-time communication.

## 🔗 Demo Link
- https://youtu.be/i7SzEbenx5w
