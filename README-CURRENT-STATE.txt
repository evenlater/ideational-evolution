THIS ZIP SUPERSEDES EVERY OTHER ZIP I'VE SENT IN THIS CONVERSATION.

THREE THINGS IN THIS ROUND:

1. MARGARET IMAGE -- RE-SENDING single.html + main.css. Your test
   confirmed the frontmatter (imageFit: "contain") was correct and my
   template logic was correct when I rebuilt locally with your exact
   file -- so the most likely explanation is the imageFit zip from two
   rounds back never fully landed on the live site. This delivery has
   both files together again so there's no chance of a partial apply.

2. HOMEPAGE PAGINATION -- full rebuild, not a patch. Home now uses
   Hugo's real pagination on the exact same post list as /posts (same
   source, same 6-per-page), so page counts are structurally
   guaranteed to match -- not two systems that could drift, just one
   shared mechanism. 7 pages on both, confirmed. Real page-number
   links now render (reusing the same pager you already see on
   Archive), not just a "1/4" counter. The featured post no longer
   appears twice -- it's excluded from the grid wherever it would
   land, confirmed empty on every single paginated page, not just
   page 1.

   Caught a real bug while building this: Hugo's pagination only
   splits what's inside the paginated loop -- everything else in a
   template still re-renders identically on every /page/N/ URL. My
   first version had the hero section written above the .Paginate
   call, which meant the full hero (image, excerpt, everything) would
   have repeated on pages 2 through 7 too. Caught it by actually
   grepping every generated page for hero-title, not by assuming the
   restructure was clean. Fixed by moving .Paginate to the top and
   gating the whole hero block to page 1 only.

   Removed the old JS shuffle button/counter entirely (both the script
   and its CSS) since it's fully replaced now.

3. ABOUT LINK -- temporary fix as discussed: no /about page exists,
   so the nav link now jumps to the About blurb already living in the
   site-wide footer (id="about") instead of pointing at a page that
   was never built. Works from any page on the site, not just home,
   since that footer section is on every page already.

Build-tested clean, Hugo v0.161.1 extended, --buildDrafts, 53 pages,
19 total paginator pages across home/archive/tags.
