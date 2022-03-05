# Mopidy-Spotify

[![Latest PyPI version](https://img.shields.io/pypi/v/Mopidy-Spotify)](https://pypi.org/project/Mopidy-Spotify/)
[![CI build status](https://img.shields.io/github/workflow/status/mopidy/mopidy-spotify/CI)](https://github.com/mopidy/mopidy-spotify/actions)
[![Test coverage](https://img.shields.io/codecov/c/gh/mopidy/mopidy-spotify)](https://codecov.io/gh/mopidy/mopidy-spotify)

[Mopidy](https://mopidy.com/) extension for playing music from [Spotify](https://www.spotify.com/).

## Status

Mopidy-Spotify is dependent on [`pyspotify`](https://pyspotify.readthedocs.io/en/latest/), a wrapper for Spotify's `libspotify` C library.
`libspotify` was [deprecated in 2015](https://github.com/mopidy/mopidy-spotify/issues/110) with no replacement.
It is unmaintained, functionally limited, and also now unavailable from the [Spotify developer site](https://developer.spotify.com/technologies/).
Where possible, we are [moving to use Spotify's Web API](https://github.com/mopidy/mopidy-spotify/issues/114) instead.
However, native playback is still only possible using `libspotify` and there is no official way for us to provide some Spotify features.

Limitations and/or bugs in `libspotify` currently result in missing/broken Mopidy-Spotify support for the following:

- Saving items to My Music ([#108](https://github.com/mopidy/mopidy-spotify/issues/108)) - possible via web API
- Podcasts ([#201](https://github.com/mopidy/mopidy-spotify/issues/201)) - unavailable
- Radio ([#9](https://github.com/mopidy/mopidy-spotify/issues/9)) - unavailable
- Spotify Connect ([#14](https://github.com/mopidy/mopidy-spotify/issues/14)) - unavailable

Working support for the following features is currently available:

- Playback
- Search
- Playlists (read-only)
- Top lists and Your Music (read-only)
- Lookup by URI

## Dependencies

- A Spotify Premium subscription. Mopidy-Spotify **will not** work with Spotify
  Free, just Spotify Premium.

- A non-Facebook Spotify username and password. If you created your account
  through Facebook you'll need to create a "device password" to be able to use
  Mopidy-Spotify. Go to http://www.spotify.com/account/set-device-password/,
  login with your Facebook account, and follow the instructions. However,
  sometimes that process can fail for users with Facebook logins, in which case
  you can create an app-specific password on Facebook by going to facebook.com >
  Settings > Security > App passwords > Generate app passwords, and generate one
  to use with Mopidy-Spotify.

- `libspotify` 12. The official C library from our `Unofficial
  libspotify archive <https://mopidy.github.io/libspotify-archive/>`_.
  The package is available as `libspotify12` from
  `apt.mopidy.com <http://apt.mopidy.com/>`__.

- `pyspotify` >= 2.0.5. The `libspotify` Python wrapper. The package is
  available as `python3-spotify` from apt.mopidy.com or `pyspotify` on PyPI.
  See https://pyspotify.readthedocs.io/en/latest/installation/ for how to install
  it and its dependencies on most platforms.

- `Mopidy` >= 3.0. The music server that Mopidy-Spotify extends.

If you install Mopidy-Spotify from apt.mopidy.com, AUR, or Homebrew, these
dependencies are installed automatically.

## Installation

### PyPI

~~~~~
sudo python3 -m pip install Mopidy-Spotify
~~~~~

### MacOS (Homebrew)

~~~~~
brew install mopidy/mopidy/mopidy-spotify
~~~~~

### Debian / Ubuntu

This extension is currently not packaged in Debian/Ubuntu, but you can install the `mopidy-spotify` Debian package from Mopidy's APT repository.

First, follow the instructions at [apt.mopidy.com](https://apt.mopidy.com) on how to setup Mopidy's APT repo on your system.

Then, install the `mopidy-spotify` package:

~~~~~
sudo apt install mopidy-spotify
~~~~~

### Arch (AUR)

~~~~~
yay -S mopidy-spotify
~~~~~

### Fedora

~~~~~
dnf install mopidy-spotify
~~~~~

See https://mopidy.com/ext/spotify/ for alternative installation methods.

## Configuration

Before starting Mopidy, you must add your Spotify Premium username and password
to your Mopidy configuration file and also visit
https://mopidy.com/ext/spotify/#authentication
to authorize this extension against your Spotify account:

~~~~~
  [spotify]
  username = alice
  password = secret
  client_id = ... client_id value you got from mopidy.com ...
  client_secret = ... client_secret value you got from mopidy.com ...
~~~~~

The following configuration values are available:

- `spotify/enabled`: If the Spotify extension should be enabled or not.
  Defaults to `true`.

- `spotify/username`: Your Spotify Premium username. You *must* provide this.

- `spotify/password`: Your Spotify Premium password. You *must* provide this.

- `spotify/client_id`: Your Spotify application client id. You *must* provide this.

- `spotify/client_secret`: Your Spotify application secret key. You *must* provide this.

- `spotify/bitrate`: Audio bitrate in kbps. `96`, `160`, or `320`.
  Defaults to `160`.

- `spotify/volume_normalization`: Whether volume normalization is active or
  not. Defaults to `true`.

- `spotify/timeout`: Seconds before giving up waiting for search results,
  etc. Defaults to `10`.

- `spotify/allow_cache`: Whether to allow caching. The cache is stored in a
  "spotify" directory within Mopidy's `core/cache_dir`. Defaults to `true`.

- `spotify/allow_network`: Whether to allow network access or not. Defaults
  to `true`.

- `spotify/allow_playlists`: Whether or not playlists should be exposed.
  Defaults to `true`.

- `spotify/search_album_count`: Maximum number of albums returned in search
  results. Number between 0 and 50. Defaults to 20.

- `spotify/search_artist_count`: Maximum number of artists returned in search
  results. Number between 0 and 50. Defaults to 10.

- `spotify/search_track_count`: Maximum number of tracks returned in search
  results. Number between 0 and 50. Defaults to 50.

- `spotify/toplist_countries`: Comma separated list of two letter ISO country
  codes to get toplists for. Defaults to blank, which is interpreted as all
  countries that Spotify is available in.

- `spotify/private_session`: Whether to use a private Spotify session. Turn
  on private session to disable sharing of played tracks with friends through
  the Spotify activity feed, Last.fm scrobbling, and Facebook. This only
  affects social sharing done by Spotify, not by other Mopidy extensions.
  Defaults to `false`.

## Resources

- [Source code](https://github.com/mopidy/mopidy-spotify)
- [Issue tracker](https://github.com/mopidy/mopidy-spotify/issues)
- [Changelog](https://github.com/mopidy/mopidy-spotify/releases)

## Credits

- Original author: [Stein Magnus Jodal](https://github.com/jodal)
- Current maintainer: [Stein Magnus Jodal](https://github.com/jodal)
- [Contributors](https://github.com/mopidy/mopidy-spotify/graphs/contributors)
