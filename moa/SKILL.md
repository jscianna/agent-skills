---
name: moa
description: Mixture of Agents - Run a query through 3 frontier LLMs in parallel, then synthesize the best answer. Use for complex analysis, due diligence, brainstorming, or when you need multiple perspectives. Cost ~$0.03/query.
---

# Mixture of Agents (MoA)

Make 3 AI models argue. Get an answer better than any single model.

## When to Use

- Complex analysis requiring multiple perspectives
- Due diligence, market research, technical evaluation
- Brainstorming and idea synthesis
- High-stakes decisions where one model's blind spots matter

**Don't use for:** Quick Q&A, real-time chat, simple lookups (overkill, 30-90s latency).

## Usage

```bash
# Requires OPENROUTER_API_KEY in environment
node scripts/moa.js "Your complex question"

# Free tier (rate-limited, use for testing only)
node scripts/moa.js "Your question" --free
```

## How It Works

```
     PROMPT
        │
   ┌────┼────┐
   ▼    ▼    ▼
[Kimi][GLM5][MiniMax]  ← 3 models respond in parallel
   │    │    │
   └────┼────┘
        ▼
   AGGREGATOR (Kimi)
   • Picks best insights
   • Resolves conflicts
   • Synthesizes answer
        │
        ▼
   FINAL ANSWER
```

## Models

| Role | Model | Why |
|------|-------|-----|
| Proposer 1 | moonshotai/kimi-k2.5 | Long context, strong reasoning |
| Proposer 2 | z-ai/glm-5 | Technical depth, different training |
| Proposer 3 | minimax/minimax-m2.5 | Nuance, thorough analysis |
| Aggregator | moonshotai/kimi-k2.5 | Fast synthesis |

## Tips

- Be specific — vague prompts get vague synthesis
- Ask for structure ("pros/cons", "top 5") to help the aggregator
- Expect 30-90s latency
