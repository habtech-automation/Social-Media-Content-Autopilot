# Social Media Content Autopilot

Write a post once in a Google Sheet. It publishes to Facebook, LinkedIn and Instagram automatically.

## The Problem

Small businesses and solo founders post the same update on several platforms by hand. They copy the text, resize the image, log in to each app and paste it again. It eats time every week, and posting becomes inconsistent the moment things get busy.

## Business Impact

- One entry in a spreadsheet replaces three manual posts
- Content goes out on a steady schedule without anyone logging in to each platform
- The whole team can add posts from one shared sheet, with no access to the social accounts themselves
- Instagram is skipped automatically when a row has no image, so nothing fails on text-only posts

## How It Works

```
Google Sheets (new row added)
        |
        v
     Router
        |
        +--> Facebook Pages: create a post (text + link)
        |
        +--> LinkedIn: create a text post
        |
        +--> Instagram Business: create a photo post (only if Image URL is filled)
```

Make checks the sheet every 15 minutes. Each new row is sent down all three paths at once.

## Stack

| Tool | Purpose |
|------|---------|
| Make.com | Workflow automation and scheduling |
| Google Sheets | Content queue |
| Facebook Pages | Publishing to a business Page |
| LinkedIn | Publishing to a profile |
| Instagram for Business | Publishing photo posts (via Facebook login) |

## Sheet Layout

| Column | Name | Used for |
|--------|------|----------|
| A | Post Text | Post body on Facebook and LinkedIn, caption on Instagram |
| B | Image URL | Public direct JPEG link for Instagram (leave empty to skip Instagram) |
| C | Link | Link attached to the Facebook post |

## Setup

1. Create a Google Sheet with the three columns above. See `sample-data/social-posts-sample.csv`.
2. In Make, create a new scenario and import `blueprint/social-media-content-autopilot.blueprint.json`.
3. Add your own connections for Google Sheets, Facebook Pages, LinkedIn and Instagram for Business.
4. Replace the placeholders in the blueprint modules:
   - `YOUR_SPREADSHEET_ID` and `YOUR_SHEET_TAB_NAME` in the Google Sheets module
   - `YOUR_FACEBOOK_PAGE_ID` in the Facebook Pages module
   - `YOUR_INSTAGRAM_ACCOUNT_ID` in the Instagram module
5. Run the scenario once with a test row, then switch it on.

### Instagram requirements

- The Instagram account must be a Business or Creator account linked to your Facebook Page
- Images must be a public, direct JPEG link. Google Drive links do not work
- The aspect ratio must be between 4:5 and 1.91:1

## Files

| File | Description |
|------|-------------|
| `blueprint/social-media-content-autopilot.blueprint.json` | Make scenario blueprint with all IDs and connections removed |
| `sample-data/social-posts-sample.csv` | Example sheet content |
| `images/scenario-proof.png` | Screenshot of the live scenario running in Make |

## Notes

- Posts publish publicly, so test with a single row first
- The scenario is built to watch new rows only, so each row is posted once
