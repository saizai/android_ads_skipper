Put layout XMLs here, with filename:
`[package name] [tags] [comments].xml`

Package name is eg `com.google.android.youtube`

Tags (include all that apply, so at least one) are:
* `unskippable-ad` an ad is playing and not *currently* skippable
  * `ad-countdown-to-skip` a countdown timer to when the ad will be skippable is currently being displayed
* `skippable-ad` an ad is playing and *currently* skippable
* `ad-panel` a closeable non-video ad panel is being displayed (e.g. app info & install links on YouTube; upgrade offers in YouTube Music)
* `rewarded-ad` an ad is playing that, if allowed to finish, will reward the user in some way (e.g. in game currency) and therefore should not be fully closed automatically
* `no-ad` no exclusively-muteable, closeable, or eventually skippable ad is being displayed (i.e. nothing to act on)
  * `ignore-ad` an ad is being displayed, but it isn't actionable so should be ignored; includes e.g. ads playing concurrently with game music that shouldn't be muted, ads that aren't closeable or skippable and don't play sound (e.g. banner and subscription feed ads), etc.

Comments are notes about what's being shown, e.g. `subscriptions page`
