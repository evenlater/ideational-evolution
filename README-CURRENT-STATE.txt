THIS ZIP SUPERSEDES EVERY OTHER ZIP I'VE SENT IN THIS CONVERSATION.

NEW FEATURE: imageFit: contain frontmatter field. Fixes exactly the
Margaret problem -- a portrait image that shouldn't be cropped to the
standard 1200x630 banner shape. Set it on that one post's frontmatter
alongside imagePosition:

  image: "/img/big-marge.png"    <- whatever the file is actually
                                    named now; point this at it
                                    directly instead of relying on
                                    filename auto-detection
  imageFit: contain

WHAT THIS FIXES ABOUT YOUR WORKAROUND: renaming the file broke
heroimage.html's auto-detection (it guesses filenames from the post's
slug, so "big-marge.png" no longer matched "analyzing-margaret" and
every thumbnail silently found nothing). The `image:` field bypasses
that guessing entirely and points straight at the real file -- no
rename needed at all, actually; you could revert the filename back to
analyzing-margaret.png and it would still auto-detect fine without
even needing the image: field. Either way works now.

imageFit: contain affects ONLY the article's own large hero banner --
thumbnails everywhere else (homepage grid, homepage hero, prev/next
nav previews) stay properly cropped as normal small crops, which is
correct regardless of the source image's orientation. Verified this
distinction directly: temporarily set imageFit: contain on the real
Margaret post, confirmed the banner shows the full portrait
(letterboxed, capped at 75vh so it doesn't dominate the page) while an
adjacent post's nav-preview thumbnail of that same image still renders
as a normal cropped thumbnail -- then reverted the test post to
original.

CLEANUP FOR YOU TO DO: remove the manual <img src> tag you added
directly in the post body -- it's redundant now that the hero banner
handles this properly through the template.

Build-tested clean, Hugo v0.161.1 extended, --buildDrafts, 53 pages.
