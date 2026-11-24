# Weekly reel agent (Tuesday, 7:15 PM Nairobi)

Scheduled Claude task that scripts, renders and publishes one short text reel a week to Facebook and Instagram, and prepares the same reel for the owner to post on TikTok. Condensed and sanitised from the production prompt.

## Steps
1. **Topic.** Read the Make data store. Stop if paused, or if a reel is already `Posted` for this Monday-to-Sunday week (one reel per week). Reuse Monday's post topic, or pick an educational job-search topic not used in the last 8 weeks. Create a `reel-YYYY-MM-DD` record as `Planned`.
2. **Script.** Four slides for a 12 to 20 second reel told as a mini story: a hook naming a common struggle (max 7 words), two value slides (max 15 words each, any example CV text labelled "Example"), and a call-to-action slide with the WhatsApp number and an official price or proof point. Write Instagram, Facebook and TikTok captions and a reel title. Same brand rules as the post agent: no invented results, no promises of jobs, no em dashes.
3. **Video.** Generate a 4-page vertical (9:16) story design in Canva, choose the candidate with the most pages, and export it as MP4 (vertical 1080p). If Canva fails twice, mark the record `Failed`, email the owner and stop.
4. **Publish.** Run the `Publish Reel` Make scenario with `platforms = facebook,instagram` and the MP4 URL. If the call returns a gateway or timeout error, **do not run it again**: find the run in the execution list and poll it until it finishes (avoids double posting). Check modules 2 (Facebook) and 3 (Instagram); retry only a failed platform once.
5. **Log and report.** Update the record (`Posted` / `Partial` / `Failed`, platforms, hook, design link, errors). Email the owner the result, a "Post to TikTok in 5 minutes" section (design link, steps, caption) and the other captions.

## Fallback added after production failures
Canva's generate-design started failing on most runs from early November 2026. The working fallback is to copy a previously checked reel layout, rewrite the text on each page, and export that copy as MP4.
