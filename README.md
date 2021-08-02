# OctoPrint-ISY

Connects OctoPrint events to ISY.

## Setup

Install via the bundled [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager)
or manually using this URL:

    https://github.com/trv-in-3d/OctoPrint-ISY/archive/main.zip

This is highly based on the IFTTT plugin by tjjfvi  [https://github.com/tjjfvi/OctoPrint-IFTTT]
This is my first attempt at Python, Octoprint plug-in development & git all rolled into one.  I modified the plugin to make calls to Universal Devices ISY web platform to support anyone using a ISY-994 for home automation.

## Configuration

COMING SOON

### Makerkeys
A unique API key for ISY.


### Default prefixes
Default prefixes for the triggers. If you have an event `MyEvent` and prefixes `prefix1-` and `prefix2-`, it will, by default make the triggers `prefix1-MyEvent` and `prefix2-MyEvent`. Seperate the prefixes with newlines.

### Events
Define events to send to ISY.

#### Triggers
A list of triggers to trigger on ISY.

#### Values
ISY Webhooks allows for a payload with three values. It will interpret this string like so:
1. If the value begins with a dot (`.`), it will use that prop of the event payload (e.g. `.name` for `PrintDone`)
1. If it begins with an at symbol (`@`):
   1. `path` will be the result of interpreting the string with the first two characters removed as a value
   1. If the second character in the value is an `f` it will prepend to `path` the base uploads folder
   1. Otherwise, the second character should be a dash (`-`)
   1. It will then upload the file at `path` to [file.io](https://file.io) and return a link to that file.
1. If it begins with a colon (`:`), it will use the string after the colon
1. If it begins with a dollar sign (`$`), it will:
   1. If the second character is a `t`:
      1. Let `time` be the result of interpreting the string with the first three characters removed as a value.
      1. If the third character is `:`, it will format `time` in `H:MM` format (e.g. `1:02`).
      1. If the third character is `$`, it will format `time` in `H:MM:SS` format (e.g. `1:02:34`)
      1. If the third character is `h`, it will format `time` in Hh` format (e.g. `1h`)
      1. If the third character is `m`, it will format `time` in `Hh Mm` format (e.g. `1h 2m`)
      1. If the third character is `s`, it will format `time` in `Hh Mm Ss` format (e.g. `1h 2m 34s`)
1. Otherwise, it will just send the plain text

