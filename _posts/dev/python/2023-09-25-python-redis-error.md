---
title: "[Python] TypeError: duplicate base class TimeoutError (aioredis)"
date: 2023-09-25
categories: [Dev, Python]
tags: [Python]
---

## Problem

Recently, I have been working on my fast-api project using a virtual environment.

However, I ran up with this error:

> class TimeoutError(asyncio.TimeoutError, builtins.TimeoutError, RedisError): 
> 
> TypeError: duplicate base class TimeoutError
{: .prompt-warning}

I found out that this error was due to ***aioredis not being supported anymore and being replaced by redis library***.

## Solution

1. `pip uninstall aioredis`

2. `pip install "redis>=4.2.0rc1"`

3. In ***".venv/Lib/site-packages/fastapi_mail/email_utils/email_check.py"*****:**
    > change `import redis` to `from redis import asyncio as aioredis`