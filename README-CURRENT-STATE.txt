THIS ZIP SUPERSEDES EVERY OTHER ZIP I'VE SENT IN THIS CONVERSATION.

ONE FILE CHANGED: static/css/main.css. One line.

THE ACTUAL BUG, finally measured rather than guessed: your two
screenshots let me compare directly -- septimus's text column uses
~88% of the phone screen's width; Darryl's was using only ~64%. Same
font sizes, wildly different line lengths. The cause: article pages
nest .single-post INSIDE .container, and last round's homepage fix
(adding 2rem mobile padding to .container) silently STACKED on top of
.single-post's own 2rem -- 64px per side, 128px total eaten from a
~390px screen. My earlier fix for one page broke the other page,
because they share a wrapper I wasn't accounting for.

FIX: .single-post's mobile side padding is now 0; .container alone
provides the full 32px each side. Text column is now ~84% of screen
width at phone size, closely matching the septimus reference (~88%).
Expect roughly 8-9 words per line instead of 5-6 -- a real difference
across a 4,000-word essay.

Desktop is untouched (its generous nesting has always looked right
and was never the complaint).

Build-tested clean, Hugo v0.161.1 extended, --buildDrafts, 53 pages.
