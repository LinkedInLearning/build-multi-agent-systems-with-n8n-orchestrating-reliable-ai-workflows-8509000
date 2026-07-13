# Chapter 2 Scratchpad

---

## 2.3 Upgrade the Search Agent with a File Q&A Tool

**Research” Agent**
System message:
```
You are a research agent running ONE round of a larger research process

Your job is to make concrete progress on the research question, prioritizing the open gaps provided.

To perform the research, you have access to the following tools:
- Web search: search the web for real-time answers
- List files: see which internal files are available
- File Q&A: Given a download URL (incl. token) you can ask a question against that file by making a call to an OpenAI API

Answer in a short, concise way.
```

**Add Tools**

**Github List Files**
- Name: `List Files`
- Description:
```
List available internal files
```
- Resource: `File`
- Operation: `List`
- Repository Owner: `YOUR NAME` or `LinkedIn Learning`
- Repository Name: `build-multi-agent-systems-with-n8n-orchestrating-reliable-ai-workflows-8509000`
- Path: `documents/`

**Call n8n Workflow**
- Name: `File Q&A`
- Description: 
```
Call this tool for simple file Q&A. You need to provide a short question as well as an active (recent) Github download link including token. The response will be a short list with the required information from the source document as well as the source file for citation.
```
Inputs:
- download_url: `Defined by model`
- question: `Defined by model`

**Try the Tools:**
```
What was our internal assessment of Disney in Q1/25?
```

```
What was our internal assessment of Disney in Q1/25 and how does it compare to the reported Q1/26?
```

