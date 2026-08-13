Files to drop into c:\dev\ideational-evolution, overwriting the existing
copies at these same relative paths:

  layouts/index.html                    (homepage: six-box shuffle grid)
  layouts/_default/baseof.html          (adds one include line for the
                                          new card-hover.html partial)
  layouts/_default/section.html         (Archive: real 6-per-page pagination)
  layouts/partials/post-card.html       (shared square card)
  layouts/partials/site-pagination.html (pager used by Archive)
  layouts/partials/card-hover.html      (NEW -- touch tap-to-preview script)
  static/css/main.css                   (hover-image CSS, gridline fix,
                                          shuffle/pager styling)

Real Hugo v0.161.1 build tested clean against your actual repo (0 errors)
before this was packaged.

Fixes in this round, from the iPhone screenshot:

1. Image preview didn't work on iPhone -- CSS :hover doesn't exist on
   touch devices at all, so tapping a card never triggered it; what you
   saw (Woodrow flashing, or appearing under the text-selection menu)
   was iOS incidentally faking a hover state during navigation/long-press,
   not the feature working. Fixed with layouts/partials/card-hover.html:
   on devices with a real mouse/trackpad, CSS :hover still handles it
   exactly as before. On touch devices, a small script makes the FIRST
   tap on an image card reveal the photo (adds an .is-peek class) and
   PREVENTS navigation; a second tap follows the link normally. This
   partial is included once, site-wide, via baseof.html, so it covers
   both the homepage and Archive automatically.

2. Missing gridlines on every platform -- this was a real pre-existing
   bug, not something new. The old CSS removed borders with
   :nth-child(3n) / :nth-last-child(-n+3), which only computes correctly
   when the total card count on a page is an exact multiple of 3. Your
   live repo currently has 4 posts (not a multiple of 3), so the math
   silently stripped borders in the wrong places everywhere -- and it
   would keep doing that on any page/batch that doesn't land on a clean
   multiple of 3, which is most of them once pagination is in play.
   Replaced with a technique that doesn't depend on counting: .post-grid
   gets gap: 1px + a background color, and each .post-card gets its own
   solid background, so the 1px gaps read as gridlines automatically,
   for any number of cards, on any screen width.

Everything from the previous round (homepage six-box shuffle via manual
seq/first/after batching, Archive's real .Paginate 6, the windowed
pager partial) is unchanged.

Nothing else in the repo was touched.
