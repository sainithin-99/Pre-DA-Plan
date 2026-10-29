
# AllianzGPT Platform Assessment for Internal Audit DA Agent

## Project Context

Our Internal Audit team prepares an annual Audit Plan containing multiple audits. Our DA team reviews each audit's objective and scope to decide whether data analytics is appropriate. We want an agent to review all audits, recommend DA suitability, explain its reasoning, identify potential analytics procedures and required data, flag uncertainties, and produce a reviewable proposed DA Plan in Excel. The final decision must remain with the human DA team.

---

## Section 1 — Agent Creation and Configuration

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 1 | Custom agents with persistent instructions | **Supported** | Navigate to **Chat agents → Create agent**. Agents persist with configured persona instructions, reference docs, and linked Spaces. | You can create a dedicated "DA Screening Agent" with permanent instructions encoding your methodology. |
| 2 | Configuration fields available | **Supported** | Available fields: **Persona instructions** (high-level guidance, AI-enhanced); **Reference documents** (up to 10 files, 50 MB total, 100K character limit after extraction; formats: .pdf, .txt, .html, .md, .csv, .doc, .docx); **Spaces** (dynamic knowledge repos with up to 100 files each); **Action connectors** (external integrations); agent description; conversation starters. | Upload your DA methodology, scoring rubric, and example plans as reference documents. Use Spaces for larger/evolving document sets. |
| 3 | Edit, test, version, share | **Partially Supported** | **Editing**: Supported — modify agent config at any time. **Testing**: Supported — chat with your agent directly. **Sharing**: Supported — share with team members. **Versioning**: Unknown / I cannot verify built-in version control. | You can iterate on the agent and share it with DA colleagues. Maintain your own version log externally (e.g., a changelog document). |
| 4 | Knowledge files in future conversations | **Supported** | Reference documents (up to 10 files, 50 MB total, 100K char limit) are persistent across all conversations with that agent. Spaces provide additional dynamic storage (up to 100 files per Space). Conversations themselves are retained for 30 days. | Your DA methodology docs, historical plans, and examples will be available in every new conversation. Keep documents under the character limit; use Spaces for larger collections. |

---

## Section 2 — Excel and File Handling

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 5 | Read/analyze .xlsx and .xls files | **Supported** | Python code execution with **pandas** and **openpyxl** libraries. Can read multiple worksheets, hidden sheets, and merged cells (via openpyxl). Reads calculated *values* (not live formula logic). **Limit**: Excel/CSV files must be under **5 MB** in chat; general file limit is 50 MB / 650K characters. | Your Annual Audit Plan workbook (25–100 records) will be well within limits. Ensure formulas are saved with calculated values before upload. |
| 6 | Process 25–100 rows without skipping | **Supported** | Code execution iterates programmatically through every row using pandas DataFrames. Row counts can be validated before and after processing. | The agent can process every audit record and confirm the count matches. Build a validation check into the agent instructions. |
| 7 | Create downloadable .xlsx output | **Supported** | Document generation supports XLSX output with multiple worksheets, tables, and formatting. openpyxl in the code environment can also create workbooks with formulas, filters, and conditional formatting. | The agent can produce a reviewable DA Screening Assessment workbook. Complex formatting (e.g., Excel Tables with auto-filters, conditional formatting) is achievable via code execution. |
| 8 | Compare two workbooks | **Supported** | Code execution can load two workbooks simultaneously, match records by key fields (e.g., audit ID/name), and flag differences, additions, or removals. | You can upload both the Annual Audit Plan and a previous DA Plan for cross-referencing and carry-forward analysis. |
| 9 | CSV, Word, and PDF support | **Supported** | **CSV**: via pandas. **Word**: reading supported (.docx). **PDF**: via PyPDF2 (text extraction; complex layouts/scanned PDFs may have reduced accuracy). Supported upload formats also include TXT, JSON, YAML, XML, PowerPoint, RTF, HTML, and Outlook messages. | Your DA methodology can be in Word or PDF. For best results with PDFs, use text-based (not scanned) documents. |
| 10 | File size and processing limits | **Partially Supported** | **Verified limits**: Chat uploads — up to 20 files per conversation; 50 MB / 650K chars per file; Excel/CSV under 5 MB; images under 10 MB. Reference docs — up to 10 files, 50 MB total, 100K char limit after text extraction. Space — up to 100 files. **Token/context window limits**: The AI has a finite context window; very large outputs may be truncated. Exact token limits are not user-configurable or verifiable. | Your audit plan workbooks should be well within limits. For very large outputs, break the assessment into sections or worksheets. |

