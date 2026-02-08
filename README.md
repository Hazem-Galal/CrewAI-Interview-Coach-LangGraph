# 🎯 AI Interview Coach with LangGraph

A comprehensive interview preparation system built on **LangGraph** that simulates realistic end-to-end interview loops for specific roles and companies. The system uses multi-agent workflow orchestration to research companies, analyze interviewers, generate targeted questions, and provide real-time coaching feedback.

## 🌟 Features

### Multi-Agent Workflow
- **research_company**: Searches for company info, tech stack, culture, and recent news
- **research_interviewer**: Analyzes interviewer background and builds persona hypotheses
- **generate_questions**: Creates 10-15 role-specific, seniority-calibrated questions
- **interviewer_bot**: Conducts the interview with intelligent follow-ups and scoring
- **get_response**: Captures answers with loop control and meta-coaching support

### Intelligent Feedback System
- **0-5 scoring** with experienced interviewer insights
- **STAR-formatted rewrites** showing optimal answer structure
- **Coverage tracking** across 5 dimensions: problem-solving, collaboration, ambiguity handling, leadership/ownership, technical depth
- **Coach mode**: Toggle for metacognitive feedback on answer structuring

### Adaptive Targeting
- **Seniority calibration**: Questions adapt for junior/mid/senior/lead levels
- **Interview type support**: Behavioral, system design, coding, or mixed
- **Company-specific**: Questions tied to actual tech stack and domain
- **Interviewer persona**: Adapts to interviewer's likely concerns and background

### Session Management
- **In-memory state** with LangGraph checkpointing
- **Export/import** session data as JSON
- **Final report generation**: Strengths, risk areas, story refinements, 3-session practice plan

## 🚀 Quick Start

### 1. Open in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Hazem-Galal/CrewAI-Interview-Coach-LangGraph/blob/main/interview_coach.ipynb)

### 2. Run Setup Cells

Execute the first few cells to install dependencies:
```python
!pip install -q langgraph langchain langchain-openai langchain-anthropic tavily-python google-search-results
```

### 3. Configure API Keys

You'll need at least one LLM provider and one search API:

