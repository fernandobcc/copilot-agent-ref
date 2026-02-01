# Research Methodologies Reference

This document provides detailed guidance on research methodologies for different scenarios.

## Source Credibility Assessment

### Academic Sources
**High Credibility:**
- Peer-reviewed journals (Nature, Science, IEEE, ACM, etc.)
- University press publications
- Government research institutions (NIH, NSF, NASA, etc.)
- Systematic reviews and meta-analyses

**Medium Credibility:**
- Conference proceedings (check conference ranking)
- Preprints (arXiv, bioRxiv) - not yet peer-reviewed
- Thesis/dissertations from reputable institutions
- Technical reports from established organizations

**Considerations:**
- Check impact factor and citation count
- Verify author credentials and affiliations
- Look for conflicts of interest declarations
- Note sample size and methodology rigor

### Industry Sources
**High Credibility:**
- Official documentation (APIs, specs, standards bodies)
- Research firms (Gartner, Forrester, McKinsey reports)
- Company engineering blogs (for their own tech)
- Open source project documentation

**Medium Credibility:**
- Trade publications (specific to industry)
- Vendor white papers (check for bias)
- Industry analyst reports
- Technical blog aggregators (HackerNews, dev.to, Medium)

**Considerations:**
- Distinguish marketing from technical content
- Check author expertise and position
- Look for case studies and real-world data
- Verify claims with multiple sources

### News and Media
**High Credibility:**
- Major news organizations (Reuters, AP, Bloomberg for finance)
- Investigative journalism with named sources
- Original reporting vs. aggregation
- Fact-checking organizations (Snopes, FactCheck.org)

**Medium Credibility:**
- Specialized news sites (TechCrunch, ArsTechnica)
- Opinion pieces from subject matter experts
- Aggregators that cite original sources

**Red Flags:**
- Uncited claims
- Anonymous or unreliable sources
- Sensationalist headlines
- No author attribution
- No publication date

## Research Question Types

### Factual Questions
**Goal:** Establish objective facts
**Approach:**
- Start with authoritative sources (official docs, primary sources)
- Cross-verify with 2-3 independent sources
- Check for updates or corrections
- Note any uncertainty or debate

**Example:** "What is the syntax for Python async/await?"
- Check: Official Python docs (primary source)
- Verify: PEP 492 (specification)
- Confirm: Working code example

### Comparative Questions
**Goal:** Evaluate options against criteria
**Approach:**
- Define clear comparison criteria upfront
- Gather data for each option systematically
- Use consistent methodology across options
- Present in table or matrix format
- Note subjective vs. objective differences

**Example:** "Should I use React or Vue?"
- Define criteria: Learning curve, performance, ecosystem, team experience
- Gather: Official benchmarks, community size, job market data
- Compare: Side-by-side on each criterion
- Recommend: Based on user's specific context

### Analytical Questions
**Goal:** Understand causes, effects, or relationships
**Approach:**
- Identify relevant variables and factors
- Look for multiple explanations
- Distinguish correlation from causation
- Check for confounding variables
- Note limitations of available data

**Example:** "Why did product X fail in market Y?"
- Research: Market conditions, competitor actions, product issues
- Analyze: Multiple contributing factors
- Synthesize: Most likely combination of causes
- Caveat: Acknowledge uncertainty

### Predictive Questions
**Goal:** Forecast or estimate future outcomes
**Approach:**
- Base predictions on historical patterns
- Identify trend drivers and dependencies
- Consider multiple scenarios
- Quantify uncertainty ranges
- Note assumptions explicitly

**Example:** "Will AI replace software engineers?"
- Analyze: Historical automation trends, current AI capabilities
- Consider: Multiple timescales and definitions of "replace"
- Synthesize: Nuanced view with probability ranges
- Disclaim: High uncertainty on long-term predictions

## Verification Techniques

### Fact Triangulation
Cross-reference claims using three independent source types:

1. **Primary source**: Original research, official statement, raw data
2. **Expert analysis**: Domain expert interpretation
3. **Independent verification**: Third-party confirmation

**Example - verifying a statistic:**
- Primary: Original study/dataset
- Expert: Academic or industry expert citing it
- Independent: News outlet or fact-checker confirming

### Chain of Attribution
Trace claims back to their origin:

1. Find the earliest source mentioned
2. Read the original in full context
3. Check if later sources accurately represent it
4. Note any "telephone game" distortions
5. Cite the original, not the intermediary

**Red flag:** "Studies show..." without naming the study

### Temporal Verification
Ensure information currency:

1. Check publication/last updated date
2. Verify no major changes since then
3. Look for "as of [date]" qualifiers
4. Search for updates or corrections
5. Note version numbers for tech topics

**Critical for:** Software versions, regulations, statistics, breaking news

### Methodology Review
For research studies and data claims:

1. **Sample size**: Is it large enough?
2. **Selection bias**: How were subjects chosen?
3. **Controls**: Was there a control group?
4. **Reproducibility**: Could this be replicated?
5. **Statistical significance**: Are results meaningful?
6. **Peer review**: Has it been validated?

