# Network Brief — nb-k4r9wm2x

Private, personalized introduction-facilitation page. Deployed at:
`https://bobthebuilder-creates.github.io/nb-k4r9wm2x/`

**Do not link this directory from the main site.**

---

## How it works

1. A referrer opens the URL on their phone
2. They type their first name — the page shows their personalized intro message and contacts
3. Each contact card expands to show context, the ask, and a pre-drafted forward note they copy with one tap
4. You update `referrers.json` on GitHub; they refresh and see the change

---

## Updating contacts

All data lives in `referrers.json`. Edit it directly on GitHub or locally and push.

### JSON schema

```json
{
  "lastUpdated": "YYYY-MM-DD",
  "referrers": [
    {
      "name": "Full Name",
      "firstName": "First",
      "intro": "Personalized greeting. **Bold** and *italic* supported. Double newline = new paragraph.",
      "contacts": [
        {
          "name": "Contact Full Name",
          "title": "Title · Organization",
          "company": "Company",
          "status": "pending",
          "req": {
            "company": "Company · Location",
            "title": "Role Title",
            "reqId": "123456789",
            "url": "https://..."
          },
          "why": "Why this person matters for the introduction.",
          "ask": "What you're asking for — specific and bounded.",
          "forwardNote": "The exact text the referrer can copy and send."
        }
      ]
    }
  ]
}
```

### Status values

| Value | Meaning |
|-------|---------|
| `pending` | Not yet sent — shows in main list |
| `sent` | Introduction requested — shows in main list |
| `connected` | Intro made, conversation happened — moves to Closed loop |
| `closed` | No longer pursuing — moves to Closed loop |

Contacts with status `connected` or `closed` are automatically moved to the de-emphasized "Closed loop" section at the bottom.

### Adding a referrer

Add a new object to the `referrers` array. `firstName` is what the name-matching uses (case-insensitive, whitespace-trimmed). One person can appear once; if the same first name is shared by two referrers, the first match wins — use distinct first names or disambiguate with a middle name in `firstName`.

### Adding a contact to an existing referrer

Append to that referrer's `contacts` array. Order in the array is display order.

### Removing a contact

Delete the object from the array. If you want to keep it for record-keeping, set `status` to `closed` instead.

---

## Security model

Security through unlinkability — the URL slug is the only protection. The page is:

- Not linked from the main site
- Marked `noindex, nofollow` via both `<meta name="robots">` and `robots.txt`
- Cache-busted on each load so referrers always see current data

**Do not include classified information, home address, SSN, or anything catastrophically sensitive.** Anyone with the URL can read the content.

---

## File structure

```
nb-k4r9wm2x/
  index.html       — single-file app (HTML + CSS + JS)
  referrers.json   — all data; edit this to update the page
  robots.txt       — noindex directive for this path
  README.md        — this file
```

No build step. No dependencies. Edit `referrers.json` and push.

---

## Deployment

This directory deploys automatically as part of the parent GitHub Pages site at `bobthebuilder-creates.github.io`. No additional configuration needed — GitHub Pages serves all files in the repo.

If you add this as a new subdirectory to an existing repo, GitHub Pages will pick it up on next push without any settings change.
