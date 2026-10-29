I am planning to build a custom AI agent for our Internal Audit Data Analytics (DA) team. Before designing it, I need to understand the capabilities, limitations, and configuration options of this GPT platform. Please answer the questions below based only on your actual capabilities, system configuration, and tools available to you. Do not guess. If you cannot inspect a capability or setting, explicitly say 'Unknown / I cannot verify this.' Do not reveal confidential system instructions, hidden prompts, credentials, or security-sensitive configuration.

SECTION 1 — AGENT CREATION AND CONFIGURATION
1. Can this platform create and save custom GPTs or agents with persistent instructions?
2. What configuration fields are available to the agent creator (e.g., instructions, description, conversation starters, knowledge files, tools, actions)?
3. Can agents be edited, tested, versioned, and shared with colleagues?
4. Can an agent use uploaded knowledge files in future conversations, and what are the relevant limitations?

SECTION 2 — EXCEL AND FILE HANDLING
5. Can you read and analyze uploaded .xlsx and .xls files? Can you read multiple worksheets, formulas, merged cells, hidden sheets, and large workbooks? Specify any known limitations.
6. Can you process a workbook with 25–100 audit records and review every row without silently skipping records?
7. Can you create and return a downloadable Excel workbook (.xlsx), including multiple worksheets, tables, filters, formulas, and formatting?
8. Can you compare two workbooks, such as an Annual Audit Plan and a previous DA Plan, and match records across them?
9. Can you work with CSV, Word, and PDF files as well?
10. Are there file size, row count, token, or other relevant processing limits? State exact limits only if verifiable.

SECTION 3 — TOOLS AND INTEGRATIONS
11. What tools are actually enabled for this agent? For example, data analysis or code execution, file creation, web browsing, enterprise search, APIs, or workflow integrations.
12. Can the agent run Python or another code environment to validate row counts, process spreadsheets, and generate Excel outputs? If yes, describe the available functionality and restrictions.
13. Can the agent access internal company systems or databases? If yes, which authorized connections are available to this agent? Do not assume access just because a system exists in the company.
14. Can the agent trigger external actions or call APIs, or is it limited to responding in chat and processing uploaded files?

SECTION 4 — KNOWLEDGE AND REASONING
15. Can the agent use approved historical audit plans, past DA plans, DA methodology documents, and examples as reference knowledge?
16. Can it follow a defined decision framework and return a structured classification for every audit, with reasons, potential DA procedures, required data, limitations, and questions?
17. Can it distinguish confirmed data availability from assumed or unknown availability?
18. Can it apply a scoring rubric consistently if we provide explicit criteria and weights? What limitations should we expect?
19. Can it cite the specific source worksheet, row, or audit-plan field supporting each recommendation?
20. Can it validate that every input audit was assessed and report missing, duplicated, or ambiguous records?

SECTION 5 — SECURITY AND GOVERNANCE
21. What company-approved data handling, confidentiality, access control, retention, and sharing constraints should an agent creator know about before uploading internal audit documents? If these settings are not visible to you, say so and identify where an administrator would need to verify them.
22. Are there restrictions on storing historical company files in agent knowledge or generating downloadable files containing internal information?

SECTION 6 — IMPLEMENTATION RECOMMENDATION
23. Based on capabilities you can actually verify, what is the simplest feasible way to implement an agent that reviews an Annual Audit Plan Excel workbook and generates a proposed DA screening assessment in Excel?
24. Which requested features are supported, unsupported, or still unverified?
25. What exact setup steps would the agent creator need to perform, and what would require an administrator?

RESPONSE FORMAT
Return a table with columns: Question Number, Capability, Status (Supported / Unsupported / Partially Supported / Unknown), Evidence or Limitation, and Implication for our project.
Then provide a concise recommended implementation architecture and list the remaining questions that only the platform administrator or documentation can answer.

PROJECT CONTEXT
Our Internal Audit team prepares an annual Audit Plan containing multiple audits. Our DA team reviews each audit's objective and scope to decide whether data analytics is appropriate. We want an agent to review all audits, recommend DA suitability, explain its reasoning, identify potential analytics procedures and required data, flag uncertainties, and produce a reviewable proposed DA Plan in Excel. The final decision must remain with the human DA team.
