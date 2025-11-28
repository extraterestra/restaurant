# Troubleshooting: Rewrite Rule Not Working

## Problem
You've set the rewrite rule correctly (Source: `/*`, Destination: `/index.html`, Action: "Rewrite"), but the URL still changes to `/index.html` when visiting `/admin`.

## Possible Causes

### 1. Browser Cache
The browser might be caching the old redirect behavior.

**Solution:**
- Clear browser cache (Ctrl+Shift+Delete or Cmd+Shift+Delete)
- Or use **Incognito/Private browsing mode**
- Or hard refresh (Ctrl+F5 or Cmd+Shift+R)

### 2. Rewrite Rule Not Applied
The rule might not have been saved correctly.

**Check:**
1. Go to Render Dashboard → Your Frontend Service → Settings
2. Verify the rule shows:
   - Source: `/*`
   - Destination: `/index.html`
   - Action: **"Rewrite"** (not "Redirect")
3. Make sure "Save Changes" button was clicked and shows as saved

### 3. Service Needs Restart
Sometimes Render needs a moment to apply the rewrite rule.

**Solution:**
- Wait 1-2 minutes after saving
- Or manually trigger a redeploy (even if no code changed)

### 4. Multiple Rules Conflict
If you have multiple rules, they might conflict.

**Solution:**
- Remove any other redirect/rewrite rules
- Keep only one rule: `/*` → `/index.html` with Action: "Rewrite"

## Testing the Rewrite Rule

1. **Open browser DevTools** (F12)
2. Go to **Network** tab
3. Visit: `https://restaurant-frontend-nuu5.onrender.com/admin`
4. Look at the first request:
   - **Request URL**: Should show `/admin`
   - **Response**: Should be `index.html` content
   - **Status**: Should be `200` (not 301/302)

If you see:
- **Status 301/302**: The rule is still a redirect, change it to "Rewrite"
- **Status 404**: The rule isn't working, check configuration
- **Status 200 with `/index.html` in URL**: Browser cache issue, clear cache

## Alternative: Check Render Documentation

Render's rewrite behavior might have specific requirements. Check:
- [Render Static Site Documentation](https://render.com/docs/static-sites)
- Look for "rewrite rules" or "SPA routing" in their docs

## Quick Fix: Force URL Update in Code

The updated `App.tsx` now includes logic to detect and fix the URL if it gets changed to `/index.html`. After deploying the updated code:

1. Commit and push the changes
2. Wait for Render to redeploy
3. Clear browser cache
4. Test `/admin` route

The code will now:
- Detect if URL is `/index.html` but should be `/admin`
- Automatically fix the URL using `history.replaceState`
- Show the admin panel correctly

