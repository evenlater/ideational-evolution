THIS ZIP SUPERSEDES EVERY OTHER ZIP I'VE SENT IN THIS CONVERSATION.

NEW FEATURE: imagePosition frontmatter field. Set it on any post:

  imagePosition: top

Valid values: any CSS object-position keyword -- top, bottom, left,
right, center (the default when omitted), or combinations like
"top left". Controls where a cover-cropped image is anchored when it
doesn't fit its frame's aspect ratio, so a photo needing its top
visible (a face near the top of a tall image, say) isn't center-cropped
awkwardly.

WIRED UP IN ALL FIVE PLACES an image can appear, not just one:
  1. Homepage six-box grid cards (and Archive, and tag pages -- they
     all share the same post-card.html partial)
  2. Homepage hero (the featured/latest post)
  3. The article's own hero banner at the top of its page
  4. Prev/next navigation preview thumbnails (both directions --
     these show the ADJACENT post's image and imagePosition, not the
     current page's, so I made sure to capture that context correctly
     rather than accidentally reading the wrong post's setting)

CAUGHT AND FIXED WHILE BUILDING: two of these (the homepage hero and
the nav-preview thumbnails) live in top-level page templates, not
partials -- in Hugo, the $ variable means something different there
(the current page being rendered) than it does inside a partial
(whatever context was passed in). Naively writing $.Params.imagePosition
in those spots would have silently read the WRONG page's setting.
Caught this before shipping by explicitly capturing each post's
context in its own variable ($post, $prev, $next) rather than relying
on $.

VERIFIED END TO END, not just in the template code: temporarily added
imagePosition: top to a real live post (Disraeli myth) and rebuilt,
confirming the actual generated HTML across all five spots correctly
showed object-position:top / background-position:top -- then reverted
that post back to its original content, confirmed zero trace of the
test left behind.

Defaults to center everywhere when the field is omitted, so nothing
changes for any existing post until Darryl actually sets it on the
one that needs it.

Build-tested clean, Hugo v0.161.1 extended, --buildDrafts, 53 pages.
