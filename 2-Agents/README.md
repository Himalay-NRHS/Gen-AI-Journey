# ChatML and Prompt Structures Across LLMs

## 1. Why prompt structure exists (first principles)

A language model only understands a single stream of tokens.

But conversations have:
- different speakers
- rules vs questions
- tool outputs vs natural language

So every serious LLM uses an internal protocol to encode:
- who is speaking
- what priority the text has
- where messages begin and end

This protocol is called a **prompt structure**.

---

## 2. ChatML (OpenAI)

### What ChatML is
ChatML is OpenAI’s internal conversation markup used to encode chat messages for the model.

The model is trained directly on this format.

---

### Core idea
Each message is wrapped with a role token.

Conceptually:
```
<|role|>
message content
```

Roles define priority and behavior.

---

### Main roles in ChatML

| Role | Purpose | Priority |
|----|----|----|
| system | Rules, identity, behavior | Highest |
| developer | App-level constraints | High |
| user | Human input | Medium |
| assistant | Model output | Generates |
| tool | Tool/function output | Special |

---

### Example ChatML
```
<|system|>
You are a helpful assistant.
<|user|>
Explain ChatML.
<|assistant|>
ChatML is ...
```

Rules:
- system must be obeyed
- user is responded to
- assistant is continued

---

### JSON vs ChatML

You send:
```json
{ "role": "user", "content": "Hello" }
```

Internally converted to:
```
<|user|>
Hello
```

JSON is for APIs.  
ChatML is for models.

---

### Why ChatML matters
It explains:
- system prompt dominance
- prompt injection
- jailbreaks
- tool calling
- chat vs completion models

---

## 3. Anthropic (Claude)

Uses explicit speaker labels.

```
Human: Explain recursion
Assistant: Recursion is ...
```

Characteristics:
- human-readable markers
- constitutional rules baked into training
- weaker exposed system control

---

## 4. Google Gemini / PaLM

Uses role-based structured input.

Example:
```json
{
  "contents": [
    { "role": "user", "parts": ["Hello"] }
  ]
}
```

Characteristics:
- multimodal-first
- strong tool integration
- role separation similar to ChatML

---

## 5. Open-source models (LLaMA, Mistral, etc.)

Use instruction templates.

Examples:
```
### Instruction:
Explain trees

### Response:
```

or

```
<s>[INST] Explain trees [/INST]
Trees are ...
</s>
```

Limitations:
- no true system role
- instructions are just text
- easier to override or inject

---

## 6. Comparison table

| Model family | Structure | System priority |
|---|---|---|
| OpenAI | ChatML tokens | Very strong |
| Anthropic | Human/Assistant labels | Medium |
| Google | Role-based JSON | Strong |
| Open-source | Text templates | Weak |

---

## 7. Why prompt injection works

Prompt injection occurs when user input:
- imitates system instructions
- breaks role boundaries

ChatML reduces this by:
- non-user-typeable tokens
- enforced role hierarchy during training

Not perfect, but safer than plain text.

---



---

## 9. Final takeaway

- ChatML is OpenAI’s conversation protocol
- You never write it directly
- All chat behavior depends on it
- Different models use different control hierarchies
- Understanding this removes guesswork