**LLM Providers** (choose one or both):
- [OpenAI API Key](https://platform.openai.com/api-keys) - for GPT-4
- [Anthropic API Key](https://console.anthropic.com/) - for Claude 3.5 Sonnet

**Search APIs** (optional, choose one or both):
- [Tavily API Key](https://tavily.com/) - AI-optimized search (recommended)
- [SERP API Key](https://serpapi.com/) - Google search fallback

### 4. Start Your Interview

Run Section 13 cells and provide:
- **Company name**: e.g., "Google", "Amazon", "Stripe"
- **Role title**: e.g., "Senior Software Engineer"
- **Seniority level**: Junior / Mid / Senior / Lead
- **Interview type**: Behavioral / System Design / Coding / Mixed
- **Optional**: Interviewer name, job description, your background

### 5. Practice!

Answer questions as they appear. Tips:
- Use **STAR format** (Situation, Task, Action, Result)
- Type `stop`, `end`, or `finish` to conclude early
- Type `how could I improve this?` to activate **coach mode**
- Review scores and rewrites to learn optimal structuring

## 📊 Workflow Architecture

```
START
  ↓
research_company (search + LLM synthesis)
  ↓
research_interviewer (persona building)
  ↓
generate_questions (10-15 targeted questions)
  ↓
interviewer_bot (ask question + score previous answer)
  ↓
  ├─→ stop_requested? → END (final report)
  └─→ get_response (capture answer) → [loop back to interviewer_bot]
```

### State Schema

```python
InterviewState:
  # Configuration
  - company_name, role_title, seniority_level, interview_type
  - job_description, interviewer_name, candidate_background
  
  # Research outputs
  - company_summary, talking_points
  - interviewer_persona, interviewer_hypotheses
  
  # Interview session
  - questions (list of generated questions)
  - conversation_history (Q/A pairs with scores)
  - current_question_index, stop_requested
  - coach_mode_active
  
  # Progress tracking
  - coverage_tracker (5 dimension scores)
  - final_report
```

## 🎓 Usage Examples

### Example 1: Behavioral Interview at Google
```python
COMPANY_NAME = "Google"
ROLE_TITLE = "Senior Software Engineer"
SENIORITY_LEVEL = "senior"
INTERVIEW_TYPE = "behavioral"
```

**Generated questions will emphasize:**
- System design trade-offs
- Cross-functional collaboration at scale
- Leadership and mentorship examples
- Google-specific challenges (distributed systems, scale, etc.)

### Example 2: Junior Coding Interview at Startup
```python
COMPANY_NAME = "Vercel"
ROLE_TITLE = "Frontend Engineer"
SENIORITY_LEVEL = "junior"
INTERVIEW_TYPE = "coding"
```

**Generated questions will focus on:**
- React/Next.js fundamentals
- Learning agility and growth mindset
- Collaboration and code review skills
- Web performance basics

### Example 3: Mixed Interview with Known Interviewer
```python
COMPANY_NAME = "Anthropic"
ROLE_TITLE = "ML Research Engineer"
INTERVIEWER_NAME = "Chris Olah"  # hypothetical
SENIORITY_LEVEL = "senior"
INTERVIEW_TYPE = "mixed"
```

**System will:**
- Research interviewer's publications and interests
- Generate questions aligned with their focus areas
- Adapt technical depth to their likely concerns

## 🔧 Customization

### Switch LLM Provider

In Section 2, modify:
```python
LLM_PROVIDER = "openai"  # or "anthropic"
MODEL_NAME = "gpt-4-turbo"  # or "claude-3-5-sonnet-20241022"
```

### Adjust Question Count

In `generate_questions_node` (Section 7), change the prompt:
```python
"Generate 15-20 interview questions..."  # instead of 10-15
```

### Modify Seniority Calibration

In Section 7, edit `seniority_guide` dict:
```python
seniority_guide = {
    "junior": "Your custom guidance...",
    "mid": "...",
    # etc.
}
```

### Change Coverage Dimensions

In Section 3, modify `coverage_tracker`:
```python
"coverage_tracker": {
    "problem_solving": 0.0,
    "communication": 0.0,  # add new dimension
    # ...
}
```

## 📈 Session Export

After completing an interview, export your session:

```python
export_session(final_state)
# Downloads: interview_session_20260208_143022.json
```

To reload later:
```python
restored_state = import_session("interview_session_20260208_143022.json")
```

## 🏗️ Architecture Decisions

### Why Single Notebook?
- **Zero deployment friction** in Colab
- **No file upload required** - just open and run
- **Self-contained** - all logic in one place
- Trade-off: Requires clear section organization (achieved via markdown headers)

### Why Both LLM Providers?
- **Redundancy** if one API is down
- **User choice** based on preferences (creative vs analytical)
- **Cost flexibility** (different pricing models)

### Why Tavily + SERP Fallback?
- **Tavily** is AI-optimized for better context extraction
- **SERP** is established and reliable
- **Graceful degradation** pattern ensures research always works

### Why JSON Export Over Drive Persistence?
- **Simpler** - no OAuth flow required
- **User control** - export only when needed
- **Portable** - works outside Colab too
- Trade-off: No automatic session recovery on runtime restart

## 🎯 Best Practices

### For Candidates
1. **Prepare stories in advance** using STAR format
2. **Use coach mode liberally** to learn structure patterns
3. **Practice multiple times** with different companies/roles
4. **Track progress** across sessions using exports
5. **Focus on coverage gaps** shown in final report

### For Customization
1. **Start with defaults** to understand the system
2. **Modify prompts gradually** - test after each change
3. **Use temperature wisely**: 0.3-0.5 for research, 0.7-0.9 for questions
4. **Add logging** if debugging node behavior
5. **Checkpoint frequently** when making major changes

## 🔒 Privacy & Security

- **API keys** are captured via `getpass` (hidden input)
- **No data persistence** beyond current session (unless exported)
- **No external logging** - all processing is local to your Colab runtime
- **Search results** are ephemeral and not stored
- **Exported JSONs** may contain interview responses - store securely

## 🐛 Troubleshooting

### "No module named 'langgraph'"
**Solution**: Restart runtime and re-run installation cell

### "API key not found"
**Solution**: Re-run Section 2 configuration cell with valid keys

### "Tavily search failed"
**Solution**: System auto-falls back to SERP - this is normal if Tavily key is missing

### Questions seem generic
**Solution**: 
- Provide job description in initial setup
- Add candidate background context
- Verify company name is spelled correctly for better search results

### Score always shows 3/5
**Solution**: LLM may be returning non-standard format - check `interviewer_bot_node` parsing logic

### Export not downloading
**Solution**: 
- Ensure running in Colab (not local Jupyter)
- Check browser's download settings
- File still saves locally - can copy manually from file browser

## 📚 References

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangChain Python](https://python.langchain.com/)
- [Tavily API](https://docs.tavily.com/)
- [STAR Interview Method](https://www.indeed.com/career-advice/interviewing/how-to-use-the-star-interview-response-technique)

## 🤝 Contributing

This is a teaching/demonstration project. Suggestions for improvements:

1. **Add visualization**: Chart coverage progress over time
2. **Multi-turn deep dives**: Interviewer can probe specific topics for 3-4 questions
3. **Industry templates**: Pre-built question sets for FAANG, startups, consulting, etc.
4. **Voice mode**: Speech-to-text for more realistic practice
5. **Peer comparison**: Anonymous benchmarking against other candidates

## 📄 License

MIT License - Feel free to use, modify, and distribute.

## 🙏 Acknowledgments

Built with:
- **LangGraph** for workflow orchestration
- **LangChain** for LLM abstractions
- **Anthropic Claude** and **OpenAI GPT-4** for intelligence
- **Tavily** for AI-optimized search

---

**Happy interviewing! 🎯**

*Remember: The goal isn't perfection - it's progress. Use this tool to build confidence, refine your stories, and develop strong answer structures. You've got this!*
