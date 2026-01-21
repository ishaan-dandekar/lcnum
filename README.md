# LCNum

**LCNum** is a tiny redirect service that lets you open LeetCode problems using their **problem number** instead of the slug.

Instead of remembering:

```
https://leetcode.com/problems/matrix-block-sum/
```

you can just use:

```
https://lcnum.ishdn.me/1314
```

and get redirected instantly.

No UI. No accounts. No tracking. Just numbers → problems.

---

## Why this exists

LeetCode internally assigns every problem a **stable numeric ID**.
Humans, unfortunately, are asked to remember slugs.

LCNum fixes that mismatch.

This is useful when:

* You remember *“problem 1314”* but not the title
* You’re discussing problems verbally or in notes
* You want fast, copy-pasteable links
* You’re building tooling, scripts, or extensions around LeetCode

---

## How it works (high level)

1. LCNum runs on **Cloudflare Workers** (edge-deployed JavaScript)

2. A **Workers KV** store maps:

   ```
   problem_number → problem_slug
   ```

3. When you visit:

   ```
   /<number>
   ```

   LCNum:

   * Looks up the number in KV
   * Redirects you to:

     ```
     https://leetcode.com/problems/<slug>/
     ```

That’s it. One lookup, one redirect.

---

## Usage

### Redirect by problem number

```
https://lcnum.ishdn.me/1
→ https://leetcode.com/problems/two-sum/
```

```
https://lcnum.ishdn.me/1314
→ https://leetcode.com/problems/matrix-block-sum/
```

### Root page

Visiting the root:

```
https://lcnum.ishdn.me/
```

shows a short tutorial explaining how to use the service.

---

## What this is (and isn’t)

### ✅ This **is**

* A redirect service
* Deterministic and stateless at runtime
* Fast (edge-served)
* Free to use

### ❌ This is **not**

* A LeetCode scraper
* A mirror of LeetCode content
* An official LeetCode API
* A replacement for LeetCode

All content ultimately lives on leetcode.com.

---

## Data source

The problem number → slug mapping is:

* Generated offline
* Uploaded once into Workers KV
* Read-only during normal operation

No writes happen during user requests.

---

## Tech stack

* **Cloudflare Workers**
* **Cloudflare Workers KV**
* Plain JavaScript (no framework)
* DNS + HTTPS via Cloudflare

---

## Status

* Core redirect logic: ✅ complete
* KV populated: ✅
* Custom domain: ✅
* Root tutorial page: ✅
* Daily / metadata endpoints: ⏳ planned (intentionally deferred)

---

## Author

Built by **Ishaan Dandekar**
Personal infra, learning project, zero monetization.

---

## License / Disclaimer

This project is **not affiliated with LeetCode**.
LeetCode is a trademark of LeetCode, Inc.

Use responsibly.