---

## Section 3 — Tools and Integrations

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 11 | Enabled tools for this agent | **Supported** | Currently enabled: **Python code execution** (data analysis, spreadsheet processing); **Document generation** (DOCX, PPTX, XLSX, PDF, images); **Enterprise search** (SharePoint knowledge bases via linked Spaces); **Web search**; **Deep research** (Quick Research for multi-source long-form analysis); **Flows** (workflow automation); **Outlook connector** (email integration). | The core toolset covers your full workflow: read audit plan → analyze → reason → generate Excel output. |
| 12 | Python code execution environment | **Supported** | Full Python environment with libraries: **pandas, numpy, scipy, scikit-learn, xgboost, openpyxl, PyPDF2, pillow**. Can validate row counts, process spreadsheets, perform calculations, and generate Excel outputs. **Restrictions**: No internet access from code environment; files created in code are not directly downloadable (use document generation for downloadable files). | You can write validation logic (e.g., "assert all 47 audits assessed") and complex data transformations. Use code for analysis, then document generation for the final deliverable. |
| 13 | Access to internal company systems/databases | **Partially Supported** | This agent has access to **SharePoint knowledge bases** (Allianz Connect Global Space with 8 knowledge bases, UX Research & Insights, Training Materials) and the **Outlook connector**. **No verified direct database connections** (e.g., SAP, audit management systems) are configured for this agent. Additional connections require admin setup via action connectors. | For your DA agent, internal audit data must be uploaded as files (Excel/PDF/Word) rather than pulled live from audit management systems — unless your admin configures a specific connector. |
| 14 | External actions and API calls | **Partially Supported** | The platform supports action connectors (Salesforce, Jira, ServiceNow, Slack, Asana, etc.) and Outlook. However, **only connectors explicitly configured and authorized by an admin are available**. This agent currently has Outlook. The agent cannot make arbitrary API calls. | If you need the agent to push results to an audit tracking system, that would require a dedicated action connector configured by your admin. For the initial use case, generating a downloadable Excel file is the recommended approach. |

---

