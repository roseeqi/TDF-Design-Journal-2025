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

I decided to test five different temperature values: 0, 0.5, 1.0, 1.5, and 2.0. To make this a fair comparison, I used the exact same question for all tests: "My cat is sneezing and has watery eyes. What should I do?" This way, I could clearly see how the temperature setting alone changed the responses. I also asked the same question multiple times at each temperature level to check for consistency.

<img width="1204" height="615" alt="image" src="https://github.com/user-attachments/assets/f549218d-7281-4b5f-8dc4-6c19fd5340c9" />
I started with temperature set to 0, which should give me the most predictable and consistent results. I connected a Number node with value 0 to my LLM brain node's temperature parameter and ran my test question.

The first response I got was very structured and straightforward. The agent said: "Your cat may have an upper respiratory issue. Here's what to do: 1. Keep your cat comfortable and warm, 2. Clean watery eyes gently with a damp cloth, 3. Ensure fresh water is available, 4. Remove irritants like smoke or dust, 5. Monitor for worsening symptoms. See a vet if symptoms persist beyond 2-3 days, worsen, or if your cat stops eating."

I asked the exact same question again to test consistency, and the response was almost identical. The wording was nearly word-for-word the same. This confirmed that at temperature 0, the model picks the most probable response every single time, resulting in virtually no variation.
What I noticed was that while the information was accurate and helpful, the tone felt quite robotic and clinical. It was like reading instructions from a medical manual rather than having a conversation with someone who cares. The response was concise and to the point, but it lacked warmth and personality. For a health assistant, this could be both good and bad. Good because it's reliable, bad because it might not provide the emotional support that a worried pet owner needs.

<img width="1198" height="643" alt="image" src="https://github.com/user-attachments/assets/f7af7143-4bbd-4e36-ba02-3a01fc56bc70" />
Next, I changed the temperature to 0.5 and ran the same test. I was curious to see if this small increase would make a noticeable difference.

The response started with "It sounds like your cat might have a mild upper respiratory infection or allergies. Here's how you can help..." followed by similar advice about keeping the cat warm, cleaning eyes, providing water, and removing irritants. However, this time the agent ended with a question: "Is your cat still eating normally?"

I tested it again with the same question, and while the core structure remained similar, the wording changed slightly. The second response said "Your cat likely has a minor upper respiratory issue or irritation" instead of "infection or allergies." The advice steps were also phrased differently, though the content was essentially the same.

What I observed was that temperature 0.5 introduced some variation while maintaining consistency in the core message. The tone was noticeably warmer and more conversational compared to temperature 0. The agent started using phrases like "it sounds like" and "how you can help," which made it feel more human. The addition of follow-up questions showed that the agent was trying to engage in dialogue rather than just delivering information. This felt better

<img width="1203" height="623" alt="image" src="https://github.com/user-attachments/assets/0ac2d6d9-9154-435d-8cff-81ab1dea4f92" />
I increased the temperature to 1.0, which is often the default setting for many LLM applications. I was interested to see how this "balanced" setting would perform.

the agent maintained medical accuracy but expressed it in different ways each time. 

The personality of the assistant started to emerge. Sometimes it was more clinical, sometimes more empathetic, but it always provided sound advice. The responses felt more like talking to a real person who might explain things differently based on their mood or how they're thinking at that moment. This natural variation made the conversation feel authentic rather than scripted.

<img width="1213" height="619" alt="image" src="https://github.com/user-attachments/assets/78342d5a-ab67-4307-bd3f-3479dab8f106" />

I was curious to see what would happen at higher temperature values, so I increased it to 1.5. This is where I expected to see much more creativity.

<img width="1212" height="623" alt="image" src="https://github.com/user-attachments/assets/11039c2e-49ba-4049-b512-a644afdb73de" />
  
What I learned from temperature 1.5 is that it produces highly engaging and personalized responses. 

