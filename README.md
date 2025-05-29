# Koala Care Agent

**Overview**
This project demonstrates a production-ready example of how voice AI can be combined with Salesforce to handle appointment scheduling, account creation, and existing booking lookups—all via phone.

**Built using:**

- Vapi for conversational voice AI

- Salesforce Intelligent Appointment Management for real-time scheduling

- n8n for backend logic and orchestration

**Key Features**
Natural language appointment booking via phone

Real-time lookup of existing patients in Salesforce

New patient onboarding with automatic account creation

Integration with Salesforce Service Territories, Work Types, and Service Appointments

Multi-turn conversation design with fallback handling

Multilingual support via Vapi (Spanish demo shown in video)

🔧 Architecture
<img width="630" alt="Screenshot 2025-05-29 at 11 31 10 am" src="https://github.com/user-attachments/assets/56a978fa-46b3-4b4e-8cd0-c08cc946bdf6" />

🛠️ How It Works
This solution combines best-in-class AI models with Salesforce to create a fully voice-driven scheduling assistant. Here’s how the system works end-to-end:

🎙️ Voice Interaction
Speech-to-Text (STT):
Powered by Deepgram (Nova-3) with multilingual transcription support, providing accurate and fast transcription even in noisy environments.

Language Understanding (LLM):
Vapi leverages OpenAI’s GPT-4o mini to interpret user intent, manage conversation flow, and decide what function/tool to call next.

Text-to-Speech (TTS):
Responses are generated and spoken using Cartesia’s Sonic-2 voice, designed to sound warm, clear, and professional in a healthcare setting.

🧠 Agent Logic via Vapi Tool Calls
Vapi uses structured tool calls to pass structured data (e.g. names, DOB, appointment preferences) from the LLM to downstream systems.

These tool calls hit a webhook in n8n, which acts as the middleware to process requests and route logic.

🔄 Backend Orchestration with n8n
n8n receives the tool call payload and determines what kind of Salesforce action is required:

get_account_details: Searches for an existing patient in Salesforce using name + DOB

create_account: Creates a new person account in Salesforce

get_available_appointments: Queries Salesforce Intelligent Appointment Management for slot availability based on date, territory, and work type

book_appointment: Creates a Service Appointment in Salesforce linked to the patient

get_booked_appointment: Retrieves future appointments for that patient

Once the relevant action is completed, n8n packages the result and responds back to Vapi, which is then passed to the voice agent to share with the user.

🔁 Continuous Conversation
The LLM remains in context through the call, adapting follow-up questions and clarifications.

Users can reschedule, explore different days, or confirm bookings—all through natural voice.





