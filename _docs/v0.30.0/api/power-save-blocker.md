---
version: v0.30.0
category: API
title: 'Power Save Blocker'
source_url: 'https://github.com/electron/electron/blob/master/docs/api/power-save-blocker.md'
---

# power-save-blocker

The `power-save-blocker` module is used to block the system from entering
low-power(sleep) mode, allowing app to keep system and screen active.

An example is:

```javascript
var powerSaveBlocker = require('power-save-blocker');

var id = powerSaveBlocker.start('prevent-display-sleep');
console.log(powerSaveBlocker.isStarted(id));

powerSaveBlocker.stop(id);
```

## powerSaveBlocker.start(type)

* `type` String - Power save blocker type
  * `prevent-app-suspension` - Prevent the application from being suspended.
    Keeps system active, but allows screen to be turned off.  Example use cases:
    downloading a file, playing audio.
  * `prevent-display-sleep`- Prevent the display from going to sleep. Keeps system
    and screen active.  Example use case: playing video.

Starts the power save blocker preventing the system entering lower-power mode.
Returns an integer identified the power save blocker.

**Note:**
`prevent-display-sleep` has higher precedence level than `prevent-app-suspension`.
Only the highest precedence type takes effect. In other words, `prevent-display-sleep`
always take precedence over `prevent-app-suspension`.

For example, an API calling A requests for `prevent-app-suspension`, and
another calling B requests for `prevent-display-sleep`. `prevent-display-sleep`
will be used until B stops its request. After that, `prevent-app-suspension` is used.

## powerSaveBlocker.stop(id)

* `id` Integer - The power save blocker id returned by `powerSaveBlocker.start`.

Stops the specified power save blocker.

## powerSaveBlocker.isStarted(id)

* `id` Integer - The power save blocker id returned by `powerSaveBlocker.start`.

Returns whether the corresponding `powerSaveBlocker` starts.