## Section 4 — Knowledge and Reasoning

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 15 | Use historical audit/DA plans as reference knowledge | **Supported** | Upload approved documents as **reference documents** (up to 10 files, preserved exactly) or add them to a **Space** (up to 100 files, searchable at runtime). Supported formats include PDF, Word, CSV, TXT, HTML, Markdown. | Upload your DA methodology, past DA plans, and example assessments. Use reference docs for critical frameworks (preserved verbatim) and Spaces for historical plans (searched dynamically). |
| 16 | Follow a decision framework with structured output | **Supported** | The AI can follow detailed instructions provided in persona instructions and reference documents. It can produce structured classifications with reasons, procedures, data requirements, limitations, and questions for each audit. | Encode your decision framework explicitly in the reference documents. The more specific and structured your criteria, the more consistent the output. |
| 17 | Distinguish confirmed vs. assumed data availability | **Partially Supported** | The AI can be instructed to explicitly label assertions as "confirmed" vs. "assumed/unknown." However, it relies on the information provided — it cannot independently verify data availability in your systems. Requires clear instructions and may occasionally conflate certainty levels without careful prompting. | Include explicit instructions like: "If data availability is not stated in the audit plan, mark as 'Unknown — requires DA team verification.'" Test and refine the prompting. |
| 18 | Apply scoring rubric consistently | **Partially Supported** | The AI can apply defined criteria and weights if provided clearly. **Key limitation**: AI reasoning is non-deterministic — the same input may produce slightly different scores across runs. Complex multi-factor rubrics may see more variability. Code execution can enforce deterministic scoring for quantifiable criteria. | For quantifiable criteria, implement scoring via code (deterministic). For qualitative judgment, use the AI with clear rubric definitions but treat scores as recommendations for human review. Run validation tests before deployment. |
| 19 | Cite specific source worksheet, row, or field | **Partially Supported** | **Code execution** can reference exact worksheet names, row numbers, and cell values (fully verifiable). **AI reasoning** citations are less precise — it may paraphrase or approximate locations. | Design the workflow so code execution extracts and tags the source location for each record, and the AI reasoning layer references those tags. This hybrid approach gives precise traceability. |
| 20 | Validate completeness (missing, duplicated, ambiguous records) | **Supported** | Code execution can count input records, detect duplicates (by key field), flag missing required fields, identify ambiguous entries, and confirm all records were assessed. This is fully deterministic and auditable. | Build completeness validation as a mandatory first step in the agent workflow. Output a validation summary (e.g., "47 audits read, 47 assessed, 0 skipped, 2 duplicates flagged"). |

---

## Section 5 — Security and Governance

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 21 | Data handling, confidentiality, access control, retention, and sharing constraints | **Partially Supported / Requires Admin Verification** | **What can be verified**: The platform runs on AWS with enterprise-grade security (HIPAA, FedRAMP, SOC 2, ISO 27001 compliance). Conversations are retained for **30 days**. Spaces respect the platform's permission system — agents only return information the user has access to. Agents can be shared with specific users/groups. **What cannot be verified**: Allianz-specific data classification policies for internal audit documents, DLP rules, geo-residency requirements, approved data categories for upload, or audit-trail/logging configurations. These are admin-level settings. | Before uploading internal audit documents, verify with your **platform administrator and CISO/DPO**: (1) Whether internal audit data is approved for this platform; (2) Data residency (which AWS Region your instance uses); (3) Retention policies beyond the 30-day conversation default; (4) Who can access Spaces/agents containing audit data; (5) Logging and audit trail requirements. |
| 22 | Restrictions on storing files in agent knowledge or generating downloadable files | **Unknown / Requires Admin Verification** | The platform technically allows storing files in reference documents and Spaces, and generating downloadable XLSX/DOCX/PDF files. However, **Allianz-internal policies** on storing classified internal audit data or generating downloadable files with internal information are not visible to the agent. | Confirm with your admin whether internal audit plan data can be: (1) stored in agent reference documents/Spaces; (2) generated as downloadable Excel files. There may be data classification restrictions (e.g., "Internal" vs. "Confidential" vs. "Strictly Confidential") that apply. |

---

## Section 6 — Implementation Recommendation

| Q# | Capability | Status | Evidence / Limitation | Implication for Project |
|----|-----------|--------|----------------------|------------------------|
| 23 | Simplest feasible implementation | **Supported** | See detailed architecture below. The recommended approach uses: a custom agent with reference docs (methodology + rubric) → user uploads Audit Plan Excel in chat → code execution reads and validates all records → AI applies framework per audit → document generation produces DA Screening Assessment .xlsx. | A working prototype can be built with no admin involvement (beyond confirming data handling approval). Estimated setup: 1–2 days for agent configuration and testing. |
| 24 | Feature support summary | **See tables above** | 15 capabilities Supported; 8 Partially Supported; 2 Unknown/Require Admin verification. No capabilities are fully Unsupported. | The core workflow is feasible. Partial-support items (scoring consistency, citation precision, security governance) require design mitigations. |
| 25 | Setup steps: agent creator vs. administrator | **Partially Supported** | See detailed steps below. Most setup is self-service for an Author-level user. Admin involvement needed for: security/compliance approval, any additional action connectors, and subscription tier confirmation. | Confirm your subscription tier (Author on Professional or Enterprise required for full capabilities). Get admin approval for data handling before uploading audit documents. |

