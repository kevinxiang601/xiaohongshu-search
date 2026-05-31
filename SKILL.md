---
name: xiaohongshu-search
description: Research and summarize travel guidance primarily from Xiaohongshu posts. Use when the user asks for travel guides, itineraries, hotel or food choices, route planning, ticket strategy, crowd-avoidance tips, packing advice, or destination comparisons that should be grounded in real Xiaohongshu experience, especially when the current workspace already contains travel-planning files that should be read first. Prefer searching Xiaohongshu in the user's normal browser through the Codex browser extension, opening posts from search-result cards, scrolling result pages and post detail panels, and using non-Xiaohongshu sources only as secondary support for hard facts.
---

# Xiaohongshu Search

## Overview

Use this skill to build travel answers from real Xiaohongshu experience posts instead of generic web summaries.

The preferred workflow is:

1. Use the user's normal browser session controlled by the browser Codex extension.
2. Search inside Xiaohongshu.
3. Open posts by clicking result cards, not by directly visiting copied post URLs.
4. Scroll both the search results page and the opened post detail panel.
5. Extract repeated advice across many posts.
6. Summarize into practical travel guidance.

Important discovery from testing: directly opening a Xiaohongshu post URL may show "当前笔记暂时无法浏览，请打开小红书App扫码查看". The reliable method is usually to search inside Xiaohongshu, then click the post card from the search results page. This opens a web detail panel where the post text and comments can often be read.

## Browser Requirement

This skill must use Xiaohongshu through the user's normal browser session controlled by the browser Codex extension.

Do not use the Codex in-app Browser, the right-side built-in browser, or `browser:control-in-app-browser` for Xiaohongshu collection. The in-app Browser does not share the user's Xiaohongshu login state and is not acceptable for this skill.

If the user's normal browser is not open:

- Use `computer-use:computer-use` to open the user's normal browser first.
- Then connect through the browser Codex extension / extension-backed browser control.
- Then open Xiaohongshu in that browser session and continue the workflow.

If the browser Codex extension cannot connect, stop and explain the issue. Do not switch to the in-app Browser.

Important rule:

- If the browser Codex extension cannot connect, stop the task and explain the issue to the user.
- If Xiaohongshu cannot be accessed through the controlled browser session, stop and explain.
- If the user is not logged in and the task requires logged-in Xiaohongshu search, ask the user to log in in the controlled browser page, then retry.
- Do not fall back to the Codex in-app Browser, generic web search, search engines, other browsers, or non-Xiaohongshu sources for finding posts unless the user explicitly asks for that.
- Non-Xiaohongshu sources may only be used later for hard facts such as opening hours, ticket rules, official policy, transport schedules, or weather, and only when needed.

If the browser Codex extension cannot connect, do not continue with another search method. Say something like:

> 我现在连不上装有 Codex 插件的浏览器，所以没法使用你的小红书登录态抓取帖子。这个 skill 要求必须从你的浏览器 Codex 插件进入小红书；我不会改用右侧内置浏览器或其他搜索来源。你可以检查浏览器是否打开、Codex 插件是否开启，或重新打开浏览器后让我再试。

Then stop.

## Workflow

### 1. Read local context first

- Inspect the current workspace folders and files when the request relates to existing travel notes.
- Extract the destination, travel dates, traveler mix, budget, transport mode, must-do items, pace, and special constraints.
- Reuse the local trip structure and naming when continuing or updating an existing guide.
- If the workspace already contains a draft guide, use Xiaohongshu evidence to confirm, adjust, or replace parts of that draft instead of starting from zero.

### 2. Break the task into search angles

Decompose the request into several keyword groups instead of one broad query.

Combine:

- destination
- attraction, district, hotel, or transport node
- trip goal such as `路线`, `住宿`, `门票`, `排队`, `美食`, `避坑`, `拍照`, `预算`, `必玩`, `红黑榜`, `项目推荐`
- traveler traits such as `家庭`, `情侣`, `学生`, `带老人`, `带小孩`, `亲子`
- time traits such as `周末`, `工作日`, `暑假`, `寒假`, `雨天`, `夜场`

Use keyword sets like:

