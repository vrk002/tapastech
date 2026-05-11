---
title: 'How to Create Your Own Blog from Scratch — A Beginner''s Guide'
description: 'A plain-English walkthrough of every component you need to launch a personal blog: domains, hosting, DNS, SSL, and more.'
pubDate: '2026-05-10'
heroImage: '../../assets/blog-hero.jpg'
---

You want a corner of the internet that is yours. A place to share what you know, document what you're building, and build a reputation over time. But the moment you Google "how to create a website," you're hit with words like DNS, CNAME, SSL, hosting, deployment — and it all feels overwhelming.

This guide explains every piece in plain English. By the end, you'll not only know *what* to do — you'll understand *why* each step exists.

---

## The Big Picture

Think of building a website like opening a physical store:

| Real World | Web World |
|---|---|
| Your store's street address | Your domain name (`tapastech.ink`) |
| The building where your store lives | Web hosting (Vercel) |
| The interior design & products | Your website code (Astro) |
| The phone directory listing | DNS records |
| Security lock on the door | SSL certificate (HTTPS) |

Every website on the internet needs all five of these things. Let's walk through each one.

---

## 1. The Domain Name — Your Address on the Internet

**What it is:** A domain name is the human-readable address people type to find your site. Instead of remembering `76.76.21.21`, they type `tapastech.ink`.

**What it does behind the scenes:**
Every device on the internet has a unique numeric address called an IP address (like `76.76.21.21`). Computers talk using these numbers. But humans are bad at memorizing numbers, so the Domain Name System (DNS) was invented — it's basically a giant phone book that converts `tapastech.ink` into `76.76.21.21`.

**Where to buy one:**
Domain registrars like Namecheap or Cloudflare let you "rent" a domain name (you pay yearly — you never truly own it permanently). Prices range from $2–$15/year depending on the extension (`.com`, `.ink`, `.dev`, etc.).

**What happens when you buy it:**
You get the right to control where that name points. You haven't built anything yet — you just own the address.

---

## 2. Web Hosting — Where Your Site Actually Lives

**What it is:** Hosting is a computer (server) that runs 24/7, stores your website's files, and serves them to anyone who visits your domain.

**What it does behind the scenes:**
When someone types `tapastech.ink` in their browser:
1. The browser asks the DNS system "where does tapastech.ink live?"
2. DNS returns the IP address of your hosting server
3. The browser connects to that server and says "give me the homepage"
4. The server sends back the HTML, CSS, and images
5. The browser renders it into the page the visitor sees

This entire exchange happens in under a second.

**Why Vercel specifically:**
Vercel is a modern hosting platform built for developers. Unlike traditional hosting (where your site lives on one computer in one location), Vercel deploys your site to a global network of servers (called a CDN — Content Delivery Network). When someone in India visits your site, they get the files from a server in India, not from a server in Virginia. This makes your site fast everywhere.

**Bonus:** Vercel has a generous free tier. For a personal blog, you'll likely never need to pay.

---

## 3. The Website Itself — What People Actually See

**What it is:** Your website is a collection of files — mostly HTML (structure), CSS (styling), and sometimes JavaScript (interactivity).

**What Astro is:**
Astro is a tool that helps you build websites more efficiently. Instead of writing raw HTML for every page, you write content in Markdown (a simple text format) and Astro converts it into proper HTML pages automatically. It also handles the blog structure, navigation, and styling.

**Static vs Dynamic:**
Astro generates *static* sites — meaning it builds all the HTML files once, upfront, and serves them as-is. There's no database being queried on every page load. This makes static sites extremely fast, cheap to host, and hard to hack.

**Behind the scenes workflow:**
1. You write a blog post in a `.md` file (plain text with formatting)
2. Astro reads all your content files and generates HTML pages
3. You push the code to GitHub
4. Vercel detects the change, rebuilds the site, and deploys automatically

---

## 4. GitHub — Your Code's Safe Home

**What it is:** GitHub is a platform that stores your code and tracks every change you make over time (called version control).

**Why you need it:**
- It's a backup of all your work
- Vercel connects to GitHub and automatically redeploys your site whenever you push new changes
- It's your public portfolio — other developers can see your work

**Behind the scenes:**
Git (the underlying technology) takes a "snapshot" of your code every time you commit. You can always go back to any previous version. When you push to GitHub, Vercel sees the new snapshot and automatically rebuilds and deploys your site within minutes.

**The workflow in practice:**
```
Write post → Save → git commit → git push → Vercel auto-deploys → Site is live
```

---

## 5. DNS Records — The Phone Book Entry

**What it is:** DNS records are instructions that tell the internet where to find your site.

**The two records you need:**

**A Record** — points your root domain to an IP address
```
tapastech.ink → 76.76.21.21 (Vercel's server)
```

**CNAME Record** — points a subdomain to another domain name
```
www.tapastech.ink → cname.vercel-dns.com (Vercel handles it from there)
```

**Why two records?**
`tapastech.ink` and `www.tapastech.ink` are technically different addresses. You need entries for both so that whether someone types the `www` or not, they land on your site.

**Why does it take time to propagate?**
DNS servers are distributed across the world. When you update a record, it takes time for that update to spread to all DNS servers globally — typically 10 minutes to 48 hours. This is called DNS propagation.

---

## 6. SSL — The Padlock in the Browser

**What it is:** SSL (Secure Sockets Layer) is what puts the `https://` in your URL and the padlock icon in the browser.

**What it does behind the scenes:**
SSL encrypts all data travelling between your visitor's browser and your server. Without it, someone on the same Wi-Fi network could read everything your visitors send and receive. With it, everything is scrambled and unreadable to anyone intercepting it.

**Why Vercel handles this for free:**
Vercel automatically generates an SSL certificate for your domain using a service called Let's Encrypt. You don't need to buy SSL separately.

---

## 7. Putting It All Together

Here's the complete journey when someone visits your site:

```
User types tapastech.ink
        ↓
Browser asks DNS: "where is tapastech.ink?"
        ↓
DNS returns Vercel's IP address
        ↓
Browser connects to Vercel's server (via HTTPS/SSL)
        ↓
Vercel serves the HTML files Astro generated
        ↓
Browser renders the page
        ↓
User reads your blog post
```

Total time: under 1 second.

---

## The Full Stack Summary

| Component | Tool | Cost | Purpose |
|---|---|---|---|
| Domain | Namecheap | ~$3/yr | Your address on the internet |
| Hosting + CDN | Vercel | Free | Serves your site globally |
| Site framework | Astro | Free | Converts markdown to HTML |
| Code storage | GitHub | Free | Version control + triggers deploys |
| DNS | Namecheap (managed) | Free | Routes domain to Vercel |
| SSL | Vercel (auto) | Free | Encrypts traffic, enables HTTPS |

**Total annual cost: ~$3/year** (just the domain).

---

## Your Action Plan

1. Buy a domain on Namecheap (~$3–12/yr)
2. Sign up for Vercel (free) and connect your GitHub account
3. Scaffold an Astro blog with `npm create astro@latest`
4. Push to GitHub
5. Deploy on Vercel with one click
6. Add your domain in Vercel settings
7. Update DNS records in Namecheap to point to Vercel
8. Wait 10–30 minutes for DNS propagation
9. Your site is live

---

## Final Thought

None of these technologies are complicated once you understand what problem each one solves. A domain solves the "how do people find me" problem. Hosting solves the "where do my files live" problem. DNS solves the "connecting the two" problem. SSL solves the "is this safe" problem.

You now understand how the internet works — at least the part that matters for running your own website.

---

*Written by Venu Kottapally — [tapastech.ink](https://tapastech.ink)*
