# Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

## AIM:
To design and implement a Python function for calculating the volume of a cylinder and integrate it with a chat-based system that uses the function-calling feature of a large language model (LLM).

## Problem Statement:
Design and integrate a Python function that calculates the volume of a cylinder, and enable the function to be called through a chat completion system, simulating an LLM interface.

## Design Steps:

### STEP 1: Design the Python Function for Volume Calculation
The volume of a cylinder can be calculated using the formula:

\[
V = \pi r^2 h
\]

Where:
- \(V\) is the volume of the cylinder.
- \(r\) is the radius of the base of the cylinder.
- \(h\) is the height of the cylinder.
- \(\pi\) is approximately 3.14159.

### STEP 2: Create a Chat Completion System
The chat system will:
- Take user input as queries.
- Detect when the user wants to calculate the volume of a cylinder.
- Call the volume calculation function when the user provides the required parameters (radius and height).

### STEP 3: Integrate the Function with the LLM's Function-Calling Feature
In a system utilizing an LLM with function-calling capabilities:
- The function must be defined to be invoked through the LLM interface.
- The LLM must be able to extract values for radius and height from the user’s query and pass them to the function.

## Program:

```python
import openai
import math

# Step 1: Function to calculate volume of a cylinder
def calculate_cylinder_volume(radius: float, height: float) -> float:
    """
    Calculate the volume of a cylinder using the formula: V = πr²h
    :param radius: Radius of the base of the cylinder
    :param height: Height of the cylinder
    :return: Volume of the cylinder
    """
    return math.pi * radius**2 * height

# Step 2: Initialize OpenAI API with your API key
openai.api_key = 'your-api-key'  # Replace with your OpenAI API key

# Step 3: Create a function that utilizes OpenAI's model to interact with the user
def chat_with_openai(query: str):
    """
    Use OpenAI's GPT model to process the query and call the function for cylinder volume calculation.
    :param query: User's query requesting volume calculation
    :return: The response from GPT model
    """
    # Call the OpenAI model to process the query with the messages format
    response = openai.ChatCompletion.create(
        model="gpt-4",  # You can change this to gpt-3.5 or another available model
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": query}
        ]
    )

    # Extract the answer from the response
    answer = response['choices'][0]['message']['content'].strip()

    # If the response contains a request for volume calculation, extract parameters and compute
    if "volume of a cylinder" in query.lower():
        try:
            # Extract the radius and height from the query (assume a simple format)
            radius = float(query.split("radius of ")[1].split(" ")[0])
            height = float(query.split("height of ")[1].split(" ")[0])
            volume = calculate_cylinder_volume(radius, height)
            return f"The volume of the cylinder is {volume:.2f} cubic units."
        except (IndexError, ValueError):
            return "Sorry, I couldn't extract the radius and height from your query. Please provide them clearly."
    else:
        return answer

# Example of using the OpenAI chat system with an LLM interface
user_query = "What is the volume of a cylinder with a radius of 5 cm and a height of 10 cm?"
response = chat_with_openai(user_query)
print(response)
```
## Output:
![image](https://github.com/user-attachments/assets/9da5f831-c2a5-4a7f-96c1-9f330f0de5cd)

## Result:
This approach demonstrates the integration of a simple mathematical calculation (volume of a cylinder) into a chat-based system. The system can detect queries related to the volume of a cylinder and automatically invoke the function to calculate it. By leveraging an LLM’s function-calling capability, dynamic and natural interactions can be made, including processing more complex queries and extracting numerical values from user input.


