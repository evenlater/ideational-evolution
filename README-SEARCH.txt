COMPLETE SEARCH FEATURE BUNDLE -- every file search depends on, in one
place, since recent zips overwrote the one that had hugo.toml in it.

  hugo.toml                       <- THE LIKELY MISSING PIECE. Its
                                     [outputs] section must include
                                     'JSON' for home, or /index.json
                                     is never generated and search has
                                     no data to search. This was the
                                     only round in the whole project
                                     that ever changed this file, so
                                     it's easy to have missed.
  layouts/index.json              <- the index template (you have this)
  layouts/partials/nav.html       <- search button + panel markup
  layouts/partials/search.html    <- the search JS
  layouts/_default/baseof.html    <- includes the JS site-wide

Diagnostic: open https://ideationalevolution.com/index.json
  404          -> hugo.toml is the fix; copy it over and redeploy
  JSON content -> data is fine, tell Claude exactly what "doesn't
                  work" looks like (button dead vs. no results) and
                  whether the browser console shows any errors
