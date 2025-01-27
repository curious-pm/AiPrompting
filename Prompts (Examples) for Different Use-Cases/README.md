## Join the Community  
### [Join Curious PM Community](https://curious.pm/) to connect, share, and learn with others!


# **Prompts (Examples) for Different Use-Cases**

## **Overview**  
This guide explains how developers can integrate AI prompting techniques into their applications to solve real-world problems, such as **audio transcription, text extraction, summarization, and chatbot development.** The examples demonstrate different prompt types and how to implement them programmatically.

---

## **How to Use Prompts in Your Code**  

To integrate AI prompting into your applications, follow these steps:

1. **Set up an AI API (e.g., OpenAI, Google Gemini, Anthropic Claude).**  
2. **Prepare the prompt dynamically in your code.**  
3. **Send the prompt to the AI API and retrieve the response.**  
4. **Process and use the AI-generated output in your application.**

---

### **Setting Up the Environment for Streamlit with Azure OpenAI API**

To set up the environment for running Streamlit applications using Azure OpenAI API, follow these steps:

---

#### **1. Install Required Dependencies**  
Ensure you have installed the necessary Python packages:

```bash
pip install streamlit requests PyPDF2
```

---

#### **2. Set Up API Credentials Securely Using Streamlit Secrets**  

1. **Create a `.streamlit/secrets.toml` file** in your project directory and add your API credentials:

    ```toml
    AZURE_OPENAI_API_ENDPOINT = "https://your-endpoint.openai.azure.com"
    AZURE_OPENAI_API_KEY = "your-secret-api-key"
    ```

2. **Load the credentials securely in your Streamlit application:**

    ```python
    import streamlit as st
    import requests

    class AzureOpenAIChat:
        def __init__(self):
            self.API_ENDPOINT = st.secrets["AZURE_OPENAI_API_ENDPOINT"]
            self.API_KEY = st.secrets["AZURE_OPENAI_API_KEY"]
    ```

---

#### **3. Run Your Streamlit Application**  

Once everything is set up, run your Streamlit application by executing the following command:

```bash
streamlit run your_script.py
```

---
### **Understanding the Syntax of AI Prompting in Code**

Before diving into the examples, let's break down the core syntax used when interacting with AI models such as OpenAI's GPT through API calls.

---

### **1. Defining the Prompt**  
The prompt is a textual input that tells the AI what task to perform. In Python, we define it as a string variable.

```python
prompt = "Transcribe the following audio file and provide a summary of key points."
```

**Explanation:**  
- `prompt` → The variable holding the instruction to the AI.  
- The text inside the quotes is what guides the AI to generate relevant responses.

---

### **2. Making an API Call to OpenAI**  

The core function for interacting with the AI model is:

```python
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": prompt}],
    max_tokens=300
)
```

#### **Breaking it down:**

- **`client.chat.completions.create(...)`** → This function sends the request to the OpenAI API and retrieves the response.

#### **Parameters Explained:**

1. **`model="gpt-4"`**  
   - Specifies which AI model to use (e.g., GPT-4 for more advanced reasoning and responses).  
   - You can replace `"gpt-4"` with `"gpt-3.5-turbo"` for a cheaper, faster model if needed.

2. **`messages=[{"role": "user", "content": prompt}]`**  
   - `messages` is a list that contains the conversation history or user inputs.  
   - `role: "user"` indicates that the prompt is coming from the user.  
   - `content: prompt` passes the defined instruction to the AI.  

   Example breakdown:
   ```python
   messages = [
       {"role": "user", "content": "What is machine learning?"}
   ]
   ```

3. **`max_tokens=300`**  
   - Limits the maximum number of tokens (words, symbols, or characters) in the AI's response.  
   - A higher value allows for longer, more detailed answers, while a lower value keeps responses brief.

---

### **3. Printing the Response**  

Once the AI generates a response, it needs to be extracted and displayed:

```python
print(response.choices[0].message.content)
```

**Explanation:**  
- `response.choices[0]` → Accesses the first generated response from the AI.  
- `.message.content` → Retrieves the text response from the AI's reply.

