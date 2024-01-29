# Concept search powered by Large Language Models

In this repository, I explore the Idea of a concept search with Large Language Models.  
Instead of an exact word match or an intelligent full-text search, I search the text for representing a concept or Idea. In this experiment, I search in the Bible, if the concept of __seeking discomfort__ is represented there.  
For this, I go through every verse and let a large Language Model rate how much this verse represents the concept of seeking discomfort.
With this technique, I will also discover verses like Matthew 7:13-14
> 13 “Enter through the narrow gate. For wide is the gate and broad is the road that leads to destruction, and many enter through it. 14 But small is the gate and narrow the road that leads to life, and only a few find it.

I think this verse represents the Idea of seeking discomfort well, but there is no intelligent search available, that would be able to find this.

## Prompt Engineering

I use the following system prompt:
> """You are an expert in the use of the english language. You will get single verse of the bible as an input and answer with a single number from 0 to 100, representing
how much the bible verse says about the concept of seeking discomfort. It is not relevant if the verse suggest that seeking discomfort is good or bad, it is about if the bible verse says anything about seeking discomfort in general.  
As guidance:  
'Book 1:30: And the Lord said you shall seek discomfort in all aspects of your life' -> very high score  
'Book 1:30: And the Lord said you should make sure, that you never venture out of your comfort zone' -> very high score  
'Book 1:30: Marc felt uncomfortable' -> high score  
'Book 1:30: Marc built himself a cosy bed, so that he can live comfortably' -> high score  
'Book 1:30: Jesus made a difficult ride of 2 days to the next city' -> medium score  
'Book 1:30: And so Jesus made water to wine' -> low score  
For the next prompt you will answer with only one number (0 to 100). 0 represents the lowest correlation to the concept of seeking comfort or
seeking discomfort and 100 represents the highest correletin to the concept of seeking comfort or seeking discomfort.
Only answer with a single number. Do NOT answer with any explanation or context.
"""

I prime the model with "You are an expert in the use of the English language" to make sure, it focuses just on the interpretation of verse and not on its prior knowledge of the bible or Christianity.  
I give it a few examples without giving out exact numbers, to hopefully improve the performance.

## Authenticastion

### Google Cloud

Create a Service account
<https://console.cloud.google.com/iam-admin/serviceaccounts?hl=en>  
add the role for Vertex-AI-User  
open service account  
select KEYS  
Create New Key
Then the credentials.json file is downloaded  
Save it somewhere  
Then put the path to that file into the environment Variable

```python
os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = 'C:/Git_Repos/try-out-vertex-ai-20aaf5516b7c.json' 
# os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = '/mnt/c/Git_Repos/try-out-vertex-ai-20aaf5516b7c.json'  
```

## OpenAI

get the API key from <https://platform.openai.com/api-keys>
and then add it to your environment.

```python
os.environ["OPENAI_API_KEY"] = "your-api-key-here"

```

## Lessons learned

Their safety is annoying!

Google safety setting
<https://ai.google.dev/tutorials/python_quickstart#safety_settings>
You can remove the blocking by setting safety settings:  
<https://stackoverflow.com/questions/77723993/gemini-pro-api-blocking-replies>
I get rate-limited on PaLM 2 and GeminiPro.
maximum of 60 Requests per minute
<https://cloud.google.com/vertex-ai/docs/generative-ai/quotas-genai?hl=en>  
I could request to up the limit
in the meantime, the limit was lifted

on the Gemini Pro requests, I randomly get some annoying grpc error.
