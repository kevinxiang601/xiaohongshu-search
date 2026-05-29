---
name: xiaohongshu-search
description: Research and summarize travel guidance primarily from Xiaohongshu posts. Use when the user asks for travel guides, itineraries, hotel or food choices, route planning, ticket strategy, crowd-avoidance tips, packing advice, or destination comparisons that should be grounded in real Xiaohongshu experience, especially when the current workspace already contains travel-planning files that should be read first. Prefer searching the Xiaohongshu official site, breaking the task into multiple keyword searches, collecting patterns across many posts, and using non-Xiaohongshu sources only as secondary support for hard facts.
---

# Xiaohongshu Search

## Overview

Use this skill to build travel answers from real Xiaohongshu experience posts instead of generic web summaries. Read local travel notes first when they exist, then search Xiaohongshu with multiple keyword combinations and turn repeated post patterns into a practical plan.

## Workflow

### 1. Read local context first

- Inspect the current workspace folders and files when the request relates to existing travel notes.
- Extract the destination, travel dates, traveler mix, budget, transport mode, must-do items, pace, and special constraints.
- Reuse the local trip structure and naming when continuing or updating an existing guide.
- If the workspace already contains a draft guide, use Xiaohongshu evidence to confirm, adjust, or replace parts of that draft instead of starting from zero.

### 2. Break the task into search angles

- Decompose the request into several keyword groups instead of one broad query.
- Combine:
  - destination
  - attraction, district, hotel, or transport node
  - trip goal such as `璺嚎`, `浣忓`, `闂ㄧエ`, `鎺掗槦`, `缇庨`, `閬垮潙`, `鎷嶇収`, `棰勭畻`
  - traveler traits such as `瀹跺涵`, `鎯呬荆`, `瀛︾敓`, `甯﹁€佷汉`, `甯﹀皬瀛ー
  - time traits such as `鍛ㄦ湯`, `宸ヤ綔鏃, `鏆戝亣`, `闆ㄥぉ`, `澶滃満`
- Use keyword sets like:
  - `鍖椾含鐜悆 浜插瓙 涓ゅぉ璺嚎`
  - `棣欐腐杩＋灏?鎻愭棭鍏ュ洯 灏婁韩鍗?閬垮潙`
  - `鍗庡己鍖?涓€鏃ユ父 璐墿 閬垮潙`

### 3. Search Xiaohongshu first

- Open `https://www.xiaohongshu.com/explore?language=zh-CN` in the browser.
- Use the site search bar and run the keyword sets one by one.
- Open many relevant posts, not just the top one or two results.
- For an ordinary destination question, inspect about 8 to 15 strong posts across multiple keyword sets when possible. For a broader itinerary or comparison task, inspect more before settling on a conclusion.
- Prefer recent posts and posts with concrete details such as queue times, prices, routes, hotel comparisons, transport steps, meal suggestions, and mistakes to avoid.
- Treat Xiaohongshu as the primary evidence base.
- Use other websites only to support hard facts such as opening hours, ticket rules, transport schedules, maps, or official policy.
- If the homepage search is blocked or incomplete, keep Xiaohongshu as the main source by finding more Xiaohongshu post URLs through browser search results and opening those pages directly.

### 4. Extract recurring experience

- Capture repeated advice instead of isolated opinions.
- Pull out:
  - what people repeatedly recommend
  - what people repeatedly warn against
  - what conditions change the advice
  - which advice best matches the user's group, budget, and travel style
- Note meaningful disagreement when it matters, such as "faster but more tiring" versus "costs more but works better for families."

### 5. Synthesize into an actionable answer

- Turn raw post patterns into a clear plan instead of a post-by-post dump.
- Prefer specific conclusions over vague summary.
- When enough evidence exists, organize the result into:
  - recommended plan
  - why it fits this traveler
  - alternatives
  - cautions
  - next decision to make
- Make it clear when a point comes mainly from Xiaohongshu experience and when it comes from an official rule.

## Output Rules

- Base the conclusion mainly on Xiaohongshu post patterns.
- Do not pretend one post equals consensus.
- Do not over-trust old posts when prices, crowds, or rules may have changed.
- When the user asks for a guide, include concrete steps, not only background.
- Keep wording simple, practical, and easy to act on.

## Quality Check

- Confirm Xiaohongshu was the main source, not a side note.
- Confirm multiple keyword searches were used.
- Confirm the answer reflects the user's real travel constraints or the local workspace files.
- Confirm non-Xiaohongshu sources only played a supporting role for hard facts.
- Confirm the final advice was synthesized from repeated experience rather than copied from individual posts.
