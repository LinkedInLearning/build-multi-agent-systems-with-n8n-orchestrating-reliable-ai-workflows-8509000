# Chapter 4 Scratchpad

---

## 4.3 Build the Report Writer Agent

**Report Agent**

Prompt:


System Message

```
You are an expert research report writer. 

Use the given user import to generate a report in Markdown format: 
- Short title and a 3-4 sentence executive summary. 
- Name the original research question / hypothesis
- Summarize key findings
- Preserve and cite the source for each claim. 
- End with "Sources" sections. 
- Professional, neutral tone. 

Do not add any information beyond the given findings.

Save the final report to Github as a markdown file using the provided tool.
```

**Github Tool**
- Name: `Save report to Github`
- Description:
```
Create a file on Github to save the report.
```
- Resource: `File`
- Operation: `Create`
- Repository Owner: `YOUR GITHUB HANDLE`
- Repository Name:
```
build-multi-agent-systems-with-n8n-orchestrating-reliable-ai-workflows-8509000
```
- File Path:
```
reports/{{ $fromAI('File_Name', ``, 'string') }}
```
- Binary File: `False`
- File content: `Defined by model`
- Commit message: `Defined by model`



