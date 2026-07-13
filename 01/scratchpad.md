# Chapter 1 Scratchpad

---

## 1.2 Search Agent

query:
```
Did Disney already release their Q2 earnings for 2026?
```
---

Prompt:
```
Research question: {{ $json.query }}
```

System Message:
```
Answer the research question using web search. Respond in a short, concise way.
```

---

## 1.3 Critique Agent

Prompt:
```
Research question:
"""
{{ $('Define Research Query').item.json.query }}
"""

Findings gathered so far:
"""
{{ $json.output }}
"""
```


System Message:
```
You are a critique agent.

Determine whether the research question has been fully answered using only the findings gathered so far.

Return only valid JSON in this exact format:

{
"done": true,
"gaps": "",
"reasoning": ""
}

Rules:
* Set "done" to true only if the findings completely answer the research question.
* Set "done" to false if the answer is incomplete, unclear, unsupported, or missing important information.
* Use "gaps" to briefly describe what is missing or still needs research.
* Use "reasoning" to briefly explain your verdict.
* Do not include markdown, comments, or any text outside the JSON.
```

Response Format: `JSON Schema`
Name: `critique_schema`

```
{
  "type": "object",
  "additionalProperties": false,
  "required": ["done", "gaps", "reasoning"],
  "properties": {
    "done": {
      "type": "boolean",
      "description": "True if the findings completely answer the research question; false otherwise."
    },
    "gaps": {
      "type": "string",
      "description": "Briefly describe what is missing, unclear, unsupported, or still needs research. Use an empty string if there are no gaps."
    },
    "reasoning": {
      "type": "string",
      "description": "Brief explanation of why the answer is complete or incomplete."
    }
  }
}
```

---

## 1.4 Research Loop

**Set Node**

query: 
```
{{ $('Round Start').item.json.query }}
```

round: 
```
{{ $('Round Start').item.json.round + 1 }}
```

findings:
```
Round {{ $('Round Start').item.json.round }} Findings:
==================
{{ $('Research').item.json.output }}

{{ $('Round Start').item.json.findings }}
```

gaps: 
```
{{ $('Parse Verdict').item.json.gaps }}
```

---

**Research agent**

Prompt:
```
Research question: {{ $json.query }}

Previous findings: 
{{ $json.findings}}

Previous gaps:
{{ $json.gaps }}
```

System prompt:
```
You are a research agent running ONE round of a larger research process

Your job is to make concrete progress on the research question, prioritizing the open gaps provided.

To perform the research, you have access to the following tools:
- Web search: search the web for real-time answers
```

---

**Critique agent**

Prompt:
```
Research question:
"""
{{ $('Define Research Query').item.json.query }}
"""

Findings gathered so far
"""
{{ $json.output }}
{{ $('Define Research Query').item.json.findings }}
"""
```




