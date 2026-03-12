# asyncio-team-guide

## Overview
This repository provides a concise guide to Python **asyncio** best practices and performance optimisation techniques for 2024. The material is distilled from the official Python documentation and a highly‑rated Real Python tutorial.

## Key Best Practices

1. **Prefer `asyncio.run()` for top‑level entry points** – it creates and closes the event loop safely.
2. **Structure concurrency with high‑level APIs** – use `asyncio.create_task()` to launch independent coroutines and `await` them via `asyncio.gather()` for parallel execution.
3. **Limit the number of concurrent tasks** – employ `asyncio.Semaphore` or `asyncio.BoundedSemaphore` to avoid overwhelming resources (e.g., network sockets).
4. **Avoid blocking calls** – never call time‑consuming CPU‑bound functions directly; offload them to a thread pool via `loop.run_in_executor` 
ord `async` etc.