- `北京环球影城 必玩项目 推荐`
- `北京环球影城 项目排名 攻略`
- `北京环球影城 排队 避坑`
- `北京环球影城 带娃 项目`
- `北京环球影城 一日游 路线`
- `香港迪士尼 提前入园 尊享卡 避坑`
- `华强北 一日游 购物 避坑`

### 3. Search Xiaohongshu inside the controlled browser

Use the user's normal browser session controlled by the browser Codex extension. Do not use the right-side built-in Browser.

1. Open `https://www.xiaohongshu.com/explore?language=zh-CN`.
2. Use the Xiaohongshu search box or Xiaohongshu search-result page.
3. If search results show "登录后查看搜索结果" or similar login prompts:
   - stop searching,
   - tell the user the controlled browser session is not logged in,
   - ask the user to log in on that browser page,
   - retry only after the user confirms.
4. Do not switch to external search engines to find Xiaohongshu URLs.
5. After results load, extract visible result cards.
6. If there are not enough relevant cards:
   - scroll the Xiaohongshu results page downward,
   - wait for more posts to load,
   - extract again.
7. If results are still weak:
   - change the Xiaohongshu keyword,
   - search again inside Xiaohongshu,
   - repeat card extraction.

If the input box is hard to fill programmatically, try:

- clicking an existing search history suggestion
- typing like a user with keyboard input
- opening the Xiaohongshu search-result URL
- searching a simpler keyword first

### 4. Collect enough search-result cards

On the search results page:

- Extract visible result cards: title, author, date, like/comment number if shown, and URL if available.
- Prefer posts that are:
  - recent
  - specific
  - experience-based
  - high interaction
  - directly relevant to the user's question
- Avoid relying only on sponsored, ticket-agent, or generic list posts.

If the current page does not show enough relevant posts:

- Scroll the Xiaohongshu search results page downward to load more cards.
- Re-extract the card list after scrolling.
- Repeat until there are enough relevant candidates.
- If results are still weak, change keywords and search again inside Xiaohongshu.

For an ordinary destination or attraction question, inspect about 8 to 15 strong posts when possible. For a broader itinerary or comparison task, inspect more.

### 5. Open posts by clicking result cards

Do not rely on direct post URLs as the primary method.

Preferred method:

1. Stay on the Xiaohongshu search results page.
2. Click a relevant post card directly.
3. Wait for the post detail panel or overlay to open.
4. Extract the visible text.
5. Scroll the right-side post content/comment area.
6. Extract again after each scroll.
7. Merge and deduplicate text lines.
8. Close the post detail panel.
9. Click the next result card.

Directly opening `https://www.xiaohongshu.com/explore/...` may fail with an App-only message. Clicking the card from the search results page is more reliable because it preserves the correct `xsec_token` and `xsec_source`.

### 6. Scroll inside each post

After opening a post, the text and comments may not all be visible at first.

For each post:

- Identify the right-side detail area containing:
  - author
  - title
  - post text
  - hashtags
  - edit date
  - comments
  - like/favorite/comment counts
- Scroll that right-side area downward several times.
- After each scroll, extract text again.
- Merge all extracted text and remove duplicate lines.
- Capture high-signal comments, especially:
  - high-liked comments
  - author replies
  - repeated questions from users
  - comments correcting or disagreeing with the post
  - comments giving current queue times, prices, routes, or recent conditions

Do not assume the first visible screen is the full post.

### 7. What to extract from each post

For every useful post, capture:

- post title
- author if visible
- date or edit date if visible
- URL if available
- main claims or recommendations
- concrete details:
  - queue times
  - route order
  - ticket or pass strategy
  - transport steps
  - prices
  - hotel or restaurant names
  - crowd level
  - weather or season context
- warnings and `避坑`
- relevant high-liked comments or author replies
- whether the post seems like:
  - personal experience
  - commercial/ticket-agent content
  - generic list
  - old or possibly outdated information

### 8. Extract recurring experience

Capture repeated advice instead of isolated opinions.

Pull out:

- what people repeatedly recommend
- what people repeatedly warn against
- which advice depends on traveler type
- which advice depends on time, crowd, or budget
- where posts disagree meaningfully

