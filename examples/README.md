Put layout XMLs here, with filename:
`[package name] [tags] [comments].xml`

Package name is eg `com.google.android.youtube`

Tags (include at least one) are:
* `unskippable-ad` an ad is playing and not *currently* skippable
  * `ad-countdown-to-skip` a countdown timer to when the ad will be skippable is currently being displayed
* `skippable-ad` an ad is playing and *currently* skippable
  * `rewarded-ad` an ad is playing that, if allowed to finish, will reward the user in some way (e.g. in game currency) and therefore should not be fully closed automatically
* `ad-panel` a closeable non-video ad panel is being displayed (e.g. app info & install links on YouTube; upgrade offers in YouTube Music)
* `no-ad` no muteable, closeable, or eventually skippable ad is being displayed (i.e. nothing to act on)
  * `ignore-ad` an ad is being displayed, but it isn't actionable so should be ignored 

Comments are notes about what's being shown, e.g. `subscriptions page`
