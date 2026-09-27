KING PIZZA ATTENDANCE — "ADD TO PHONE" FIX
============================================

WHAT WAS WRONG
---------------
Chrome and Edge only offer a real "Add to phone" / "Install app" option
when a page qualifies as an installable web app. That requires THREE
things which the original files did not have:
  1. A web app manifest (name, icons, start screen).
  2. A registered service worker (a small background script).
  3. The page served over HTTPS (or http://localhost) — NOT opened
     directly from a file (a file:// address never qualifies, no
     matter what is in the HTML).

WHAT WAS ADDED
---------------
Every HTML file now links to its own manifest (manifest-<branch>.json),
a shared service worker (sw.js) is registered automatically, and two
app icons (icon-192.png, icon-512.png) were generated from the existing
King Pizza logo. Each sidebar also got an "Install App" button that
appears once Chrome/Edge decides the page is installable, as a backup
to the browser's own menu option.

Files you must upload TOGETHER, in the same folder, on a real web
server (or hosting service) reached over https://:
  - all 7 King_Pizza_*.html files
  - all 7 manifest-*.json files
  - sw.js
  - icon-192.png
  - icon-512.png

HOW TO CHECK IT WORKED
-----------------------
1. Upload the folder to your HTTPS host (e.g. your existing web
   hosting, Netlify, Vercel, Firebase Hosting, GitHub Pages, etc.).
2. Open one of the King_Pizza_*.html pages in Chrome or Edge on an
   Android phone (or desktop Chrome/Edge for a quick check).
3. Wait a few seconds and use the browser's menu (⋮) — "Add to phone"
   / "Install app" should now appear, or the "Install App" button in
   the sidebar will appear on its own.
4. If it still doesn't appear, open Chrome DevTools → Application →
   Manifest on desktop first — it will tell you exactly which
   requirement (icon, HTTPS, manifest field) is still missing on your
   hosting.

IMPORTANT
---------
If these files are opened by double-clicking them on the phone/PC
(a file:// address in the address bar), "Add to phone" will never
work — this is a browser security rule, not something fixable in the
HTML. They must be hosted on a real web address.
