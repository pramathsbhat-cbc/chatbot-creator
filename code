import streamlit as st
import openai

st.set_page_config(page_title="AI Chatbot Creator", page_icon="🤖")

st.title("🤖 AI Chatbot Creator")
st.caption("Make your own chatbot by customizing its personality, tone, and role!")

# Sidebar for customization
st.sidebar.header("🎨 Customize Your Chatbot")
chatbot_name = st.sidebar.text_input("Chatbot Name", "Chatter")
chatbot_tone = st.sidebar.selectbox("Tone", ["Friendly", "Formal", "Funny", "Sarcastic", "Motivational"])
chatbot_role = st.sidebar.text_input("Bot Role (e.g., tutor, therapist, friend)", "Study Buddy")

# OpenAI API Key input
openai_api_key = st.sidebar.text_input("🔑 OpenAI API Key", type="password")

user_input = st.text_input("💬 Ask your chatbot something...")

def generate_prompt(tone, role, name, user_msg):
    return f"""
You are an AI chatbot named {name}, designed to be a {role}. 
Your tone should be {tone.lower()}. Answer the following message accordingly:

User: {user_msg}
{name}:"""

if user_input and openai_api_key:
    prompt = generate_prompt(chatbot_tone, chatbot_role, chatbot_name, user_input)

    try:
        openai.api_key = openai_api_key
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=prompt,
            max_tokens=150,
            temperature=0.7,
        )
        bot_reply = response.choices[0].text.strip()
        st.markdown(f"**{chatbot_name}:** {bot_reply}")
    except Exception as e:
        st.error(f"⚠️ Error: {str(e)}")
elif user_input:
    st.warning("Please enter your OpenAI API key in the sidebar.")
