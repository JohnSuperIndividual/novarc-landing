# Reddit Post Draft — r/LocalLLaMA

**Title:** I built a DeepSeek API proxy — OpenAI-compatible, 90% cheaper than GPT-4o

---

**Body:**

I've been running inference costs for my side projects for the past year and the bills were getting ridiculous — $200+/month just on OpenAI calls for things that honestly didn't need GPT-4o quality.

So I set up **NovArc API**: a unified OpenAI-compatible gateway routing to DeepSeek V3 and Qwen models. Thought I'd share it since this community probably has the same pain.

**What it is:**
- OpenAI-compatible endpoint (just swap the `base_url`)
- Routes to DeepSeek V3, Qwen-Plus, Qwen-Max, Qwen-Turbo
- Unified billing, usage dashboard, per-key rate limits

**Price comparison (per million tokens):**

| Model | Input | Output |
|-------|-------|--------|
| NovArc (DeepSeek V3) | $0.75 | $1.25 |
| GPT-4o | $5.00 | $15.00 |
| Claude 3.5 Sonnet | $3.00 | $15.00 |

That's roughly **6–12x cheaper** than GPT-4o for most workloads.

**The one-line switch:**

```python
# Before
client = OpenAI(base_url="https://api.openai.com/v1", api_key="sk-...")

# After (that's literally the only change)
client = OpenAI(base_url="https://new-api-production-d6db.up.railway.app/v1", api_key="your-novarc-key")
```

Everything else — streaming, function calling, system prompts, LangChain/LlamaIndex integrations — works without any changes.

**Free tier:** Signing up gives you 5M tokens free (~$3.75 value at PAYG rates), no credit card. Enough to run a meaningful eval on your actual workload.

If you're already using DeepSeek directly, you're probably getting similar prices — but the value here is the management layer: multiple keys, usage tracking per project, automatic failover if one provider goes down.

Paid plans start at $9/mo for 5M tokens/month if you want predictable billing.

API: https://new-api-production-d6db.up.railway.app

Happy to answer questions or take feedback — still early days.

---

*Tags: deepseek, openai-alternative, llm-api, cost-optimization*
