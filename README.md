# [HumanTask.ai](https://humantask.ai/) Example

This is an example of how to use [HumanTask.ai](https://humantask.ai/) to improve the results of OpenAI's GPT-4 and ensure reliable and accurate code generation.

Check out the [HumanTask.ai](https://humantask.ai/) website for more information.

## Without HumanTask.ai

See the result [here](https://chat.openai.com/share/ccd692f9-2719-4946-bd51-3b35e844e5cf) or on the [`main` branch](https://github.com/lucasmrdt/human-task-example).

```python
prompt = "Create a JS `pay(amount: number)`  \
function that opens stripe payment for the   \
provided amount."

outputs = OpenAI().chat.completions.create(
  messages=[{
    "role": "user",
    "content": prompt,
  }],
  model="gpt-4",
)
response = outputs.choices[0].message.content

# Got 3 Errors:
# - ❌ TypeError: Cannot destructure property 'amount' of 'req.body' as it is undefined.
# - ❌ Access to fetch at 'http://localhost:3000/create-checkout-session' from origin 'http://localhost:1234' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
# - ❌ POST http://localhost:3000/create-checkout-session 500 (Internal Server Error) Invalid API Key provided: YOUR_STR**********_KEY
```

## With HumanTask.ai

See the result on the [`humantask` branch](https://github.com/lucasmrdt/human-task-example/tree/humantask).

```python
import humantask

prompt = "Create a JS `pay(amount: number)`  \
function that opens stripe payment for the   \
provided amount."

outputs = OpenAI().chat.completions.create(
  messages=[{
    "role": "user",
    "content": prompt,
  }],
  model="gpt-4",
)
response = outputs.choices[0].message.content

response = humantask.create(
  prompt=prompt,
  proposed_response=response,
)

# Got 0 Errors! 🎉
```
