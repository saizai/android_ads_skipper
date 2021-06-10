# Ad examples

## Layout XML files

Put layout XMLs here, with filename:
`[package name] [tags] [- description].xml`

### Package name

The Android package name, eg `com.google.android.youtube`.

### Tags

Include all of the following that apply, in the order below, space delimited:

* `no-ad` no ad at all is being displayed
* *there's at least one ad displayed*
  * `ad-1` *etc.* number each displayed ad separately
  * *what can we do about it?*
    * `actionable` we can *currently* take some action (mute, skip, close, etc)
      * `collapsible` a closeable or minimizable non-video ad panel is being displayed (e.g. app info & install links on YouTube; upgrade offers in YouTube Music; subscription offers on apps & websites; etc)
      * `skippable` an ad is playing and skippable
    * `later-actionable` there's something we can't do now, but can later
      * `later-skippable` will be skippable later
        * `countdown` a countdown timer to when the ad will be skippable is currently being displayed
    * `unactionable` an ad is being displayed, but there's nothing we can do about it, and won't be if we wait (i.e. we should ignore it)
      * `never-actionable` it's not possible to do anything about it
      * *already did as much as we could*
        * `collapsed` an ad is being displayed, but it's already been collapsed as much as possible
  * *sound* the ad's sound is:
    * `silent` inherently silent, so system audio doesn't need to be muted
    * `muted` muted *within the app*, so system audio doesn't need to be muted
    * `mutable` playing sound, and ad sound is mutable *within the app* (by clicking something), so we should either do that or mute system also
     * `unmutable` playing only ad sound, and the ad sound is not mutable within the app, so we should mute the system
      * `parallel-sound` ad is playing sound, but (within the same app) in parallel with sound the user may want (eg gameplay), so we shouldn't mute system
  * `rewarded` if allowed to finish, the ad will reward the user in some way (e.g. in-game currency) and therefore should not be fully closed automatically

### Description

If description is present, put ` - ` between tags and description.

Optional notes about what's being shown, e.g. `subscriptions page`.

* If the app is a web browser, include the domain first, e.g. `www.nytimes.com article`.

---

## Targeting criteria

### Filename

[raw_criteria.json] (as opposed to [../combined_criteria.json], which merges everything in this into final criteria, which then gets converted into optimized XPath strings for the client)

### Standardization 

* Unix line endings (LF `\n` only, not CRLF `\r\n`)
* UTF-8 encoded
* String keys
* Strings delimited by `"`
* 2 space indents

### Contents

A hash of:
* `file` **string** the example XML file name
* `package` **string** the package name, as above
* `domain` **string** *(optional)* the domain name (if this is from a browser), as above
* `description` **string** *(optional)* overall context of this layout, as above
* `elements` **array of hashes** for each ad, and each non-ad source of sound (i.e. desired audio/video content), in this layout. Keys:
  * `tags` **array of strings** as above
  * `description` **string** *(optional)* description of this ad 
  * `actions` **hash** what to do if this is found. Keys:
     * `click` **bool** *(optional)* click this element. Set to false if it would trigger an ad.
     * `mute` **bool** *(optional)* mute system volume. Set to false if detecting this element means we should *unmute* (or override another indication to mute), e.g. because it indicates that desirable sound is playing. Don't set this key either way if it's e.g. a silent ad, since a different, non-silent ad might also be playing.
     * `watch` **bool** *(optional)* start actively watching for changes (e.g. for countdown timers)
     * `ignore` **bool** *(optional)* ensure that the compiled targeting criteria *don't* include this, because it's a potential false positive
     * `ignore_as_reward` **bool** *(optional)* don't automatically click if this element because clicking it would stop the user from getting a reward. Usually in game reward ads have two steps to close. `mute` the video ad itself, and `click` the first step ad close, but `click` *and* `ignore_as_reward` the confirmation warning that they'll lose the reward for watching the ad. This ensures that the ad is as close to closed as possible without losing the reward no matter what (to minimize user annoyance), and the user can set a preference on whether they want it to automatically be fully closed or not. 
  * `xml` **hash** this ad's element from the XML. Keys:
     * `class` **string** the element class (from immediately after the opening `<` until the next space), e.g. `android.widget.Button`
     * `id` **string** *(optional)* the `android:id`
     * `text` **string** *(optional)* the `android:text`
     * `contentDescription` **string** *(optional)* the `android:contentDescription`
     * `clickable` **bool** *(optional)* `android:clickable`
     * `enabled` **bool** *(optional)* `android:enabled`
   * `parent_xml` same, for the parent element
   * `target` **hash of `/^…$/` regexes** targeting criteria to be used in the ad blocker. Usually just one of `class`, `id`, or `text` keys, but can be multiple. Keys are same as for `xml`. Should almost always include `enabled` for everything and `clickable` if the `action` is `click`. E.g. `("clickable": true, "text": /^Subscribe for.*offer.collapse the message$/)`.
 
