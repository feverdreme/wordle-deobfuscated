# Partially Deobfuscated World Source Code

## Findings:
- this was most likely written in es6, which was then targetted to es5, shown through the lack of `const`, `let`, and `class` keywords
- `window.hash` is a hash to verify that hte javascript bundle the correct version, and is probably used in case Cache-Control goes wonky or anything, however I cannot determine where the validation logic is
- the wordle evalutation function for a row is not a function in the globaL scope, but is defined by manually adding a string key to an object and then assigned with an anon func
- `e` is usually an object
- `a` is usually an object property name
- `window.localStorage.gameState` and `window.localStorage.statistics` are where the info is stored for sols, current board states, progress, streaks, etc.
- 864e5 is the number of millisconds in a day
- the ordering of the answers is predetermined, and I renamed the variable to `possibleAnswers`
- it calcualtes it by subtracting `new Date()` (which is today) from a constant (probably when wordle was first deployed or created)
    - im leaving out details, like how it standardizes the dates to `setHour(0,0,0,0)`
- it then uses that to get the index for today's solution
- it's a progressive web app, although chrome can't recognize it, but the iPhone can
    - this is actually really interesting, because since it's deterministc entirely, it has a really easy way of doing offline caching as per the PWA reqiurements, and the only thing it really needs is today's date, which can be retrieve from a syscall for systemtime when there's no network connection
    - it's basically a mobile game so it makes sense to have PWA functionality
- there is a custom `game-app` element created with the customElement API
- `!0`, `!1`, `void 0`, i mean, come on