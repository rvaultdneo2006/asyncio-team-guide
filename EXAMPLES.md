# Asyncio Usage Examples

## Simple Task Creation
```python
import asyncio

async def fetch_data(i):
    await asyncio.sleep(1)
    return f"result {i}"

async def main():
    tasks = [asyncio.create_task(fetch_data(i)) for i in range(5)]
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())
```

## Limiting Concurrency with Semaphore
```python
import asyncio

sem = asyncio.Semaphore(3)

async def limited_task(i):
    async with sem:
        await asyncio.sleep(2)
        print(f"Task {i} done")

async def main():
    await asyncio.gather(*(limited_task(i) for i in range(10)))

asyncio.run(main())
```

## Cancelled Tasks Graceful Cleanup
```python
import asyncio

async def worker():
    try:
        while True:
            print("working...")
            await asyncio.sleep(1)
    except asyncio.CancelledError:
        print("cleanup before exit")
        raise

async def main():
    task = asyncio.create_task(worker())
    await asyncio.sleep(3)
    task.cancel()
    try:
        await task
    except asyncio.CancelledError:
        pass

asyncio.run(main())
```

## Running Blocking Code in Executor
```python
import asyncio, time

def blocking_io():
    time.sleep(2)
    return "io result"

async def main():
    loop = asyncio.get_running_loop()
    result = await loop.run_in_executor(None, blocking_io)
    print(result)

asyncio.run(main())
```

---
These examples illustrate common patterns for task management, concurrency limiting, cancellation handling, and integrating blocking I/O with asyncio.