---

## Recommended Implementation Architecture

### Step 1 — Prepare Your Knowledge Assets

- Write a clear **DA Screening Methodology** document (.md or .docx) defining: decision criteria, scoring rubric, classification labels (e.g., High/Medium/Low DA suitability), required output fields, and uncertainty-handling rules
- Prepare **1–2 example DA assessments** showing the expected input → output transformation
- Optionally gather **historical DA plans** for reference

### Step 2 — Create the Custom Agent *(Agent Creator — Author role)*

- Navigate to **Chat agents → Create agent**
- **Persona instructions**: Define the agent's role ("You are an Internal Audit DA Screening Assistant..."), output format expectations, and behavioral rules (e.g., "Never skip a record," "Flag uncertainty explicitly")
- **Reference documents** (up to 10 files): Upload your DA methodology, scoring rubric, and example assessments
- **Space** (optional): Create a Space with historical DA plans and audit reference materials for dynamic retrieval

### Step 3 — Design the Conversation Workflow

1. The user uploads the **Annual Audit Plan (.xlsx)** in chat
2. The agent uses **code execution** to: read all worksheets, validate record count, flag duplicates/missing fields
3. The agent applies the **DA screening framework** to each audit using AI reasoning grounded in the reference methodology
4. The agent uses **code execution** to compile results into a structured DataFrame with all required columns
5. The agent uses **document generation** to produce the final **DA Screening Assessment (.xlsx)** for download

### Step 4 — Test and Iterate

- Test with a sample audit plan (5–10 audits) and verify every row is assessed
- Validate scoring consistency by running the same input 3–5 times
- Refine persona instructions and methodology document based on results

---

## Steps Requiring Administrator Involvement

| Step | Responsibility | Action |
|------|---------------|--------|
| 1 | **Admin / CISO / DPO** | Approve upload of internal audit data to the platform; confirm data classification compliance |
| 2 | **Admin** | Confirm subscription tier supports agent creation (Author on Professional or Enterprise) |
| 3 | **Admin** | Confirm the AWS Region and data residency meet Allianz requirements |
| 4 | **Admin** (if needed) | Configure additional action connectors (e.g., to audit management systems) |
| 5 | **Agent Creator** | All other setup (agent creation, reference docs, Spaces, testing, sharing) |

---

## Remaining Questions for Platform Administrator

These items could not be verified from within the agent and require administrator or compliance confirmation:

1. **Data classification approval** — Is internal audit plan data approved for upload to this platform?
2. **Data residency** — Which AWS Region hosts this instance, and does it meet Allianz geo-residency requirements?
3. **Retention and logging** — What audit trail/logging exists for agent interactions and file uploads beyond the 30-day conversation retention?
4. **Agent versioning** — Is there built-in version control for agent configurations, or should the team maintain this externally?
5. **Downloadable file governance** — Are there DLP controls on files generated and downloaded from the platform?
6. **Subscription tier** — Confirm your team has Author-level access on Professional or Enterprise plan
7. **Database connectors** — If live integration with audit management systems is needed in the future, which action connectors are available or can be configured?

---

## Useful Links

- **Employee Self-Service Tool**: https://aztech.service-now.com/employeeportal
- **AllianzGPT FAQ**: https://allianzms.sharepoint.com/sites/DE1214-connect-az-technology-data-analytics/SitePages/Frequently-Asked-Questions-(FAQs).aspx
- **AllianzGPT ServiceNow Knowledge Base**: https://aztech.service-now.com/nav_to.do?uri=%2Fkb_view.do%3Fsys_kb_id%3D2dd0f6d22bf8cf504180ff84c191bf8c
- **Incident F-Group**: A.TEC.DE.IT.GPT

> **Note**: Feature availability depends on your plan.
