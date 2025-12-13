# 5.3 Integrating AI with Existing APIs

## 📋 Learning Objectives
By the end of this module, you will be able to:
- Understand Function Calling (Tool Use) in LLMs
- Integrate external APIs with AI agents
- Build tools that LLMs can use autonomously
- Handle API responses and errors gracefully
- Create a Smart Assistant that uses real-world APIs

**Estimated Time:** Week 3-4 (8-10 hours)

---

## 📘 Theory Section (50%)

### The Problem: LLMs Are Isolated

LLMs are incredibly smart, but they live in a bubble:
- ❌ Can't check real-time weather
- ❌ Can't look up stock prices
- ❌ Can't query your database
- ❌ Can't send emails

**Function Calling** gives LLMs "hands" to interact with the world.

### What is Function Calling?

Instead of just generating text, the LLM can output **structured instructions** to call functions.

```mermaid
graph LR
    A[User: "What's the weather in NYC?"] --> B[LLM]
    B --> C{Decision}
    C -->|Text Response| D["I don't have real-time data"]
    C -->|Function Call| E[Call get_weather NYC]
    E --> F[Execute API]
    F --> G[Return: 72°F, Sunny]
    G --> B
    B --> H["It's currently 72°F and sunny in NYC"]
```

### How It Works

#### Step 1: Define Available Tools

```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get current weather for a city",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "City name, e.g., New York"
                    },
                    "unit": {
                        "type": "string",
                        "enum": ["celsius", "fahrenheit"]
                    }
                },
                "required": ["city"]
            }
        }
    }
]
```

#### Step 2: LLM Chooses to Call Function

```json
{
  "role": "assistant",
  "content": null,
  "tool_calls": [{
    "function": {
      "name": "get_weather",
      "arguments": "{\"city\": \"New York\", \"unit\": \"fahrenheit\"}"
    }
  }]
}
```

#### Step 3: You Execute the Function

```python
def get_weather(city, unit="fahrenheit"):
    # Call real weather API
    response = requests.get(f"https://api.weather.com/v1/{city}")
    return response.json()
```

#### Step 4: Send Result Back to LLM

```python
messages.append({
    "role": "tool",
    "content": '{"temp": 72, "condition": "Sunny"}'
})

# LLM generates final answer
final_response = llm(messages)
```

### Function Calling vs. Traditional APIs

| Traditional Chatbot | With Function Calling |
|---------------------|----------------------|
| Static responses | Dynamic, real-time data |
| Limited to training data | Access to any API |
| Can't take actions | Can execute tasks |

### Real-World Use Cases

1. **Customer Support**
   - Check order status
   - Update account info
   - Create support tickets

2. **Finance**
   - Get stock prices
   - Calculate investments
   - Fetch exchange rates

3. **E-Commerce**
   - Search products
   - Check inventory
   - Place orders

4. **Productivity**
   - Send emails
   - Create calendar events
   - Query databases

---

## 🧪 Lab Section (50%)

### Lab 1: Function Calling Basics (OpenAI)

**Objective**: Make your first function call

```python
# lab_function_calling.py
from openai import OpenAI
import json
from dotenv import load_dotenv

load_dotenv()
client = OpenAI()

# Define a simple function
def get_current_time(timezone="UTC"):
    """Get current time for a timezone."""
    from datetime import datetime
    import pytz
    tz = pytz.timezone(timezone)
    return datetime.now(tz).strftime("%H:%M:%S")

# Define tool schema
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_current_time",
            "description": "Get the current time in a specific timezone",
            "parameters": {
                "type": "object",
                "properties": {
                    "timezone": {
                        "type": "string",
                        "description": "Timezone name, e.g., America/New_York"
                    }
                },
                "required": ["timezone"]
            }
        }
    }
]

# Create chat completion
messages = [{"role": "user", "content": "What time is it in Tokyo?"}]

response = client.chat.completions.create(
    model="gpt-4",
    messages=messages,
    tools=tools,
    tool_choice="auto"
)

# Check if function was called
if response.choices[0].message.tool_calls:
    tool_call = response.choices[0].message.tool_calls[0]
    function_name = tool_call.function.name
    arguments = json.loads(tool_call.function.arguments)
    
    print(f"LLM wants to call: {function_name}({arguments})")
    
    # Execute function
    if function_name == "get_current_time":
        result = get_current_time(**arguments)
        print(f"Function returned: {result}")
        
        # Send result back to LLM
        messages.append(response.choices[0].message)
        messages.append({
            "role": "tool",
            "tool_call_id": tool_call.id,
            "content": result
        })
        
        # Get final response
        final_response = client.chat.completions.create(
            model="gpt-4",
            messages=messages
        )
        
        print(f"Final answer: {final_response.choices[0].message.content}")
```

### Lab 2: Multi-Function Agent

**Objective**: Build an agent with multiple tools