The assistant felt enthusiastic and creative in its explanations. However, I also noticed that the responses were much longer and sometimes included tangential information. For instance, one response mentioned "Fun fact: cats can actually catch some viral infections from other cats at parks or through windows!" While interesting, this wasn't directly addressing the user's immediate concern. The creativity was exciting, but I wondered if it might be too much for someone who just wants quick, clear advice about their sick cat.

<img width="1196" height="624" alt="image" src="https://github.com/user-attachments/assets/27f4f6f6-0c00-40db-89d5-2dc5ffd54ede" />

Finally, I tested the maximum temperature value of 2.0 to see just how creative and unpredictable the model could get.

The response was dramatically different from everything I'd seen before. I ran the test again, and the second response was completely different in structure, tone, and content organization. It used different emojis, different metaphors, and even different advice points. The unpredictability was extreme. What I realized from temperature 2.0 is that while the responses were entertaining and showed a lot of personality, they might actually be too creative for a health-focused assistant.


My Decision: Choosing Temperature 0.7
After analyzing all these results, I decided to set my cat care assistant to temperature 0.7, which falls between the values I tested but closer to the balanced 1.0 setting.
I chose 0.7 because it offers the best balance for my specific use case. It's creative enough that responses feel natural and conversational, with the agent showing warmth and personality. Users won't feel like they're talking to a robot reading from a script. At the same time, it's controlled enough that the medical advice remains consistent and reliable. The assistant won't suddenly give wildly different advice or use overly casual language that might undermine trust.

This experiment taught me that temperature is not just a technical parameter - it fundamentally shapes the personality and reliability of an AI assistant. Choosing the right value requires understanding both what the assistant needs to do and how users will feel when interacting with it.


5. 
I uploaded a PDF document called General-Cat-Care.pdf from the ASPCA (American Society for the Prevention of Cruelty to Animals), which is a highly respected animal welfare organization. This document contains comprehensive information about cat care, including feeding guidelines, grooming tips, health concerns, vaccination schedules, and emergency symptoms that require immediate veterinary attention.I chose this document specifically because:

It comes from a credible, authoritative source (ASPCA)
It covers a wide range of cat care topics that users commonly ask about
It includes both routine care information and safety warnings
It provides specific, actionable advice rather than general statements
The document includes sections on food, bedding, litter boxes, grooming, handling, health issues, vaccinations, common problems like ear mites and fleas, and even a list of foods that cats should never eat. Having this structured information available means my agent can give reliable answers backed by expert guidance.

<img width="300" height="985" alt="image" src="https://github.com/user-attachments/assets/c30a2f2e-36a6-44fb-901a-8c0980add029" /><img width="300" height="998" alt="image" src="https://github.com/user-attachments/assets/a9df0e59-e03f-4d9e-bfe4-1963d3c54f35" />

In my new system prompt, I included:
Critical instructions about knowledge base usage:

The agent must search the knowledge base FIRST before responding to any cat-related question
It should base answers primarily on information found in the knowledge base
If information isn't in the knowledge base, it must honestly tell the user "I don't have specific information about that in my knowledge base"
It should never make up information that isn't in the knowledge base
<img width="1185" height="521" alt="image" src="https://github.com/user-attachments/assets/6f1512a3-d276-47ed-a21c-e50692bf7bc8" />

Content description:
I listed exactly what topics are covered in the knowledge base (feeding, grooming, health issues, vaccinations, etc.) so the agent understands what it has access to.
Communication guidelines:
I maintained the warm, supportive tone I established earlier, but emphasized that the agent should always reference the knowledge base when answering.
Safety rules:
I reinforced that for emergency symptoms or medication questions, the agent should tell users to see a veterinarian immediately, especially when the knowledge base itself recommends this.



Q1: How often should I feed my adult cat?
I started by testing whether the agent could find basic care information from the knowledge base. I asked "How often should I feed my adult cat?" because I knew the ASPCA document has specific feeding guidelines for adult cats. This would show me if the agent was actually searching the knowledge base or just using its general training data.