For example:

- "刺激党必玩" versus "带娃慎选"
- "排队久但值得" versus "排队久不值得"
- "工作日可裸冲" versus "节假日必须早享/优速通"
- "适合拍照" versus "不适合专门排队"

### 9. Use non-Xiaohongshu sources only for hard facts

Treat Xiaohongshu as the primary evidence base for lived experience.

Use other sources only to verify hard facts such as:

- official opening hours
- ticket rules
- transport schedules
- official show times
- weather
- map locations
- current policy changes

Clearly separate "Xiaohongshu experience pattern" from "official rule".

### 10. Synthesize into an actionable answer

Turn raw post patterns into a clear plan.

Prefer specific conclusions over vague summaries.

When enough evidence exists, organize the result into:

- recommended plan
- priority ranking
- why it fits the traveler
- alternatives
- cautions
- what to skip or only do if time is left
- next decision the user should make

Example structure:

- "最推荐"
- "第二梯队"
- "不建议硬排"
- "适合带娃"
- "适合刺激党"
- "适合拍照"
- "避坑"
- "一日路线建议"

## Browser Extension Extraction Pattern

When using browser plugin tools, the successful pattern is:

1. If the user's normal browser is not open, use Computer Use to open it first.
2. Connect to that browser through the browser Codex extension / extension-backed browser control.
3. Open Xiaohongshu.
4. Search keyword inside Xiaohongshu.
5. Click a result card.
6. Extract detail panel text.
7. Scroll the post detail area.
8. Extract again.
9. Close panel.
10. Scroll result page if needed.
11. Continue to the next post.

Pseudo-flow:

```js
// Conceptual flow only. Follow the active extension-backed browser skill's exact setup instructions.
// Do not use the Codex in-app Browser/right-side Browser for this skill.

if the user's normal browser is not open:
  open the user's normal browser with Computer Use

connect to the browser through the Codex browser extension
open Xiaohongshu explore page
search keyword inside Xiaohongshu

while collectedPosts < target:
  cards = extract visible result cards

  if cards are not enough:
    scroll search results page down
    continue

  for each relevant card:
    click card from search results page
    wait for post detail panel

    postTextPieces = []
    repeat several times:
      postTextPieces.push(extract visible detail panel text)
      scroll right-side post detail/comment area down

    mergedPostText = merge and deduplicate postTextPieces
    save title, author, date, url, text, comments

    close detail panel

  if collectedPosts still not enough:
    change keyword and search again inside Xiaohongshu
```

Important implementation notes:

- Do not use the Codex in-app Browser even if it is easier to open a page there.
- Clicking search-result cards is more reliable than directly opening post URLs.
- If direct URL opens an App-only block, go back to search results and click the card.
- If a card opens but the text seems incomplete, scroll the right-side detail area.
- If comments do not load, scroll more slowly and wait briefly between scrolls.
- If the search results are sparse, scroll the results page down or use a new Xiaohongshu keyword.
- If the page has search history suggestions, clicking a suggestion can be more reliable than filling the input box.

## Output Rules

- Base the conclusion mainly on Xiaohongshu post patterns.
- Do not pretend one post equals consensus.
- Do not over-trust old posts when prices, crowds, or rules may have changed.
- Include the number of posts inspected when useful.
- Mention if some posts were App-only or could not be fully read.
- When the user asks for a guide, include concrete steps, not only background.
- Keep wording simple, practical, and easy to act on.
- Do not dump every post. Summarize repeated patterns and cite representative post titles when helpful.

## Quality Check

Before finalizing, confirm:

- Xiaohongshu was the main source.
- Multiple posts were inspected.
- Browser Codex extension access worked; if it did not work, the task stopped instead of falling back to the in-app Browser or other search sources.
- Multiple Xiaohongshu keyword searches were used if the first keyword was weak.
- Search-result cards were clicked directly when possible.
- The search results page was scrolled if there were not enough posts.
- Post detail panels were scrolled to capture more complete text and comments.
- The answer reflects the user's real travel constraints or local workspace files.
- Non-Xiaohongshu sources only supported hard facts.
- The final advice was synthesized from repeated experience rather than copied from one post.
