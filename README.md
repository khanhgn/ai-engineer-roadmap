# The AI Engineer Roadmap

Ten steps from your first line of Python to shipping AI products people actually use.

AI engineering isn't the same as machine learning engineering. You don't need to train models from scratch. You just need to know how to use them to build real things. This is the path I'd follow, in order, with the best free resources I've found for each step.

Made by [Khanh](#follow). Star it if it's useful. Pass it on to someone starting out.

## How to use this

Work top to bottom. The order matters, each step assumes the one before it. For each step, read the short intro, learn the bullets, then work through the resources. Don't try to master everything. Get functional, build something, come back deeper later. The only step that really counts is the last one: build and ship.

## The roadmap

| # | Step | Tier |
|---|------|------|
| 1 | [Python and Git](#1-python-and-git) | Foundations |
| 2 | [Model inference](#2-model-inference) | Core |
| 3 | [Agents and tool calling](#3-agents-and-tool-calling) | Core |
| 4 | [Structured output and prompting](#4-structured-output-and-prompting) | Core |
| 5 | [Embeddings](#5-embeddings) | Retrieval |
| 6 | [Deployments](#6-deployments) | Production |
| 7 | [Guardrails](#7-guardrails) | Production |
| 8 | [Databases](#8-databases) | Retrieval |
| 9 | [Caching](#9-caching) | Production |
| 10 | [Context management](#10-context-management) | Production |

## 1. Python and Git

Everything else sits on top of these two. Python is the language of AI tooling, Git is how you save and share code without losing your mind.

Learn:
- Python syntax, data structures, functions, the standard library
- Virtual environments and package management (pip, venv, uv)
- Git basics: commit, branch, merge, rebase, remotes, pull requests

Resources:
- [The Python Tutorial](https://docs.python.org/3/tutorial/index.html) (docs). The canonical, always-current official Python walkthrough. The source of truth for syntax and the standard library.
- [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/) (free book). The most-recommended practical beginner-to-intermediate Python resource.
- [Google's Python Class](https://developers.google.com/edu/python) (course). Free course with lectures and exercises, aimed at people who already program. Fast on-ramp.
- [Pro Git (2nd ed.)](https://git-scm.com/book/en/v2) (free book). The definitive Git book. Explains the commands and the internal model behind them.
- [Learn Git Branching](https://learngitbranching.js.org/) (interactive). Visual in-browser sandbox that makes branching, merging and rebasing click.
- [GitHub Git Cheat Sheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf) (cheatsheet). One page of the Git commands you'll actually use.
- [TheAlgorithms/Python](https://github.com/TheAlgorithms/Python) (repo). A huge collection of clean, educational Python. Good for reading idiomatic code.

## 2. Model inference

The core skill. Send a prompt to a model, get a response back through an API. Once you can do this reliably and you understand tokens and streaming, the rest is just composition.

Learn:
- Calling model APIs (Anthropic Claude, OpenAI) from code
- The request and response shape, system prompts, message roles
- Tokens: how they're counted, how they're billed, why they cap your context
- Streaming responses for responsive UIs

Resources:
- [Get started with Claude](https://platform.claude.com/docs/en/get-started) (docs). Your first Messages API call in cURL, Python or TS, with the token usage block shown.
- [Streaming Messages (Claude)](https://platform.claude.com/docs/en/build-with-claude/streaming) (docs). Incremental SSE streaming for text, tool use and thinking, with SDK examples.
- [Token counting (Claude)](https://platform.claude.com/docs/en/build-with-claude/token-counting) (docs). Count input tokens before you send. Essential for cost, rate limits and context.
- [Claude pricing](https://platform.claude.com/docs/en/about-claude/pricing) (reference). Per-model pricing and how tokens are billed. The reference for cost modelling.
- [OpenAI Text generation](https://developers.openai.com/api/docs/guides/text) (docs). The other major provider's take, via the Responses API.
- [anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python) and [openai-python](https://github.com/openai/openai-python) (repos). The official SDKs. Sync/async clients, streaming helpers, typed responses.
- [claude-cookbooks](https://github.com/anthropics/claude-cookbooks) and [openai-cookbook](https://github.com/openai/openai-cookbook) (repos). Runnable, copy-paste inference patterns from both providers.

## 3. Agents and tool calling

A model that can call your functions stops being a chatbot and starts being a system that does things: searches, runs code, hits APIs. Tool calling plus a loop is the foundation of every agent.

Learn:
- Tool calling: schemas, the tool_use to tool_result round trip, tool_choice
- The agent loop: reason, act, observe, repeat
- Agent design patterns: chaining, routing, orchestrator-workers, and when not to use an agent at all
- Agent frameworks and SDKs

Resources:
- [Tool use with Claude](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview) (docs). The canonical reference for client vs server tools, the round trip, and tool_choice. Start here.
- [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview) (docs). Build agents with the same loop, built-in tools and context management that power Claude Code.
- [Build a tool-using agent](https://platform.claude.com/docs/en/agents-and-tools/tool-use/build-a-tool-using-agent) (tutorial). Walkthrough from a single tool call up to a production agent loop.
- [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (article). The reference essay on agent design patterns and the workflow vs agent distinction.
- [OpenAI Function calling guide](https://developers.openai.com/api/docs/guides/function-calling) (docs). The shared mental model across vendors: JSON-schema tools, strict mode, parallel calls.
- [ReAct: Synergizing Reasoning and Acting](https://arxiv.org/abs/2210.03629) (paper). The landmark paper behind the reason-then-act loop. Underneath nearly every agent framework.
- [claude-cookbooks](https://github.com/anthropics/claude-cookbooks) (repo). Runnable notebooks for tool use, tool_choice forcing, and context patterns.
- [LangChain Agents](https://docs.langchain.com/oss/python/langchain/agents) (docs). The most widely used agent framework, with multi-provider examples.

## 4. Structured output and prompting

Real products need data, not prose. Structured output turns a model into a reliable API that returns valid JSON. And prompting is the highest-leverage skill on this list. The gap between a demo and a product is often just the prompt.

Learn:
- Prompt engineering: clarity, examples, XML structure, separating instructions from data
- Output formatting and controlling how the model responds
- Schema-constrained JSON output, and why it beats "please return JSON"
- Validation and retries on structured responses

Resources:
- [Prompting best practices (Claude)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) (docs). Clarity, examples, XML structuring, output formatting, agentic prompting.
- [Anthropic's Interactive Prompt Engineering Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) (course). A free 9-chapter hands-on course in notebooks. The single best place to learn prompting.
- [Prompt Engineering Guide (dair-ai)](https://github.com/dair-ai/Prompt-Engineering-Guide) (guide). A well-respected open guide ([web version](https://www.promptingguide.ai/)) covering prompting, context engineering, RAG and agents.
- [OpenAI Structured outputs](https://developers.openai.com/api/docs/guides/structured-outputs) (docs). The definitive guide to schema-constrained generation with json_schema and Pydantic/Zod helpers.
- [Strict tool use (Claude)](https://platform.claude.com/docs/en/agents-and-tools/tool-use/strict-tool-use) (docs). Guarantee output matches a JSON schema exactly with strict: true.
- [instructor](https://github.com/567-labs/instructor) (repo). The most popular structured-output library. Define a Pydantic model, get validated typed data back with retries.
- [outlines](https://github.com/dottxt-ai/outlines) (repo). Constrained decoding that guarantees valid JSON, regex or grammar at generation time.

## 5. Embeddings

Embeddings turn text into vectors so you can search by meaning instead of keywords. They're the engine behind semantic search, recommendations, and RAG, which is how you give a model knowledge it wasn't trained on.

Learn:
- What embeddings are: mapping semantic similarity to spatial proximity
- Choosing a model (dimensions, cost, multilingual, benchmarks)
- Similarity search and approximate nearest neighbours
- RAG basics: chunk, embed, retrieve, generate

Resources:
- [What are Vector Embeddings (Pinecone)](https://www.pinecone.io/learn/vector-embeddings/) (article). The best plain-language explainer of how embeddings turn similarity into spatial proximity.
- [Vector embeddings (OpenAI)](https://developers.openai.com/api/docs/guides/embeddings) (docs). The canonical API reference: use cases, cosine similarity, dimensions, token limits.
- [Introduction to Embeddings (Cohere)](https://docs.cohere.com/docs/embeddings) (docs). Covers input_type, multilingual and multimodal embeddings, and compression.
- [Sentence Transformers: Semantic Search](https://sbert.net/examples/sentence_transformer/applications/semantic-search/README.html) (docs). The open-source, self-hosted path, with runnable code.
- [Embedding Models: Architecture to Implementation (DeepLearning.AI)](https://www.deeplearning.ai/short-courses/embedding-models-from-architecture-to-implementation/) (free course). Builds a dual-encoder from scratch in about an hour.
- [MTEB Leaderboard](https://huggingface.co/spaces/mteb/leaderboard) (resource). The standard benchmark for picking an embedding model. Check it before you commit.
- [faiss](https://github.com/facebookresearch/faiss) (repo). Meta's industry-standard similarity-search library, scaling to billions of vectors.

## 6. Deployments

Code on your laptop helps no one. Deployment is how your app becomes something people can reach: wrapped in an API, containerised, running in the cloud.

Learn:
- Serving an app as an API (FastAPI)
- Containerisation with Docker
- Deploying to the cloud
- High-throughput model serving (vLLM) when you host models yourself

Resources:
- [FastAPI in Containers (Docker)](https://fastapi.tiangolo.com/deployment/docker/) (docs). The authoritative guide to containerising a FastAPI app. The default way to wrap an LLM app as an API.
- [Docker: Get Started](https://docs.docker.com/get-started/) (free course). Docker's own hands-on onboarding: images, containers, Compose from zero.
- [Docker Python guide](https://docs.docker.com/guides/python/containerize/) (docs). Official walkthrough for containerising a Python app.
- [vLLM Documentation](https://docs.vllm.ai/en/latest/) (docs). The reference for high-throughput serving: PagedAttention, continuous batching, OpenAI-compatible server.
- [vllm-project/vllm](https://github.com/vllm-project/vllm) (repo). The most widely adopted open-source serving engine, 200+ architectures.
- [Serving LLMs with vLLM: a practical guide](https://nebius.com/blog/posts/serving-llms-with-vllm-practical-guide) (tutorial). End to end: standing up a vLLM server from install to serving requests.
- [Deploy FastAPI on Docker for production](https://markaicode.com/tutorial/how-to-deploy-fastapi-on-docker-production/) (article). Production hardening: multi-stage builds, Gunicorn and Uvicorn workers, health checks.

## 7. Guardrails

Once real users hit your app, things go wrong: prompt injection, unsafe output, leaked PII, hallucinations. Guardrails are the validation layer that keeps an AI product safe and trustworthy in production.

Learn:
- Input and output validation
- Content moderation
- Prompt injection, the number one LLM risk, and how to defend against it
- Guardrails frameworks and evaluations

Resources:
- [Guardrails AI](https://guardrailsai.com/docs) (docs). The core Python framework for input/output guards, plus a hub of pre-built validators.
- [NeMo Guardrails](https://docs.nvidia.com/nemo/guardrails/latest/) (docs). NVIDIA's toolkit for programmable rails: content safety, jailbreak detection, topic control, PII.
- [OpenAI Moderation guide](https://developers.openai.com/api/docs/guides/moderation) (docs). The free omni-moderation-latest endpoint across 13 harm categories. The standard baseline filter.
- [OWASP LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) (reference). The authoritative definition of the number one LLM risk, with mitigations and attack scenarios.
- [OWASP Prompt Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html) (guide). A concise, practical defence checklist with code.
- [Safe and Reliable AI via Guardrails (DeepLearning.AI)](https://www.deeplearning.ai/courses/safe-and-reliable-ai-via-guardrails) (free course). Builds guards from scratch on a real chatbot, taught by Guardrails AI's founder.
- [Simon Willison on Prompt Injection](https://simonwillison.net/series/prompt-injection/) (article). Ongoing writing by the person who coined the term. Explains why injection stays unsolved.

## 8. Databases

AI apps still need to store things: user data, documents, and the vectors from step 5. Knowing which database to reach for, relational or vector or both, is what keeps your app fast and your data sane.

Learn:
- SQL fundamentals (still essential, most data is relational)
- Vector databases and how indexing (HNSW) works
- Managed (Pinecone) vs self-hosted (Chroma, Weaviate, pgvector)
- When a vector DB is not the answer

Resources:
- [What is a Vector Database? (Pinecone)](https://www.pinecone.io/learn/vector-database/) (article). The best single primer on embeddings, indexing and similarity search.
- [SQLBolt](https://sqlbolt.com/) (course). Free browser-based lessons from SELECT through joins and subqueries. The fastest way to build SQL muscle memory.
- [PostgreSQL Tutorial](https://www.postgresql.org/docs/current/tutorial.html) (docs). The canonical SQL fundamentals walkthrough, from the source.
- [pgvector](https://github.com/pgvector/pgvector) (repo). Adds vector search to Postgres, so structured data and embeddings live in one place.
- [Chroma](https://docs.trychroma.com/) (docs). Python-first, embeddable open-source vector store. The easiest way to prototype RAG locally.
- [Pinecone](https://docs.pinecone.io/) (docs). The leading fully-managed vector DB. Scale without running infrastructure.
- [Weaviate](https://docs.weaviate.io/weaviate) (docs). Open-source vector DB with built-in vectorisation and hybrid search.
- [Which database when for AI?](https://mkdev.me/posts/which-database-when-for-ai-are-vector-databases-all-you-need) (article). Sharp framing for the vector vs structured vs hybrid decision.

## 9. Caching

LLM calls are slow and cost money. Caching cuts both: reuse repeated context and repeated answers instead of paying for them every time. Often the single biggest lever on latency and cost.

Learn:
- Prompt caching: reusing large static context across calls
- Semantic caching: serving cached answers for similar, not identical, queries
- TTLs, thresholds, cache invalidation
- The cost and latency math

Resources:
- [Prompt caching (Claude)](https://platform.claude.com/docs/en/build-with-claude/prompt-caching) (docs). cache_control breakpoints, TTLs, pricing, best practices. The go-to for Claude caching.
- [Prompt caching (OpenAI)](https://developers.openai.com/api/docs/guides/prompt-caching) (docs). Automatic caching, breakpoints, and structuring prompts to cut latency and cost.
- [Prompt Caching 101 (OpenAI Cookbook)](https://developers.openai.com/cookbook/examples/prompt_caching101) (notebook). Hands-on runnable examples across tools, multi-turn chats and images.
- [Prompt caching notebook (Anthropic Cookbook)](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/prompt_caching.ipynb) (notebook). Official end-to-end example measuring cost and latency gains.
- [What is semantic caching? (Redis)](https://redis.io/blog/what-is-semantic-caching/) (article). Provider-agnostic explainer of the embed, similarity, hit/miss flow and threshold tuning.
- [RedisVL SemanticCache API](https://redis.io/docs/latest/develop/ai/redisvl/api/cache/) (docs). How to stand up a production semantic cache on Redis.
- [GPTCache](https://github.com/zilliztech/GPTCache) (repo). The open-source "memcache for LLMs". A modular semantic cache with LangChain and LlamaIndex integrations.

## 10. Context management

The context window is finite and precious. As conversations and agent runs grow, you have to decide what stays, what gets summarised, and what gets dropped. Managing context well is what separates a toy from an agent that runs for hours.

Learn:
- How the context window works and what counts toward it
- Context engineering: curating the smallest set of high-signal tokens
- Compaction, summarisation, and structured note-taking (agent memory)
- Why models degrade in the middle of long contexts, and how to lay context out

Resources:
- [Context windows (Claude)](https://platform.claude.com/docs/en/build-with-claude/context-windows) (docs). How the window works, what counts toward it, context rot, and server-side compaction.
- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) (article). Anthropic's flagship guide: treat context as a scarce resource. Compaction, memory, progressive disclosure.
- [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) (article). Managing context across many windows with persistent state and incremental progress.
- [Lost in the Middle](https://arxiv.org/abs/2307.03172) (paper). The landmark study showing models retrieve best from the start and end, and degrade in the middle.
- [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) (paper). OS-style paging between in-context and external memory. Foundational for agent memory design.
- [mem0](https://github.com/mem0ai/mem0) (repo). A popular universal memory layer for agents across sessions.

## The last step: build and ship

The roadmap ends where the real learning starts. Pick one idea and build it end to end: inference, a prompt, a tool call, a vector search, a guardrail, deployed behind an API. Ship something people can actually use. Then do it again. That loop is the job.

## Other repos and tutorials I find helpful

Not part of the roadmap, just things I keep going back to.

- [mlabonne/llm-course](https://github.com/mlabonne/llm-course). Probably the best free LLM course out there. Fundamentals, the science side, and the engineering side, with Colab notebooks for everything.
- [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps). A huge pile of runnable LLM app examples: agents, RAG systems, the lot. Great for stealing patterns.
- [chiphuyen/aie-book](https://github.com/chiphuyen/aie-book). The repo behind Chip Huyen's AI Engineering book. The [resources.md](https://github.com/chiphuyen/aie-book/blob/main/resources.md) file alone is worth the visit.
- [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch). If you ever want to actually understand what's under the hood, Sebastian Raschka walks you through building an LLM from scratch in code.
- [Hannibal046/Awesome-LLM](https://github.com/Hannibal046/Awesome-LLM). The classic awesome-list for LLMs. Milestone papers, open models, tools, all in one place.
- [dair-ai/Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide). Deep, well-maintained guide to prompting, context engineering, RAG and agents.
- [roadmap.sh/ai-engineer](https://roadmap.sh/ai-engineer). The interactive AI engineer roadmap. A different take on the same journey, worth a look for a second opinion.
- [DeepLearning.AI short courses](https://www.deeplearning.ai/courses/). Free, short, hands-on courses on basically every topic on this list. My default when I want to learn one thing fast.

## Follow

I'm breaking down every step in this roadmap. If it's useful, follow along:

- YouTube: [@khanhgn](https://youtube.com/@khanhgn)
- TikTok: [@khanhcore](https://tiktok.com/@khanhcore)
- Instagram: [@khanhcore](https://instagram.com/khanhcore)
- X: [@khanhcore](https://x.com/khanhcore)

Star this repo so you can find it later, and share it with someone who's just starting out.

## Contributing

Found a broken link or a resource that belongs here? Open an issue or a pull request. Keep it free, high-quality, and beginner-friendly.

## License

[MIT](LICENSE). Use it, remix it, share it.
