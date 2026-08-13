Files to drop into c:\dev\ideational-evolution, overwriting the existing
copies at these same relative paths. This is the FULL cumulative set from
this thread -- safe to drop in wholesale even if you're not sure exactly
which files changed since your last update.

  layouts/index.html                    homepage: six-box shuffle grid
                                         (includes a fix for a real bug in
                                         the batching logic -- Hugo's append
                                         flattens slices instead of nesting
                                         them, which would have broken as
                                         soon as more than 6 posts existed)
  layouts/_default/baseof.html          includes card-hover.html site-wide
  layouts/_default/section.html         Archive: real 6-per-page pagination
  layouts/_default/single.html          NEW FIX: <h1> now runs through
                                         markdownify, so *Julian*-style
                                         markdown in a title actually
                                         becomes gold italic <em> instead
                                         of showing literal asterisks
  layouts/partials/post-card.html       NEW FIX: title also markdownified;
                                         excerpt paragraph is now omitted
                                         entirely when there's no subtitle
                                         instead of falling back to the
                                         full auto-Summary (which was
                                         stretching cards into rectangles)
  layouts/partials/site-pagination.html pager used by Archive
  layouts/partials/card-hover.html      touch tap-to-preview script
  static/css/main.css                   cumulative: hover-image CSS,
                                         gap+background gridlines (no longer
                                         dependent on card count being a
                                         multiple of 3), shuffle/pager
                                         styling, NEW: gold-italic em rule
                                         for .single-post h1 and .post-card
                                         h4 (this literally did not exist
                                         anywhere before except the site's
                                         logo -- that's why Julian never
                                         went gold), NEW: aspect-ratio: 1/1
                                         + flex layout + title line-clamp
                                         so cards stay square regardless of
                                         content length, NEW: real ## Markdown
                                         headers now get the site's actual
                                         h2 styling, NEW: mobile reading
                                         column widened -- less side padding,
                                         larger base font, more line-height

Real Hugo v0.161.1 build tested clean against your actual repo, including
--buildDrafts, before this was packaged.

Content: 2026-03-29-gore-vidal-julian-self-portrait.md is a genuinely new
converted post (Gore Vidal / "Julian") -- ready to review, still draft: true.
Two other pilot posts from earlier in this thread turned out to be
duplicates of posts Darryl had already converted himself (the Disraeli
myth review and the Wilson/Pound/Joyce piece) and are NOT included here to
avoid overwriting his already-finished, better versions (which have
subtitles, hero images, and populated sources that my blind scrape
couldn't have known about).

Nothing else in the repo was touched.