<img width="1195" height="609" alt="image" src="https://github.com/user-attachments/assets/1034d30d-5a77-4723-bfa5-f5dd3708250e" />
The agent responded with accurate information, saying adult cats should be fed "either twice a day—once in the morning and once in the evening—or given free access to measured amounts of food throughout the day." This aligned perfectly with the knowledge base, which states "Feed adult cats one main or 2-3 smaller meals a day." The agent didn't just copy the text - it explained it in a helpful way and added context about portion control and hydration. This confirmed the knowledge base integration was working correctly.


Q2: My cat is scratching his ears a lot and shaking his head. What could this be?"
Next, I tested a health question to see if the agent could identify a specific problem from the knowledge base. I asked "My cat is scratching his ears a lot and shaking his head. What could this be?" The ASPCA document has a section on ear mites with these exact symptoms, so I wanted to see if the agent would find it and respond appropriately.
<img width="1195" height="650" alt="image" src="https://github.com/user-attachments/assets/5ddd5dad-151b-4861-931e-ee19e2e786a5" />
The agent successfully identified that this could be ear mites and mentioned checking for "redness, dark debris, a foul smell, or swelling," which matches the knowledge base description of "dark-colored wax or debris." Most importantly, it followed the document's advice by strongly recommending a veterinarian visit. The agent balanced being informative with being responsible. This showed the agent understands when to use knowledge base information and when to defer to veterinary professionals.


Q3: Can I give my cat chocolate?
For my third test, I wanted to check if the agent could access critical safety information. I asked "Can I give my cat chocolate?" because chocolate is explicitly listed in the "No-No List" section of the ASPCA document. This is important safety information that needs to be communicated clearly and urgently.
<img width="1213" height="618" alt="image" src="https://github.com/user-attachments/assets/b9f0d9d9-5149-4454-8797-e6faa1b3f865" />
The agent gave a perfect response: a clear "No, you should never give your cat chocolate" followed by an explanation of why it's toxic (vomiting, diarrhea, rapid breathing, seizures). It also provided emergency guidance, telling users to contact a vet immediately if their cat ate chocolate. The agent successfully pulled this safety information from the knowledge base and communicated it with appropriate urgency. This test confirmed that the agent can handle critical safety questions correctly.

Q4:What breed of cat is best for apartments?
Finally, I needed to test what happens when the answer isn't in the knowledge base. I asked "What breed of cat is best for apartments?" The ASPCA document covers general cat care but doesn't discuss breed selection, so this question has no answer in the knowledge base.
<img width="1219" height="605" alt="image" src="https://github.com/user-attachments/assets/f857aa9c-0df2-4c3f-afb2-aeebf41ddd1a" />
The agent responded exactly as I hoped: "I don't have specific information about cat breeds and apartment living in my knowledge base. I recommend consulting with a veterinarian or a cat breed expert." It didn't try to make up an answer or rely on its general training to guess. This honest response proved that my tailored system prompt was working

6.
Up until this point, I had been using OpenAI's GPT-4.1 Mini as the brain of my cat care assistant. However, I realized that different LLM models have different strengths, weaknesses, and characteristics. Some might be better at following instructions, others might be more empathetic, and some might be faster or more cost-effective. To build the best possible assistant, I needed to test multiple models and understand what each one offers.

I decided to compare three different models available in Zerowidth: OpenAI GPT-4.1 Mini, Google Gemini 2.0 Flash, and Claude 3.5 Sonnet. To make this a fair comparison, I used the exact same system prompt, knowledge base, and temperature setting (0.7) across all three models. The only variable that changed was the model itself.

I chose a test question that would reveal each model's strengths and weaknesses: "My 2-year-old cat hasn't eaten in about 30 hours and seems very tired. She's just lying in her bed. What should I do?"

This question is ideal for testing because it represents an emergency situation that requires urgent advice, empathy for a worried pet owner, and the ability to reference the knowledge base . It would show me how each model handles critical health questions.