**Expected Output Example:**  
```plaintext
Key points from the audio:
1. The meeting discussed project deadlines and new goals.
2. Budget allocations were finalized.
3. Team collaboration strategies were emphasized.
```
---

### **Key Points**

1. **Define a clear prompt** – This guides the AI effectively.  
2. **Choose the right model** – Balance cost, speed, and accuracy.  
3. **Set appropriate token limits** – Optimize responses based on your needs.  
4. **Extract the right response** – Always check the structure of the AI's output.

---

## **Implementing Different Types of Prompts in Real-World Scenarios**


Here are **Streamlit-based AI app examples** for each type of prompt, including implementation and expected outputs.

---

## **1. Zero-Shot Prompting - Audio Transcription**

### **Description:**  
Zero-shot prompting to convert an audio file to text without prior examples.

### **Implementation:**
```python
import streamlit as st
import requests

class AzureOpenAIChat:
    def __init__(self):
        self.API_ENDPOINT = st.secrets.get("AZURE_OPENAI_API_ENDPOINT", "")
        self.API_KEY = st.secrets.get("AZURE_OPENAI_API_KEY", "")

    def generate_response(self, query: str, max_tokens: int = 300):
        headers = {"Content-Type": "application/json", "api-key": self.API_KEY}
        data = {"messages": [{"role": "user", "content": query}], "max_tokens": max_tokens}
        response = requests.post(self.API_ENDPOINT, headers=headers, json=data)
        response.raise_for_status()
        return response.json()

def main():
    st.set_page_config(page_title="Audio Transcription", page_icon="🎤")
    st.title("Audio to Text Transcription")

    uploaded_file = st.file_uploader("Upload an audio file", type=["mp3", "wav"])
    if uploaded_file:
        with st.spinner("Transcribing audio..."):
            chat_client = AzureOpenAIChat()
            response = chat_client.generate_response("Transcribe this audio.")
            if response and "choices" in response:
                transcript = response["choices"][0]["message"]["content"]
                st.success("Transcription completed!")
                st.text_area("Transcription", transcript)
            else:
                st.error("Failed to transcribe audio.")

if __name__ == "__main__":
    main()
```

### **Expected Output:**
```plaintext
Key points from the audio:
- The speaker discussed project timelines.
- A budget review was conducted.
- Action items were assigned to the marketing team.
```

---

## **2. One-Shot Prompting - PDF Text Extraction**

### **Description:**  
Extracting key details from a PDF with a single example guiding the AI.

### **Implementation:**
```python
import streamlit as st
import requests
from PyPDF2 import PdfReader

def extract_text_from_pdf(uploaded_file):
    reader = PdfReader(uploaded_file)
    return "\n".join(page.extract_text() for page in reader.pages)

def main():
    st.set_page_config(page_title="PDF Extractor", page_icon="📄")
    st.title("Extract Key Details from PDF")

    uploaded_file = st.file_uploader("Upload a PDF file", type="pdf")
    if uploaded_file:
        pdf_text = extract_text_from_pdf(uploaded_file)
        prompt = f"""
        Example: Given the document 'invoice.pdf', extract details such as invoice number, date, and total amount.
        Now, process the following text:\n{pdf_text}
        """

        chat_client = AzureOpenAIChat()
        response = chat_client.generate_response(prompt)
        if response and "choices" in response:
            extracted_info = response["choices"][0]["message"]["content"]
            st.text_area("Extracted Information", extracted_info)
        else:
            st.error("Failed to extract key details.")

if __name__ == "__main__":
    main()
```

### **Expected Output:**
```plaintext
Invoice Details:
- Invoice Number: INV-2024001
- Date: 01/01/2024
- Total Amount: $5,000
```

---

## **3. Few-Shot Prompting - Document Summarization**

### **Description:**  
Summarizing text with multiple examples provided for guidance.

