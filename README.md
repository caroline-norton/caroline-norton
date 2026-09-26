# understory website

A static 4-page website (Home, Services, About, Contact) built for GitHub
Pages: plain HTML + one shared `styles.css`, no framework, no build step.

The site was rebranded from an earlier "Grainline" placeholder concept to
**understory**, per `understory-brand-guidelines.md` in this folder: that
file is the source of truth for every colour, font, spacing and copy-voice
decision below. If the brand evolves further, that's the file to update
first.

## 1. Adding images

All images live in `/images/`. Every spot that still needs a photo shows a
dashed placeholder box naming the exact filename and suggested size it's
waiting for: see [`images/PLACEHOLDERS.md`](images/PLACEHOLDERS.md) for the
full list. The site's own duotone photography (see §7) is already wired in
and doesn't need anything from you.

To add an image:

1. Save your file into `/images/` using the **exact filename** shown on the
   placeholder box (e.g. `caroline.jpg`).
2. Open the relevant `.html` file, find the matching `<!-- [IMAGE: ...] -->`
   comment, and replace the `<div class="img-placeholder">...</div>` block
   immediately after it with a real `<img>` tag, for example:

   ```html
   <img src="images/caroline.jpg" alt="Caroline, founder of understory">
   ```

   Keep (or rewrite) the `alt` text so it still describes the image.
3. Save and refresh the page. That's it, no build step.

The `favicon.png` reference is already wired into every page's `<head>`; you
only need to drop the file in.

## 2. Replacing `[PLACEHOLDER: ...]` text

Search every `.html` file for the literal text `[PLACEHOLDER:` to find every
spot that still needs your input. As of this build, these are:

