---
name: quantlix-inquiry-preparation
description: Prepare a Quantlix project inquiry from a person's approved requirements and details when they ask to contact Quantlix, preserving explicit consent and review before submission.
---

# Quantlix inquiry preparation

## When to use this

Use this skill when a person asks to draft or send a project inquiry to Quantlix. A service-research question alone does not authorize contact or newsletter subscription.

Read https://quantlix.com/openapi.json for the current contact schema and https://quantlix.com/auth.md for public access boundaries. Identify the relevant published service through search_pages and read_page at https://quantlix.com/mcp/ if needed.

Prepare the project scope, constraints and specific questions using only the person's supplied requirements. Ask for missing required personal details rather than guessing. Show the proposed name, email, subject, message and optional company/phone details for review. Obtain genuine consent and explicit direction to send the approved content. Draft preparation does not itself submit anything.

An authorized client may POST JSON to https://quantlix.com/api/contact/ with consent=true and the documented fields, with a 20 KiB body limit. A native form requires consent=yes and a same-origin Origin header. A confirmed write is HTTP 201 with ok=true. JSON errors include code, message and hint.

On validation failure, resolve only the rejected fields with the person. Before an approved write, generate an Idempotency-Key of 16-128 ASCII letters, digits, dots, underscores, colons or hyphens. On timeout, retry only with that original key and identical approved input. Without a key, do not retry automatically or claim success: a lead may already exist. Reusing a key with changed input returns 409. Keys are scoped by operation and retained durably. MCP and WebMCP are read-only and cannot submit the inquiry. Never use a live submission as a test.