### **Implementation:**
```python
import streamlit as st
import requests

def main():
    st.set_page_config(page_title="Text Summarizer", page_icon="📝")
    st.title("Summarize Reports")

    text_input = st.text_area("Paste your document here:", height=200)
    if st.button("Summarize"):
        prompt = f"""
        Example 1: Summarize the financial report in bullet points:
        - Revenue grew by 10%.
        - Expansion into new markets.
        
        Example 2: Summarize the marketing report:
        - Increased social media engagement.
        - New campaign launched.

        Now, summarize the following document:\n{text_input}
        """
        
        chat_client = AzureOpenAIChat()
        response = chat_client.generate_response(prompt)
        if response and "choices" in response:
            summary = response["choices"][0]["message"]["content"]
            st.text_area("Summary", summary)
        else:
            st.error("Failed to generate summary.")

if __name__ == "__main__":
    main()
```

### **Expected Output:**
```plaintext
- The company's revenue increased by 20%.
- New partnerships were established in Europe.
- Cost efficiency improved by 15%.
```

---

## **4. Chain-of-Thought Prompting - IT Support Chatbot**

### **Description:**  
A troubleshooting chatbot that breaks the problem down step by step.

### **Implementation:**
```python
import streamlit as st
import requests

def main():
    st.set_page_config(page_title="AI Troubleshooter", page_icon="🛠️")
    st.title("AI Troubleshooting Assistant")

    issue = st.text_input("Describe your issue:")
    if st.button("Get Solution"):
        prompt = f"""
        Let's solve the issue step by step.
        The user reports the issue: {issue}

        Step 1: Check power connection.
        Step 2: Restart the device.
        Step 3: Update software if needed.
        Step 4: Contact support if issue persists.
        """
        
        chat_client = AzureOpenAIChat()
        response = chat_client.generate_response(prompt)
        if response and "choices" in response:
            solution = response["choices"][0]["message"]["content"]
            st.text_area("Solution", solution)
        else:
            st.error("Failed to provide troubleshooting steps.")

if __name__ == "__main__":
    main()
```

### **Expected Output:**
```plaintext
Step 1: Ensure the device is properly connected to a power source.
Step 2: Restart the device and check if the issue persists.
Step 3: Update the software to the latest version.
Step 4: If the issue continues, contact technical support.
```

---

## **5. Instruction-Based Prompting - Fitness Plan Generator**

### **Description:**  
Generating a personalized fitness plan with clear instructions.

### **Implementation:**
```python
import streamlit as st
import requests

def main():
    st.set_page_config(page_title="Fitness Plan", page_icon="💪")
    st.title("AI-Powered Fitness Plan")

    goal = st.selectbox("Select your fitness goal:", ["Weight Loss", "Muscle Gain", "General Fitness"])
    experience = st.selectbox("Experience Level:", ["Beginner", "Intermediate", "Advanced"])
    
    if st.button("Generate Plan"):
        prompt = f"Generate a {goal.lower()} workout plan for a {experience.lower()} person, 3 days a week."
        
        chat_client = AzureOpenAIChat()
        response = chat_client.generate_response(prompt)
        if response and "choices" in response:
            plan = response["choices"][0]["message"]["content"]
            st.text_area("Your Personalized Plan", plan)
        else:
            st.error("Failed to generate plan.")

if __name__ == "__main__":
    main()
```

### **Expected Output:**
```plaintext
Week 1-2:  
- 30 min cardio (3 times a week)  
- Strength training (light weights)  

Week 3-4:  
- Increase cardio duration to 45 min  
- Moderate strength training (increase reps)
```

---

Here are additional examples for **Contextual Prompting** and **Prompt Chaining**, implemented in **Streamlit** with **Azure OpenAI API**, including code and expected console outputs.

---

## **6. Contextual Prompting - Email Classification**

### **Description:**  
Provide background information to AI for classifying emails based on categories like Work, Personal, or Promotions.

