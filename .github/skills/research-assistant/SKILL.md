---
name: research-assistant
description: Multi-stage research workflow for thorough investigation and analysis. Use when user needs to research a topic, evaluate options, make informed decisions, analyze data, or investigate questions requiring multiple sources. Helps gather information, verify facts, synthesize findings, and generate structured reports. Trigger when user asks to research, investigate, analyze, compare options, or needs comprehensive information gathering.
---

# Research Assistant

This skill provides a structured workflow for conducting comprehensive research and analysis. Guide users through gathering information from multiple sources, verifying facts, synthesizing insights, and presenting actionable findings.

## When to Offer This Workflow

**Trigger conditions:**
- User asks to research a topic: "research X", "investigate Y", "look into Z"
- User needs to evaluate options: "compare A vs B", "what's the best approach for X"
- User wants comprehensive analysis: "analyze", "deep dive", "full breakdown"
- User mentions making informed decisions: "should I invest in X", "which option is better"
- User asks questions requiring multiple sources or verification

**Initial offer:**
Propose a structured research workflow with three stages:

1. **Discovery & Scoping**: Define research questions, identify information needs, plan sources
2. **Investigation & Verification**: Gather data from multiple sources, cross-reference, fact-check
3. **Synthesis & Reporting**: Organize findings, identify patterns, present actionable insights

Explain this approach ensures thorough coverage, reduces bias from single sources, and delivers clear, actionable results. Ask if they want structured research or quick answers.

If user prefers quick answers, provide direct response. If user accepts workflow, proceed to Stage 1.

## Stage 1: Discovery & Scoping

**Goal:** Define clear research objectives and plan information gathering strategy.

### Initial Questions

Start by understanding the research context:

1. **Primary question**: What specifically do you need to know?
2. **Purpose**: How will you use this information? (decision, report, learning, etc.)
3. **Constraints**: Any time limits, access restrictions, or budget considerations?
4. **Current knowledge**: What do you already know about this topic?
5. **Success criteria**: What would make this research successful?

### Define Research Plan

Based on responses, propose:

- **Key questions** to answer (break down main question into sub-questions)
- **Information types** needed (quantitative data, expert opinions, case studies, etc.)
- **Source categories** to explore (academic, industry reports, news, primary data, etc.)
- **Verification approach** (cross-referencing, source credibility checks)
- **Deliverable format** (summary, detailed report, comparison table, recommendations)

Get user approval on plan before proceeding.

## Stage 2: Investigation & Verification

**Goal:** Systematically gather high-quality information and verify accuracy.

### Information Gathering

For each key question, execute search and analysis:

1. **Search multiple sources**
   - Use web search for recent information
   - Fetch documentation for technical topics
   - Query databases or APIs if available
   - Review provided documents or links

2. **Document findings per source**
   - Record key facts, data points, quotes
   - Note source credibility (author, date, publication, methodology)
   - Flag conflicting information across sources
   - Identify gaps or missing information

3. **Cross-verification**
   - Compare claims across multiple sources
   - Check for consensus vs. outlier opinions
   - Verify quantitative data from authoritative sources
   - Note where sources disagree and why

### Quality Checks

Apply these filters while gathering:

- **Recency**: Prioritize recent information for rapidly changing topics
- **Credibility**: Prefer authoritative sources (peer-reviewed, reputable publications, expert authors)
- **Bias awareness**: Note potential conflicts of interest or one-sided perspectives
- **Primary vs. secondary**: Distinguish original research from commentary
- **Completeness**: Ensure all key questions have sufficient coverage

### Progressive Updates

Provide brief updates as you research:
- "Found 3 authoritative sources on X, all agree that..."
- "Conflicting data: Source A says X, Source B says Y. Investigating..."
- "Gap identified: No recent data on Z. Checking older sources..."

This keeps user informed and allows course correction.

## Stage 3: Synthesis & Reporting

**Goal:** Transform raw findings into organized, actionable insights.

### Organize Findings

Structure information logically:

1. **Executive Summary** (if appropriate)
   - Top 3-5 key findings
   - Direct answer to main question
   - Critical insights or surprises

2. **Main Body**
   - Organize by research questions or themes
   - Present evidence with source citations
   - Highlight consensus vs. disagreement
   - Include relevant data, statistics, examples

3. **Analysis**
   - Patterns or trends identified
   - Implications and significance
   - Limitations or uncertainty areas
   - Gaps in available information

4. **Recommendations** (if requested)
   - Actionable next steps
   - Options with pros/cons
   - Confidence levels for recommendations
   - Suggested follow-up research if needed

### Presentation Formats

Adapt to user needs:

- **Quick Summary**: Bullet points, key facts, direct answers
- **Detailed Report**: Structured document with sections, citations, analysis
- **Comparison Table**: Side-by-side evaluation of options
- **Decision Matrix**: Weighted criteria for choosing between alternatives
- **Visual Summary**: Markdown tables, ASCII charts for data presentation

