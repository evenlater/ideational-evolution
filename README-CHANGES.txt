Files to drop into c:\dev\ideational-evolution, overwriting the existing
copies at these same relative paths:

  layouts/index.html                    (homepage: six-box shuffle grid)
  layouts/_default/section.html         (Archive: real 6-per-page pagination)
  layouts/partials/post-card.html       (new — shared card used by both)
  layouts/partials/site-pagination.html (new — pager used by Archive)
  static/css/main.css                   (adds hover-image + button + pager CSS
                                          to the end; nothing removed)

What changed, in brief:
- .post-card now shows a background photo on hover (via heroimage.html's
  existing image-resolution logic) with a dark scrim, dimming the text
  rather than replacing it. Cards with no resolvable image keep the old
  plain hover.
- Homepage's old full-image .post-stack section is replaced by a
  post-card grid identical in style to Archive, pulling the most recent
  24 posts (change $homeCount in index.html to adjust), chunked into
  batches of 6. A "More essays" button cycles forward through batches,
  wrapping to the start. No page reload.
- The old .stack-card CSS is left untouched in main.css but is no
  longer referenced anywhere -- safe to delete later if you want to
  clean it up.
- Archive (/posts, layouts/_default/section.html) now calls
  .Paginate ... 6 and uses the same post-card partial, so it grows in
  pages of six as new posts are added, exactly like the homepage grid.
  Pagination controls use a windowed pager (current +/- 2, first/last,
  ellipses) styled to match the site's condensed/letter-spaced look.

Nothing else in the repo was touched.