| File | What to replace |
|---|---|
| `index.html`, `services.html`, `about.html`, `contact.html` (footer, repeated on every page) | Email address, phone/WhatsApp number, location line (LinkedIn is filled in: [caroline-norton-2847018a](https://www.linkedin.com/in/caroline-norton-2847018a/)) |
| `contact.html` | Same three remaining details again in the "Direct details" box, plus the "come back to you within `[1–2 working days]`" turnaround time |
| `about.html` | Credentials paragraph (qualifications, memberships, notable experience), currently just a placeholder sentence |

Each placeholder is also wrapped in an amber `<span class="needs-text">` so
it's easy to spot visually in the browser, not just in the source.

## 3. Setting up Formspree (contact form)

The form in `contact.html` posts to Formspree, since GitHub Pages can't run
server-side code.

1. Go to [formspree.io](https://formspree.io) and create a free account.
2. Create a new form. Formspree gives you a form ID that looks like
   `xyzwabcd`.
3. Open `contact.html`, find this line near the top of the `<form>` tag:

   ```html
   <form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```

4. Replace `YOUR_FORM_ID` with your real ID and save.
5. Submit a test message once the site is live to confirm it arrives in your
   Formspree dashboard/email.

The form already includes a hidden honeypot field (`_gotcha`) for spam
protection and a `_subject` field, both recommended by Formspree. The
"I'm enquiring about" dropdown offers Root, Canopy, Union, and Not sure yet,
matching the three service lines.

## 4. Deploying to GitHub Pages

1. Create a new GitHub repository named exactly `USERNAME.github.io`
   (replace `USERNAME` with your GitHub username).
2. Upload every file in this folder to the repo: drag-and-drop through the
   GitHub website works fine, or use `git push` if you're comfortable with
   the command line. Make sure `.nojekyll` (an empty file) comes along; it
   won't show up unless "show hidden files" is on in your file browser.
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to "Deploy from a branch",
   branch `main`, folder `/ (root)`.
5. Save. GitHub gives you a URL like `https://USERNAME.github.io`; it can
   take a minute or two to go live after the first deploy.

## 5. Connecting a custom domain

1. Open the `CNAME` file in this repo and replace its placeholder line with
   your real domain (just the domain, e.g. `understory.co.za`, no
   `https://`).
2. At your domain registrar, add the DNS records GitHub documents for
   custom domains:
   - For an apex domain (`understory.co.za`): four `A` records pointing at
     GitHub's IP addresses (listed in GitHub's
     [custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)).
   - For a `www` subdomain: a `CNAME` record pointing at
     `USERNAME.github.io`.
3. Back in **Settings → Pages**, enter the same domain in the "Custom
   domain" field and save.
4. Once DNS has propagated (can take up to 24 hours) and GitHub verifies it,
   tick **"Enforce HTTPS"**.
5. **Update the domain everywhere else it's hard-coded as a placeholder**:
   `robots.txt`, `sitemap.xml`, and the `<link rel="canonical">` plus
   `og:url`/`og:image`/`twitter:image` meta tags at the top of all four
   `.html` files all currently say `YOURDOMAIN.co.za`. Find-and-replace that
   string with your real domain across the whole folder.

## 6. Editing text later

Every page is plain HTML: open the `.html` file in any text editor, find
the text, change it, save, and re-upload (or `git push`) the file. There's
no build step, so the change is live as soon as GitHub Pages redeploys
(usually under a minute).

**Voice reminders from the brand guide**, worth keeping in mind if you add
copy yourself: sentence case in headlines (not Title Case), short
declaratives, one forest reference per section maximum, and the
mycorrhizal-network / crown-shyness biology is explained exactly once, on
the About page, never re-explained or referenced as jargon in a headline
or button.

## 7. Design notes: brand system & photo treatment

Every token below (colour, type, spacing, shape) is copied directly from
`understory-brand-guidelines.md` §4 and §8, or added at your request (teal):

| Token | Value | Used for |
|---|---|---|
| `--color-ink` | `#1B1A17` | Primary text |
| `--color-paper` | `#F6F4EF` | Primary background |
| `--color-accent` (amber) | `#C17F3A` | Links, underlines, service-label chips, icons; never small body text (fails AA on paper, see guide §4.2/§6) |
| `--color-teal` | `#2F6B67` | Secondary accent; unlike amber, this one passes AA for body text on paper (roughly 5.5:1), so it's safe for links/small text too |
| `--color-teal-dark` | `#1F4A47` | Teal hover/active state |
| `--color-teal-deep` | `#142523` | Dark section backgrounds (the "who this is for" band and the footer), replacing plain ink with a teal cast |
| `--color-teal-light` | `#C9E4E0` | Pale teal photo highlight tone (used in the homepage hero photo's duotone) |
| `--color-teal-tint` | `#E2EFED` | Very pale teal wash, the background of the homepage "What we do" band |
| `--color-line` | `#DAD5C9` | Hairline borders |
| `--color-muted` | `#8B8577` | Secondary/caption text |

Fonts: **Fraunces** (display/headings) and **Inter** (body, plus the
service-label/eyebrow accent), both Google Fonts, loaded per the guide's
`<link>` snippet. The brand guide's original spec called for a third font,
IBM Plex Mono, set in uppercase for the `Root`/`Canopy`/`Union` labels and
section eyebrows (a "specimen label" look). At your request this was
swapped to bold, uppercase **Inter** instead (`--font-label` in
`styles.css`), so the site now loads two font families instead of three.
Shape language is sharp/flat: 2 to 4px radii, hairline borders, no drop
shadows, no rounded bubbly buttons.

**Photography, a deliberate compromise, worth understanding:** the brand
guide explicitly says *"no literal photography of forests, trees, or
nature-lifestyle stock imagery"* and recommends abstract single-colour
line-work instead. You asked to use your own photos from
`images/forest-theme/` for a foresty feel: a direct conflict with that
rule. The resolution agreed on: five photos (`hero-canopy.jpg`,
`about-biology.jpg`, `service-root.jpg`, `service-canopy.jpg`,
`service-union.jpg`) are run through a duotone treatment in the brand's
ink/paper/amber/teal palette. That keeps them off the "lifestyle stock
photo" register the guide warns about and closer to the "botanical/
scientific illustration" the guide asks for instead, while still being
your real photographs.

**How the cropping actually works (this changed after the first pass
looked stretched):** each source photo is resized to a sensible size while
keeping its own native aspect ratio, with no pre-cropping at all. The
`<img>` tags then carry a `.photo-crop` class (defined in `styles.css`)
that sets a fixed display box plus `object-fit: cover`. The browser does
the cropping at render time, zooming into the centre of whichever photo it
is, and `object-fit: cover` can never stretch an image, it only crops. If
a particular photo's default centre crop isn't framing the right thing
once you look at it, add `object-position` to that specific `<img>` (e.g.
`object-position: top` or `object-position: 30% 60%`) rather than
re-cropping the source file.

The display box shape comes from a ratio class: `.ratio-4-3` (the About
page photo), or `.ratio-7-2` (a wide 3.5:1 banner, used for the homepage
hero and all three Root/Canopy/Union photos on the Services page). Add
`.size-half` to cap an image at roughly half the content width instead of
full width (used on the hero and the Union photo). To change any photo's
shape later, it's just a class swap on that one `<img>`, no image
regeneration needed.

The original untouched files stay in `images/forest-theme/` if you want to
reprocess them differently; regenerate the duotone versions with:

```python
from PIL import Image, ImageOps, ImageEnhance
im = ImageOps.exif_transpose(Image.open("source.jpg"))
im.thumbnail((1400, 1400))  # keeps native ratio, just caps the size
gray = ImageOps.grayscale(im)
gray = ImageEnhance.Contrast(gray).enhance(1.15)
ImageOps.colorize(gray, black="#1B1A17", white="#F6F4EF").save("output.jpg")
```

If you'd rather follow the guide to the letter, the cleanest fix is to swap
these `<img>` tags for actual line-work SVGs (root-system or
branching-network diagrams in `--color-accent` on `--color-paper`), the
guide's stated first choice.

## 8. Service-line content mapping (Root / Canopy / Union)

The brand architecture requires exactly three service lines, always shown
together in that order, and forbids inventing a fourth. The site's older
"Small Businesses" / "Individuals" split had to be remapped onto that
structure; here's exactly how, so you can sanity-check it:

| Old content | New home | Why |
|---|---|---|
| HR foundations, development plans, succession planning, HR management systems | **Root** (`services.html#root`) | "Long-term, mostly invisible structural work": matches the guide's own description almost exactly |
| Career guidance & coaching (impartial sounding board, difficult conversations, exploring options) | **Canopy** (`services.html#canopy`) | Reframed as deciding "who gets space to grow": the guide's own phrase for what Canopy governs |
| CV optimisation + interview preparation (candidate side) | **Union** (`services.html#union`) | "Matching people to roles," candidate half |
| "Refine your recruitment/interview skills" (was a Small-Business bullet) | **Union**, "For hiring teams" card | Union is explicitly defined as serving *both* hirer and hiree; this bullet is the hirer half, moved here rather than left in Root |

Nothing was deleted: every real sentence from the old build is still on the
site, just regrouped under the service line it actually belongs to. Note
that this service line was originally named "Splice" and was renamed to
"Union" at your request; `understory-brand-guidelines.md` has been updated
to match, with a note recording the rename.

## 9. On-page SEO (targeting searches like "HR consulting South Africa")

What's already wired in, all achievable from static files:

- **Per-page titles and meta descriptions** naturally include "South
  Africa" plus the relevant service term (HR consulting, people strategy,
  career coaching, CV optimisation) without keyword-stuffing.
- **`<html lang="en-ZA">`** on every page: the correct locale signal for
  South African English, and it reinforces the British/SA spelling used
  throughout.
- **`robots.txt`** and **`sitemap.xml`** at the repo root, so search
  engines can find and crawl all four pages. Both currently point at the
  `YOURDOMAIN.co.za` placeholder; update them per §5 above.
- **JSON-LD structured data** (`ProfessionalService` schema) on
  `index.html`, describing understory, its service area (South Africa),
  its site URL, and `sameAs` (the real LinkedIn profile). It deliberately
  leaves out `address` and `telephone` rather than invent them; add those
  two fields once the real details replace the footer's
  `[PLACEHOLDER: ...]` text.
- **Open Graph and Twitter Card meta tags** on every page, so links shared
  on social media or WhatsApp show a proper title, description, and
  preview image. The preview image (`images/og-cover.jpg`) is a new
  placeholder, listed in `images/PLACEHOLDERS.md`, that still needs a real
  file (1200×630px).
- **`<link rel="canonical">`** on every page, so search engines treat one
  URL per page as authoritative.
- Heading hierarchy (one `<h1>` per page), descriptive alt text, and
  internal linking were already solid from the previous build pass;
  nothing new was needed there.

**What this can't do on its own:** on-page SEO is necessary but not
sufficient. The single highest-leverage thing outside this repo, for a
local-intent search like "HR consulting South Africa," is a **Google
Business Profile listing** (needs the real address and phone number,
which are still placeholders here). Real, filled-in credentials on the
About page, a LinkedIn company page, and any backlinks from directories or
past clients all matter more than meta tags once the basics above are in
place. A brand-new domain also simply takes time to rank regardless of how
well it's optimised; don't expect overnight results.

## Acceptance checklist

- [x] Four pages build and link to each other with relative links.
- [x] Design implements the brand guide's tokens exactly (colour, type,
      spacing, shape), plus the requested teal addition; see §7 above.
- [x] Fully responsive; nav collapses into a hamburger under ~720px.
- [x] Root / Canopy / Union always appear together, in that order, styled
      as a distinct set (mono, uppercase, amber underline).
- [x] The mycorrhizal/crown-shyness biology appears exactly once, in plain
      language, on the About page, not referenced elsewhere.
- [x] All six client testimonials preserved verbatim on the About page.
- [x] Every image spot without a real photo yet has a labelled placeholder
      box + alt text guidance.
- [x] Contact form wired to Formspree with a placeholder ID + honeypot.
- [x] `.nojekyll`, `CNAME` (placeholder), favicon reference, and this
      README are present.
- [x] Semantic HTML with a single `<h1>` per page, labelled form fields,
      and keyboard-reachable nav.
- [x] No em dashes in this project's own content (HTML, CSS, this README).
- [x] British English spelling throughout (already correct before this
      pass; verified, not changed).
- [x] On-page SEO: titles, descriptions, structured data, Open Graph tags,
      canonical links, `robots.txt`, `sitemap.xml`; see §9 above.

**One open conflict, flagged rather than silently resolved:** using your
forest photos at all sits against the brand guide's explicit "no literal
nature photography" rule. See §7 above for the stylistic compromise and how
to swap in pure line-art instead if you'd rather follow the guide exactly.

Everything else on the checklist was completed. The remaining open items
are the ones only you can fill in: your Formspree ID, contact details, the
credentials paragraph, Caroline's headshot, the `og-cover.jpg` share image,
and (for full SEO benefit) your real domain and a Google Business Profile.
#   c a r o l i n e - n o r t o n  
 