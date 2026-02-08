# 🚀 Quick Start Guide

## For Google Colab (Recommended)

### 1. Open the Notebook
Click here: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Hazem-Galal/CrewAI-Interview-Coach-LangGraph/blob/main/interview_coach.ipynb)

### 2. Run All Cells
- Go to **Runtime** → **Run all**
- Or press `Ctrl+F9` (Windows/Linux) or `Cmd+F9` (Mac)

### 3. Enter API Keys
When prompted, enter your API keys (at least one LLM provider):

```
🔐 Enter your API keys (input will be hidden)

OpenAI API Key (optional, press Enter to skip): [your-key-here]
Anthropic API Key (optional, press Enter to skip): [your-key-here]
Tavily API Key (optional, press Enter to skip): [your-key-here]
SERP API Key (optional, press Enter to skip): [your-key-here]
```

**Get API Keys:**
- OpenAI: https://platform.openai.com/api-keys
- Anthropic: https://console.anthropic.com/
- Tavily: https://tavily.com/ (free tier available)
- SERP API: https://serpapi.com/ (optional)

### 4. Configure Your Interview

Scroll to **Section 13: Main Execution** and fill in:

```
Company name: Google
Role title: Senior Software Engineer
Interviewer name (optional): [Enter or skip]
Seniority level: 1) Junior  2) Mid  3) Senior  4) Lead
Choose (1-4): 3
Interview type: 1) Behavioral  2) System Design  3) Coding  4) Mixed
Choose (1-4): 4
```

### 5. Start Practicing!

The system will:
1. 🔍 Research the company (15-30 seconds)
2. 👤 Research the interviewer (if provided)
3. ❓ Generate 10-15 targeted questions
4. 🎤 Start asking questionsAnswe each question naturally. After each answer, you'll receive:
- **Score** (0-5) with interviewer insights
- **STAR-formatted rewrite** showing optimal structure

**Special Commands:**
- Type `stop`, `end`, or `finish` to conclude early
- Type `how could I improve this?` for coaching feedback

### 6. Review Your Report

After the interview ends, you'll get a comprehensive report:
- 💪 Strengths
- ⚠️ Risk areas
- 📚 Stories to refine
- 🎯 3-session practice plan

---

## For Local Jupyter (Advanced)

### 1. Clone Repository
```bash
git clone https://github.com/Hazem-Galal/CrewAI-Interview-Coach-LangGraph.git
cd CrewAI-Interview-Coach-LangGraph
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Set Up API Keys
Create a `.env` file:
```env
OPENAI_API_KEY=your-key-here
ANTHROPIC_API_KEY=your-key-here
TAVILY_API_KEY=your-key-here
SERPAPI_API_KEY=your-key-here
```

### 4. Launch Jupyter
```bash
jupyter notebook interview_coach.ipynb
```

### 5. Follow Colab Steps 2-6 Above

---

## πTips for Best Results

### Before Starting
1. **Have 3-5 stories prepared** using STAR format
2. **Review the company** website and recent news
3. **Identify your target seniority** realistically
4. **Set aside 30-45 minutes** for a full session

### During the Interview
1. **Answer naturally** - don't overthink initially
2. **Use coach mode** if you get stuck structuring
3. **Note your scores** - aim for consistent 4-5s
4. **Read the rewrites carefully** - they show optimal patterns

### After the Interview
1. **Export your session** to track progress
2. **Review risk areas** in the final report
3. **Practice identified weak stories** separately
4. **Repeat with different companies/roles**

---

## 🎯 Example Session (5 minutes)

```
🏢 Company: Stripe
💼 Role: Senior Backend Engineer
📊 Seniority: Senior
🎤 Type: Mixed

Questions Generated: 12

Q1: "Tell me about a time you designed a system for high-volume payment 
processing. What trade-offs did you consider?"

Your Answer: [2-3 minutes using STAR]

📊 Score: 4/5 - Strong technical depth, good trade-off analysis
✨ Rewrite: [Optimized version]

Q2: "Describe a situation where you had to debug a complex distributed 
systems issue. How did you approach it?"

[Continue for 8-10 questions or type 'stop']

📝 Final Report Generated
💾 Session exported: interview_session_20260208.json
```

---

## ⚡ Troubleshooting

| Issue | Solution |
|-------|----------|
| "Module not found" | Restart runtime and re-run installation cell |
| API errors | Verify keys are correct, check account credits |
| Questions too generic | Add job description and candidate background |
| Slow research | Normal for first run (30-45 seconds) |
| Export not working | Check Colab browser download permissions |

---

## 📞 Need Help?

1. Check the full [README.md](README.md) for detailed documentation
2. Review the troubleshooting section
3. Open an issue on GitHub
4. Verify all dependencies are installed correctly

---

**Ready to ace your next interview? Let's go! 🚀**