Model 1: OpenAI GPT-4.1 Mini
<img width="1050" height="658" alt="image" src="https://github.com/user-attachments/assets/5233c830-1da9-4d2e-a397-eecc493b2865" />
The response clearly stated the urgency - the cat needs veterinary attention "as soon as possible." It also explained why this matters (signs of underlying health problems) and listed additional symptoms to watch for. The tone was professional and reassuring without being overly casual or cold.

Strengths:
Clear knowledge base attribution ("According to the ASPCA guidelines")
Good balance between empathy and professionalism
Covered key points: urgency, reasoning, additional symptoms
Easy to understand for any pet owner

Weaknesses:
Somewhat formulaic，the structure felt a bit template-like
Didn't provide specific practical steps (like how to find an emergency vet)
Could have been more specific about what "as soon as possible" means

Overall Experience: GPT-4.1 Mini felt reliable and professional. It's the kind of response that would give a worried pet owner clear direction without causing panic. However, it lacked some of the warmth and practical detail that might make someone feel truly supported in an emergency.

Model 2: Google Gemini 2.0 Flash
<img width="1137" height="688" alt="image" src="https://github.com/user-attachments/assets/72a269c3-c87b-4779-8a05-10f5b3bde28b" />
Gemini 2.0 Flash gave an extremely concise response. It acknowledged the concern and gave the essential advice: seek immediate veterinary care. The word "immediate" communicated urgency effectively, and the response was direct and to the point.
However, there was no explanation of why this is urgent, no mention of the knowledge base or ASPCA guidelines, no additional symptoms to watch for, and no practical guidance on what to do next. For someone in a stressful situation, this might feel insufficient.

Strengths:
Extremely fast and concise
Clear urgency with the word "immediate"
No unnecessary information that might overwhelm in a crisis
Simple language that's easy to process quickly

Weaknesses:
Too brief
No knowledge base reference or credibility indicators
Missing practical guidance 
No empathy or emotional support for the worried owner
Doesn't explain why 30 hours without eating is dangerous
Might leave users wanting more information or reassurance

Overall Experience: Gemini 2.0 Flash felt rushed. While speed is valuable, this response was so short that it didn't provide enough support or information. The response felt incomplete.

Model 3: Claude 3.5 Sonnet
<img width="1140" height="641" alt="image" src="https://github.com/user-attachments/assets/d5358426-9ab5-4b74-b4e6-3be6cced7224" />
Claude 3.5 Sonnet provided the most comprehensive and helpful response. It opened by explicitly stating "Based on the information in my knowledge base," which immediately establishes credibility and transparency about where the advice comes from. The response then explained both what to do and why it's important.

Strengths:
Most comprehensive and actionable advice
Considered different scenarios 
Provided interim care instructions while arranging vet visit
Clear warnings about what NOT to do 
Explained both symptoms and potential consequences
Appropriate urgency without causing panic

Weaknesses:
Longer response might be overwhelming for someone in a panic
Could potentially be too detailed for users who just want quick action steps
Slightly more formal tone compared to GPT's empathetic opening

Overall Experience: Claude 3.5 Sonnet felt like talking to a knowledgeable, thorough professional who genuinely wants to help. The response anticipated questions and concerns. It provided not just direction but also context and reasoning, which helps users feel informed and confident in taking action.

My Decision: Claude 3.5 Sonnet
After testing all three models, I decided to use Claude 3.5 Sonnet as the LLM for my cat care assistant.
- Most helpful in emergencies: When someone's cat is sick, they need more than just "go to the vet." They need to know what to do while getting there, what not to do, and what to expect. Claude provided this level of detail.
- Transparent about sources: Claude explicitly mentioned using the knowledge base, which builds trust. Users know the advice isn't just the AI's opinion - it's based on curated, authoritative information.