### Consensus Checking
Determine scientific/expert consensus:

1. Look for systematic reviews or meta-analyses
2. Check multiple expert opinions
3. Note outliers vs. mainstream views
4. Distinguish emerging vs. established science
5. Acknowledge areas of active debate

## Common Research Biases

### Confirmation Bias
**Problem:** Seeking information that confirms existing beliefs
**Mitigation:**
- Actively search for contradicting evidence
- Ask "What would prove me wrong?"
- Present strongest counterarguments
- Consider alternative explanations

### Availability Bias
**Problem:** Overweighting easily recalled information
**Mitigation:**
- Systematically search, don't rely on memory
- Check for representative samples
- Look for base rates and statistics
- Question vivid but rare examples

### Recency Bias
**Problem:** Overweighting recent information
**Mitigation:**
- Check historical context and trends
- Look for long-term patterns
- Don't assume latest = best
- Consider cyclical phenomena

### Authority Bias
**Problem:** Uncritically accepting expert opinions
**Mitigation:**
- Verify even expert claims
- Check for conflicts of interest
- Look for expert disagreement
- Evaluate evidence, not just credentials

### Selection Bias
**Problem:** Non-representative information sources
**Mitigation:**
- Seek diverse source types
- Include dissenting views
- Check for publication bias (negative results unpublished)
- Consider what's not being said

## Specialized Research Workflows

### Technical Implementation Research
1. **Official docs first**: Always start with authoritative documentation
2. **Version check**: Ensure examples match your version
3. **Working example**: Find or create a minimal reproduction
4. **Common issues**: Check GitHub issues, Stack Overflow
5. **Best practices**: Look for production use cases
6. **Alternatives**: Know why this vs. other approaches

### Market Research
1. **Market size**: Total addressable market (TAM), current size, growth rate
2. **Players**: Key companies, market share, positioning
3. **Trends**: Growth drivers, declining segments, emerging tech
4. **Data sources**: Industry reports, company financials, government data
5. **Validation**: Cross-check claims with multiple sources
6. **Recency**: Market data becomes stale quickly

### Historical Research
1. **Primary sources**: Original documents, firsthand accounts
2. **Secondary analysis**: Historian interpretations
3. **Context**: Historical circumstances and norms
4. **Bias awareness**: Whose perspective is recorded?
5. **Corroboration**: Multiple independent sources
6. **Historiography**: How has interpretation evolved?

### Scientific Research
1. **Peer review**: Prefer published, reviewed studies
2. **Replication**: Has it been reproduced?
3. **Sample size**: Adequate statistical power?
4. **Methodology**: Sound experimental design?
5. **Funding**: Check for conflicts of interest
6. **Consensus**: Outlier or mainstream finding?

## Reporting Best Practices

### Executive Summary Structure
- **Lead**: Most important finding first
- **Context**: Why this matters
- **Key findings**: 3-5 bullet points
- **Recommendation**: If requested
- **Caveats**: Major limitations or uncertainties

### Main Body Organization
- **Logical flow**: Questions → Evidence → Analysis
- **Clear headers**: Scannable section titles
- **Evidence first**: Facts before interpretation
- **Citation inline**: Source with each claim
- **Visuals**: Tables for comparisons, lists for steps

### Confidence Indicators
Use explicit confidence levels:

- **High confidence**: Multiple authoritative sources agree, recent data, clear methodology
- **Medium confidence**: Some sources agree, reasonable data, standard methodology
- **Low confidence**: Limited sources, old data, questionable methodology, conflicting claims

### Handling Uncertainty
- **Acknowledge**: "Data is limited on this question"
- **Range estimates**: "Between X and Y" rather than single point
- **Conditional**: "If assumption A holds, then..."
- **Update trigger**: "Would change if new data shows..."

## Quality Checklist

Before finalizing research:

- [ ] All key questions answered or gaps noted
- [ ] Claims supported by credible sources
- [ ] Sources cited with links/references
- [ ] Conflicting information addressed
- [ ] Publication dates included
- [ ] Methodology appropriate for question type
- [ ] Biases considered and mitigated
- [ ] Confidence levels indicated
- [ ] Limitations acknowledged
- [ ] Recommendations justified
- [ ] Actionable next steps provided (if appropriate)

## Example Citation Formats

### Inline citation (preferred for chat):
"According to the official Python documentation (v3.11), async/await was introduced in PEP 492."

### With link:
"Studies show 60% adoption rate ([Source: 2025 Developer Survey](https://example.com), n=10,000)"

### Multiple sources:
"Performance improvements of 2-3x reported by both [TechBlog](https://example.com/1) and [BenchmarkSite](https://example.com/2)"

### With confidence:
"Market size estimated at $50-80B (Medium confidence - based on 3 analyst reports from 2024-2025)"

### Noting disagreement:
"Effectiveness is debated: [Study A](link) found 30% improvement while [Study B](link) found no significant effect"
