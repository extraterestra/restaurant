# Fix: Change Redirect to Rewrite in Render

## Problem
You configured a redirect rule, but it's changing the URL from `/admin` to `/index.html`. This prevents React from seeing the original path.

## Solution

In Render Dashboard:

1. Go to your **restaurant-frontend** service
2. Go to **Settings** tab
3. Find the **"Redirect and Rewrite Rules"** section
4. **Change the Action dropdown from "Redirect" to "Rewrite"**
5. Click **"Save Changes"**

## What's the Difference?

- **Redirect (301/302)**: Changes the URL in the browser
  - `/admin` → Browser URL becomes `/index.html` ❌
  - React never sees `/admin`

- **Rewrite (200)**: Serves `index.html` but keeps the original URL
  - `/admin` → Browser URL stays `/admin` ✅
  - React sees `/admin` and handles it correctly

## Correct Configuration

- **Source**: `/*`
- **Destination**: `/index.html`
- **Action**: **"Rewrite"** (not "Redirect")

After saving, wait for the service to update (usually instant), then test:
- `https://restaurant-frontend-nuu5.onrender.com/admin` should show the admin panel
- The URL should stay as `/admin` (not change to `/index.html`)

