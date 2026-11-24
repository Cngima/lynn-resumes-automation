# Make data store: "Lynn Resumes Post Log"

The agents have no memory between runs, so all state lives in one Make data store. Every run reads it first and writes to it last.

## Record fields
| Field | Purpose |
|---|---|
| `key` | Record ID (see key patterns below) |
| `date` | Run date (Africa/Nairobi) |
| `pillar` | Content type: Educational, Client Story, Offer, Community, REEL, WHATSAPP |
| `topic` | What the post covered, used to avoid repeats |
| `status` | `Planned`, `Posted`, `Partial`, `Failed`, `Sent to Carol` |
| `platforms_ok` | Platforms that returned a post ID |
| `headline` | Main line on the graphic |
| `canva_design` | Edit link of the design that passed the quality check |
| `notes` | Screenshot used, what the quality check fixed, errors |

## Key patterns
| Key | Written by | Holds |
|---|---|---|
| `config` | Owner | Business facts the agents may use: contact numbers, proof points, positioning, prices, process, services, topic backlog, `paused: yes` switch |
| `YYYY-MM-DD` | Social post agent | One record per posting day |
| `reel-YYYY-MM-DD` | Reel agent | One record per weekly reel |
| `wa-YYYY-MM-DD` | WhatsApp agent | Daily Status pack |
| `story-<canva asset id>` | Set up with Claude, checked by the owner | The facts visible in each client testimonial screenshot, and whether it may be used (`Use` / `Exclude`) |

## Why the `story-` records exist
Client stories must never claim anything the client did not say. Each screenshot was read once, its visible facts were written down, and screenshots that showed a client's name or sensitive content were marked `Exclude`. Agents may only tell a story from these recorded facts.