```python
# lab_multi_tool_agent.py
import json
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI()

# Define multiple functions
def calculate_tip(bill_amount, tip_percentage=15):
    """Calculate tip amount."""
    return round(bill_amount * (tip_percentage / 100), 2)

def convert_currency(amount, from_currency, to_currency):
    """Convert currency (mock data)."""
    rates = {"USD_EUR": 0.85, "EUR_USD": 1.18, "USD_GBP": 0.73}
    key = f"{from_currency}_{to_currency}"
    return round(amount * rates.get(key, 1), 2)

# Define tools
tools = [
    {
        "type": "function",
        "function": {
            "name": "calculate_tip",
            "description": "Calculate tip for a bill",
            "parameters": {
                "type": "object",
                "properties": {
                    "bill_amount": {"type": "number"},
                    "tip_percentage": {"type": "number"}
                },
                "required": ["bill_amount"]
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "convert_currency",
            "description": "Convert between currencies",
            "parameters": {
                "type": "object",
                "properties": {
                    "amount": {"type": "number"},
                    "from_currency": {"type": "string"},
                    "to_currency": {"type": "string"}
                },
                "required": ["amount", "from_currency", "to_currency"]
            }
        }
    }
]

# Function registry
FUNCTIONS = {
    "calculate_tip": calculate_tip,
    "convert_currency": convert_currency
}

def run_agent(user_message):
    """Run the agent with function calling."""
    messages = [{"role": "user", "content": user_message}]
    
    while True:
        response = client.chat.completions.create(
            model="gpt-4",
            messages=messages,
            tools=tools
        )
        
        message = response.choices[0].message
        
        # If no tool calls, we're done
        if not message.tool_calls:
            return message.content
        
        # Execute each tool call
        messages.append(message)
        for tool_call in message.tool_calls:
            function_name = tool_call.function.name
            arguments = json.loads(tool_call.function.arguments)
            
            print(f"📞 Calling: {function_name}({arguments})")
            
            # Execute function
            result = FUNCTIONS[function_name](**arguments)
            
            # Add result to messages
            messages.append({
                "role": "tool",
                "tool_call_id": tool_call.id,
                "content": str(result)
            })

# Test
print(run_agent("My bill is $50, what's a 20% tip?"))
print(run_agent("Convert 100 USD to EUR"))
```

### 🎯 Mini Project 2: Smart Weather Assistant

**Objective**: Build a weather assistant using a real API

**Requirements**:
1. Use OpenWeatherMap API (free tier)
2. Support multiple cities
3. Handle errors gracefully
4. Return formatted weather info

**Starter Code**:

```python
# weather_assistant.py
import os
import json
import requests
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI()

WEATHER_API_KEY = os.getenv("OPENWEATHER_API_KEY")

def get_weather(city, units="metric"):
    """Fetch real weather data from OpenWeatherMap."""
    try:
        url = f"http://api.openweathermap.org/data/2.5/weather"
        params = {
            "q": city,
            "appid": WEATHER_API_KEY,
            "units": units
        }
        response = requests.get(url, params=params)
        response.raise_for_status()
        
        data = response.json()
        return {
            "city": data["name"],
            "temperature": data["main"]["temp"],
            "condition": data["weather"][0]["description"],
            "humidity": data["main"]["humidity"]
        }
    except Exception as e:
        return {"error": str(e)}

# TODO: Define tools schema for get_weather

tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get current weather for a city",
            "parameters": {
                # TODO: Define parameters
            }
        }
    }
]

def weather_chat():
    """Interactive weather chatbot."""
    print("🌤️  Weather Assistant (type 'quit' to exit)")
    messages = []
    
    while True:
        user_input = input("\nYou: ")
        if user_input.lower() == 'quit':
            break
            
        messages.append({"role": "user", "content": user_input})
        
        # TODO: Implement the agent loop
        # 1. Call LLM with tools
        # 2. If tool_calls, execute get_weather
        # 3. Send result back
        # 4. Print final response

if __name__ == "__main__":
    weather_chat()
```

**Extension Challenges**:
1. Add weather forecast (5-day)
2. Support temperature unit preferences
3. Add location auto-complete
4. Cache API results to save requests

---

## 🔧 Advanced Patterns

### Pattern 1: Error Handling

```python
def safe_function_call(func, **kwargs):
    """Wrap function calls with error handling."""
    try:
        return {"success": True, "data": func(**kwargs)}
    except Exception as e:
        return {"success": False, "error": str(e)}
```

### Pattern 2: Rate Limiting

```python
from functools import lru_cache
import time

@lru_cache(maxsize=100)
def cached_api_call(city):
    """Cache results for 5 minutes."""
    return get_weather(city)
```

### Pattern 3: Async Function Calling

```python
import asyncio

async def async_get_weather(city):
    """Non-blocking API calls."""
    # Use aiohttp for async requests
    pass
```

---

## 📚 Resources & References

### Documentation
- [OpenAI Function Calling Guide](https://platform.openai.com/docs/guides/function-calling)
- [LangChain Tools & Agents](https://python.langchain.com/docs/modules/agents/)

### APIs to Try
- [OpenWeatherMap](https://openweathermap.org/api) - Weather data
- [Alpha Vantage](https://www.alphavantage.co/) - Stock prices
- [NewsAPI](https://newsapi.org/) - News articles
- [ExchangeRate-API](https://www.exchangerate-api.com/) - Currency conversion

### Best Practices
- Always validate function outputs before sending to LLM
- Use descriptive function names and parameter descriptions
- Implement timeouts for API calls
- Log all function calls for debugging

---

## ✅ Knowledge Check

Before moving to the next module, ensure you can:
- [ ] Explain how function calling works
- [ ] Define tool schemas correctly
- [ ] Execute functions based on LLM responses
- [ ] Handle errors in function calls
- [ ] Complete the Weather Assistant mini-project

---

**Next Module**: [5.4 Examples: Chat with PDF](../5.4_Chat_With_PDF/content.md)