### **Implementation:**
```python
import streamlit as st
import requests

class AzureOpenAIChat:
    def __init__(self):
        self.API_ENDPOINT = st.secrets.get("AZURE_OPENAI_API_ENDPOINT", "")
        self.API_KEY = st.secrets.get("AZURE_OPENAI_API_KEY", "")

    def generate_response(self, query: str, max_tokens: int = 300):
        headers = {"Content-Type": "application/json", "api-key": self.API_KEY}
        data = {"messages": [{"role": "user", "content": query}], "max_tokens": max_tokens}
        response = requests.post(self.API_ENDPOINT, headers=headers, json=data)
        response.raise_for_status()
        return response.json()

def main():
    st.set_page_config(page_title="Email Classifier", page_icon="📧")
    st.title("AI Email Classification")

    email_subject = st.text_input("Enter email subject:")
    email_body = st.text_area("Enter email body:")

    if st.button("Classify Email"):
        prompt = f"""
        You are an email assistant. Classify the following email based on categories such as 'Work', 'Personal', or 'Promotions'.
        Subject: {email_subject}
        Body: {email_body}
        """

        chat_client = AzureOpenAIChat()
        response = chat_client.generate_response(prompt)

        if response and "choices" in response:
            category = response["choices"][0]["message"]["content"]
            st.success(f"Email Category: {category}")
        else:
            st.error("Failed to classify the email.")

if __name__ == "__main__":
    main()
```

### **Expected Output (Console):**
```plaintext
Email Category: Promotions  
Reason: Contains discount offers and sales-related content.
```

---

## **7. Prompt Chaining - Travel Itinerary Planning**

### **Description:**  
Breaking down a complex task (like planning travel) into smaller sequential prompts.

### **Implementation:**
```python
import streamlit as st
import requests

class AzureOpenAIChat:
    def __init__(self):
        self.API_ENDPOINT = st.secrets.get("AZURE_OPENAI_API_ENDPOINT", "")
        self.API_KEY = st.secrets.get("AZURE_OPENAI_API_KEY", "")

    def generate_response(self, query: str, max_tokens: int = 300):
        headers = {"Content-Type": "application/json", "api-key": self.API_KEY}
        data = {"messages": [{"role": "user", "content": query}], "max_tokens": max_tokens}
        response = requests.post(self.API_ENDPOINT, headers=headers, json=data)
        response.raise_for_status()
        return response.json()

def main():
    st.set_page_config(page_title="Travel Planner", page_icon="🌍")
    st.title("AI Travel Itinerary Planner")

    destination = st.text_input("Enter your travel destination:")
    duration = st.slider("Number of days", min_value=1, max_value=14, value=5)

    if st.button("Plan Itinerary"):
        step1_prompt = f"Suggest a {duration}-day travel itinerary for {destination}."

        with st.spinner("Planning your trip..."):
            chat_client = AzureOpenAIChat()
            response1 = chat_client.generate_response(step1_prompt)

            if response1 and "choices" in response1:
                itinerary = response1["choices"][0]["message"]["content"]
                st.text_area("Suggested Itinerary", itinerary)

                # Chained prompt for restaurants
                step2_prompt = f"Based on this itinerary for {destination}, suggest restaurants for each day."

                response2 = chat_client.generate_response(step2_prompt)
                if response2 and "choices" in response2:
                    restaurants = response2["choices"][0]["message"]["content"]
                    st.text_area("Suggested Restaurants", restaurants)
                else:
                    st.error("Failed to fetch restaurant recommendations.")

if __name__ == "__main__":
    main()
```

### **Expected Output (Console):**
```plaintext
Day 1:  
- Visit the Eiffel Tower.  
- Explore the Louvre Museum.  
- Dine at Le Jules Verne.

Day 2:  
- Day trip to Versailles.  
- Evening boat ride on the Seine.

Suggested Restaurants:
Day 1: Le Meurice, Cafe de Flore  
Day 2: Angelina, Le Procope
```

---

## **Best Practices for Effective Prompting**  

- **Be Clear and Specific:** Provide detailed instructions to improve AI understanding.  
- **Iterate and Refine:** Adjust prompts based on output quality.  
- **Use Examples:** Guide AI with sample data or patterns.  
- **Break Complex Problems:** Split large tasks into smaller, manageable prompts. 