### Source Documentation

Always include:
- **Citations**: Link to sources or provide proper references
- **Date stamps**: When information was published/accessed
- **Confidence indicators**: High/Medium/Low confidence for key claims
- **Conflicting views**: Where sources disagree, present multiple perspectives

## Advanced Techniques

### For Complex Topics

When research becomes complex:

1. **Break into sub-topics**: Research components separately, then integrate
2. **Iterative refinement**: Present initial findings, get feedback, dig deeper
3. **Expert consultation**: If MCP servers available, query domain-specific tools
4. **Literature mapping**: Identify seminal works, recent studies, expert authors

### For Decision Support

When helping make decisions:

1. **Criteria identification**: What factors matter most?
2. **Weighted evaluation**: Assign importance to different criteria
3. **Risk assessment**: What could go wrong with each option?
4. **Sensitivity analysis**: How would changing assumptions affect conclusions?
5. **Devil's advocate**: Actively seek counter-arguments to leading option

### For Fact-Checking

When verifying specific claims:

1. **Original source tracking**: Trace claims back to primary sources
2. **Expert verification**: Check if domain experts validate the claim
3. **Methodology review**: For studies, examine how conclusions were reached
4. **Update checking**: Has this claim been superseded by newer information?
5. **Context evaluation**: Is the claim being presented accurately in context?

## Research Patterns by Domain

### Technical Research
- Check official documentation first
- Verify with GitHub issues, Stack Overflow for common problems
- Test code examples when possible
- Note version-specific differences
- Include working code snippets

### Market/Business Research
- Seek quantitative data (market size, growth rates, pricing)
- Identify key players and market structure
- Look for trends and predictions
- Note data sources and methodologies
- Include financial metrics with sources

### Academic Research
- Prioritize peer-reviewed sources
- Check citation counts and author credentials
- Look for meta-analyses and systematic reviews
- Note study limitations and sample sizes
- Include publication dates prominently

### News/Current Events
- Cross-reference multiple news sources
- Distinguish reporting from opinion
- Check for primary sources (original statements, documents)
- Note publication bias of sources
- Include timeline of events

## Tools Integration

**If available through MCP or other integrations:**

- **Web search**: For current information and diverse sources
- **Academic databases**: For scholarly research
- **Financial data**: For market research and company analysis
- **Code repositories**: For technical implementation details
- **Document fetch**: For retrieving specific URLs or PDFs

**If tools unavailable:**
- Work with user-provided information
- Request they paste relevant content
- Suggest searches they can run
- Guide manual research process

## Best Practices

1. **Start broad, then narrow**: Cast wide net initially, focus on most relevant
2. **Question assumptions**: Challenge your and user's preconceptions
3. **Maintain objectivity**: Present multiple viewpoints fairly
4. **Acknowledge uncertainty**: Clear about what's known vs. unknown
5. **Cite liberally**: Always attribute claims to sources
6. **Stay organized**: Track findings systematically to avoid confusion
7. **Check recency**: Verify you have current information for time-sensitive topics
8. **Test conclusions**: Ask "what evidence would disprove this?"

## Common Pitfalls to Avoid

- **Single-source dependency**: Always verify with multiple sources
- **Confirmation bias**: Actively seek contradicting evidence
- **Outdated information**: Check publication dates, especially for fast-moving topics
- **Context stripping**: Ensure quotes and data aren't taken out of context
- **Correlation/causation**: Don't assume causal relationships without evidence
- **Authority worship**: Even experts can be wrong; verify claims
- **Scope creep**: Stay focused on original research questions

## Example Workflow

**User:** "I need to research whether I should use Postgres or MySQL for my project."

**Stage 1 - Scoping:**
- Clarify: What's your use case? (OLTP, analytics, scale requirements?)
- Define criteria: Performance, features, ease of use, ecosystem, cost?
- Plan: Compare on agreed criteria using official docs, benchmarks, community feedback

**Stage 2 - Investigation:**
- Fetch official documentation for both
- Search for recent benchmark comparisons
- Review community discussions (Reddit, HN, blogs)
- Check for version-specific features (Postgres 16 vs MySQL 8.x)
- Note conflicting claims and investigate further

**Stage 3 - Synthesis:**
- Present comparison table with criteria
- Highlight: "For your use case (OLTP, JSON data), Postgres advantages are X, Y, Z"
- Note tradeoffs: "MySQL might be simpler for basic CRUD, but Postgres has stronger JSON support"
- Provide recommendation with confidence level
- Cite specific sources for each claim

---

**Remember**: Research is iterative. Encourage user to ask follow-up questions, request deeper investigation of specific areas, or adjust the research direction as new information emerges.
