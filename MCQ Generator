from openai import OpenAI
from getpass import getpass

# Step 3: Set up OpenRouter API client
def setup_openrouter_client():
    api_key = getpass("Enter your OpenRouter API key: ")
    
    client = OpenAI(
        base_url="https://openrouter.ai/api/v1",
        api_key=api_key,
    )
    return client

# Step 4: Create MCQ generation function
def generate_mcqs(client, topic):
    prompt = f"""Generate 10 high-quality multiple-choice questions about {topic}.
    Each question should:
    - Have 4 plausible options (A-D)
    - Clearly indicate the correct answer
    - Be conceptually accurate
    - Avoid trivial or obvious questions
    
    Format each question like this:
    [Question number]. [Question text]
    A) [Option A]
    B) [Option B]
    C) [Option C]
    D) [Option D]
    Correct Answer: [Letter]
    
    Separate questions with a blank line."""

    try:
        completion = client.chat.completions.create(
            extra_headers={
                "HTTP-Referer": "https://colab.research.google.com",
                "X-Title": "MCQ Generator",
            },
            model="meta-llama/llama-3.2-3b-instruct:free",
            messages=[
                {"role": "user", "content": prompt}
            ],
            temperature=0.7,
            max_tokens=2000
        )
        return completion.choices[0].message.content
    except Exception as e:
        return f"An error occurred: {str(e)}"

# Step 5: Main execution flow
def main():
    client = setup_openrouter_client()
    topic = input("Enter the topic for MCQs: ").strip()
    
    print("\nGenerating MCQs...\n")
    mcqs = generate_mcqs(client, topic)
    
    print(f"10 MCQs about {topic}:\n")
    print(mcqs)

# Run the program
if __name__ == "__main__":
    main()