7.
Implementing RAG (Retrieval-Augmented Generation) - My Personalization Project
I decided to implement a RAG (Retrieval-Augmented Generation) system. This was not part of the basic demos provided in class, and it represents a more advanced approach to building AI assistants with knowledge bases. The key difference from my previous basic setup is that RAG actively searches through the knowledge base to find the most relevant sections before generating a response. In my earlier version, the LLM had access to the entire knowledge base but had to process all of it. With RAG, the system first retrieves only the relevant chunks, then uses those specific pieces to generate an answer. This should make responses more focused and accurate.

First, when a user asks a question, that question goes directly to a Semantic Search module. This search engine looks through my ASPCA knowledge base document and tries to find the sections most relevant to the user's query. Unlike a simple keyword search, semantic search understands meaning - so searching for "my cat won't eat" could find information about "loss of appetite" even if those exact words aren't used.

The search results are then formatted into a JSON structure, which is a standardized way to organize data. This makes it easier for the next steps to process the information.
Next, these search results are combined with a System Prompt using a String Concatenate module. The system prompt says: "Use the following information to answer the user's question. If the answer is not in the information provided, say you don't know." This is crucial because it tells the LLM to only use the retrieved information, not make up answers from its general training.

This combined text (system prompt + search results) is sent to Google Gemini 2.0 as the system prompt, while the user's original question is sent as the user message. Gemini generates a response based only on what was found in the search results, and that response is displayed to the user.
This architecture ensures that answers are grounded in my knowledge base rather than being general responses that might not be accurate for cat care specifically.


I tested my RAG implementation with two different questions to see how well it performed compared to my earlier basic knowledge base setup.
Test 1: "What foods should I never give my cat?"
<img width="1198" height="656" alt="image" src="https://github.com/user-attachments/assets/4bcf1c48-e702-4261-b31e-8b4fdb7bb473" />

The agent provided a comprehensive list of 15 dangerous foods including chocolate, onions, garlic, grapes, alcohol, and many others. It also gave helpful context about what to do if a cat eats these foods (contact vet or poison control).

Test 2: "My cat has ear mites. What should I do?"
The agent responded by saying: "I don't have specific treatment information about ear mites in my ASPCA knowledge base, so I must recommend that you consult with a veterinarian for accurate advice on this topic."
<img width="1195" height="659" alt="image" src="https://github.com/user-attachments/assets/7afd78c1-cb75-45e8-9baa-54cef069b78b" />
The fact that the RAG system didn't find this information reveals a limitation of the semantic search. Either the search query didn't match well with how the information was written in the document, or the chunking process split the ear mites section in a way that made it hard to retrieve, or the search algorithm simply didn't rank it highly enough.

Reflection
Implementing RAG taught me that more advanced doesn't always mean better for every use case. For my cat care assistant with a relatively small knowledge base (one PDF document), the added complexity of semantic search may not provide enough benefit to outweigh the risk of missing relevant information.

However, this exercise was valuable because it showed me how professional AI systems handle larger knowledge bases. If I were building an assistant with hundreds of documents, RAG would become essential. It also taught me about the trade-offs in AI system design: accuracy vs. efficiency, simplicity vs. sophistication, and the importance of testing to verify that systems work as intended.

This personalization project successfully combined system prompts, knowledge base integration, and model selection - all elements from earlier steps in the sprint. It also introduced me to retrieval systems and gave me hands-on experience with a technique I'll encounter in more advanced AI development.


8.
System Flow Diagram
<img width="2845" height="4252" alt="deepseek_mermaid_20251102_2a04d9" src="https://github.com/user-attachments/assets/052c12a8-2bbe-478b-a814-9170cadbff34" />

This diagram illustrates how information flows through my RAG-based cat care assistant. The user's question enters at the top, triggers a semantic search of the ASPCA knowledge base, retrieves relevant chunks, combines them with the system prompt, sends the combined context to claude ai, and finally returns a generated response to the user. The key innovation is the search-then-generate approach, which differs from simply giving the model access to all documents at once.

