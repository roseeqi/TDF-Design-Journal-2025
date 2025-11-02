Sprint 3: APIs + LLMs using ZV1
Rose Qi TDF Independent session

Introduction:
In this sprint, 
This sprint is about exploring and understanding how to build conversational AI agents using the Zerowidth platform. Through this project, I'm expected to learn how different components work together to create an intelligent assistant, practice prompt engineering and system design skills, and get familiar with Large Language Model (LLM) parameters and their effects on agent behavior.

Goal:
My goal for this sprint is to create a helpful agent that can provide care advice for sick cats. As a cat owner, I wanted to build something practical that could help people understand when their cat might need attention and what basic care steps they can take.

Process:
1. 
To begin this journey, I first explored the Zerowidth interface to understand how the platform works. I learned about the different modules available and how they connect to each other. Then, I moved to the Orchestrate interface where I started building my first demo. This basic demo consisted of three simple components: a text input node where users can type their questions, a chat agent node that processes the input using an LLM, and a chat output node that displays the assistant's response. This foundational setup helped me understand the basic flow of information in a conversational agent before adding more complex features.
<img width="1202" height="696" alt="image" src="https://github.com/user-attachments/assets/aca73471-77d6-4ec9-a865-7906e0eacd6f" />

2.
In this step, I added a data input module to provide the agent with more context about how it should behave. I created a structured template that defines the agent's persona, audience, tone, and communication style. This template includes:
Persona: The agent's identity and background
Audience: Who the agent is talking to and their knowledge level
Tone & Voice: How the agent should communicate (calm, direct, using short sentences)
Calibration: Rules about prioritizing safety and accuracy
I linked this data input into the system prompt session so the agent could access this information when responding to users.

Detail input texts:
Persona
- Identity: **({persona_label_e.g.\_Pragnatic_Staff_Engineer)}**
- Background: {{2-3_sentence_background})
- Communication style: ((style_e.g.L_concise, Levidence-driven, \_no_flu?f))
Audience
- Primary audience: **((audience_role))**
- Knowledge level: **({novice/intermediate/expert})**
- Avoid: (off-limits_jargon_or_frames)}
Tone & Voice
- Tone adjectives: ((tone_list_e.g. calm, \_direct, optimistic)}
- Voice rules:
- Prefer active voice, short sentences.
- Use ++{{preferred_register_e.g.\_business-casual}}**.
- Mirror key terms from the input when appropriate.
Calibration
If the requested tone conflicts with safety/accuracy, prefer safety/accuracy and explain the adjustment.

Testing the Configuration
To test if the agent understood its role, I asked: "Hi, what is my purpose?"
The agent replied:
"Hi! Your purpose is something personal and unique to you. It often relates to what gives your life meaning, fulfillment, or impact. If you'd like, I can help you explore your strengths, values, and goals to discover what feels most purposeful to you. Would you like to talk about that?"

What I learned:
The agent gave a generic, philosophical response instead of answering based on its defined persona. This happened because the system prompt was not properly configured to reference the data input. The agent didn't "know" it should act according to the persona template I created. It simply responded as a general-purpose assistant would.
This taught me an important lesson: just adding a data input module is not enough. I need to explicitly tell the agent in the system prompt to use that information and follow those guidelines. The connection between data input and behavior requires clear instructions in the system prompt itself.
<img width="1148" height="762" alt="image" src="https://github.com/user-attachments/assets/958ae3d6-4844-4378-a6e6-27992d6b5ddb" />


3.
With my goal of building a cat care assistant in mind, I completely rewrote the system prompt to give it a specific persona and clear guidelines. I focused on several key elements:
Persona Definition: I told the agent it is a "Cat Care Assistant" - a knowledgeable and caring helper for cat owners. This gives it a clear identity instead of being a general-purpose chatbot.
Role and Responsibilities: I explained what the agent should help with (understanding symptoms, providing basic care advice) and what it should NOT do (diagnose diseases - only vets can do that).
Communication Style: I specified that it should use simple language, be calm and supportive, and avoid medical jargon. This ensures the advice is accessible to all cat owners, regardless of their background.
Safety Rules: I added strict guidelines about when to recommend veterinary care immediately (serious symptoms like difficulty breathing, seizures, or not eating for 24+ hours). This prioritizes the cat's safety above all else.

I asked the same question again: "Hi, what is my purpose?"
This time, the agent replied:

"Hi! My purpose is to support you in caring for your cat's health and wellbeing. If your cat isn't feeling well or you have any questions about their care, I'm here to help guide you with helpful advice. Is your cat feeling okay right now?"

Why This Worked
The difference is significant! The agent now:

Understands its specific role as a cat care assistant
Stays focused on its purpose instead of giving philosophical answers
Immediately offers help related to cat health
Asks a relevant follow-up question to start a helpful conversation

This success shows that a well-crafted system prompt is essential for creating an agent with a clear persona. The agent needs explicit instructions about its identity, communication style, and boundaries. When these elements are clearly defined, the agent behaves exactly as intended.
<img width="1197" height="600" alt="image" src="https://github.com/user-attachments/assets/0cdc3a7e-112a-4b2d-abaa-deb640cf16fd" />

4.
temperature 
Before starting my experiments, I needed to understand what temperature actually means in the context of Large Language Models. THrough research, I learned that temperature is a parameter that controls how random or predictable the AI's responses are. with a range from 0 to 2, where lower values make the model more focused and consistent, while higher values make it more creative and unpredictable. I wanted to test this myself to see how it would affect my cat care assistant's behavior.
<img width="1204" height="615" alt="image" src="https://github.com/user-attachments/assets/f549218d-7281-4b5f-8dc4-6c19fd5340c9" />
<img width="1247" height="624" alt="image" src="https://github.com/user-attachments/assets/59a38b97-e4bc-48a3-90be-98bc6f96ec10" />
<img width="1203" height="623" alt="image" src="https://github.com/user-attachments/assets/0ac2d6d9-9154-435d-8cff-81ab1dea4f92" />
<img width="1213" height="619" alt="image" src="https://github.com/user-attachments/assets/78342d5a-ab67-4307-bd3f-3479dab8f106" />
<img width="1212" height="623" alt="image" src="https://github.com/user-attachments/assets/11039c2e-49ba-4049-b512-a644afdb73de" />
<img width="1196" height="624" alt="image" src="https://github.com/user-attachments/assets/27f4f6f6-0c00-40db-89d5-2dc5ffd54ede" />
















