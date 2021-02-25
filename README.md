Unofficial fork of Vital
========================

This is an unofficial fork of [Vital] with changes aimed at use on GNU/Linux
as an LV2 plugin.

[Vital]: https://github.com/mtytel/vital/

This fork is not affiliated with Vital or Matt Tytel in any way. If you enjoy
Vital or this unofficial fork, I encourage you to support Vital financially
by purchasing it at [vital.audio](https://vital.audio) or by donating to Matt
Tytel using the PayPal “Donate” button on [this page](https://tytel.org/helm/).

Building
--------

Note that the plugin will be built as “Vial”, rather than “Vital”.

```bash
make lv2
sudo make install_lv2
```

Add `-j<n>` to use `<n>` parallel processes, and add `CONFIG=Debug` to the
end of both commands to build a debug version (not suitable for general use,
but essential for debugging and compiles much faster).

(You can also try building the standalone version with `make standalone`,
although it might not play well with JACK yet, and you can try building the
VST3 version with `make vst3`, which installs to ~/.vst3, but I get crashes
when opening the UI with the VST3 version.)

Changes from upstream
---------------------

* Fixed an issue which caused the plugin host to freeze when opening the UI.
  See [this commit][ca78].

* Fixed an issue causing graphical glitches and crashes when opening the UI,
  closing it, and then reopening it. This workaround is probably not ideal, as
  it increases the time it takes to open the UI—see [this commit][e95a] for
  more information, and if you’re familiar with JUCE, please let me know if you
  know of a better workaround. (Note: I haven’t verified that this issue is
  present on x86, although I suspect it is—if you use x86 and would like to
  help out, try undoing the changes in [this commit][e95a] and let me know if
  the UI looks and works the same after closing and reopening.)

* Temporarily disabled the UI labeled `ExternalUI`, as it was causing crashes
  whenever the UI was closed. The other UI, `ParentUI`, seems to be the default
  in at least Ardour and Carla anyway, so it shouldn’t be a catastrophic
  change. (I also haven’t verified that this issue is present on x86, but I
  suspect it is—if you want to help out, try changing `ParentUI` to
  `ExternalUI` in Vial.ttl after building/installing, and see if you’re able to
  open and close the UI without crashes.)

* Plugins are now installed to /usr/local/lib rather than /usr/lib. The
  installation prefix can be configured via the Make variable `PREFIX`; it’s
  `/usr/local` by default, but could be changed to, e.g., `/usr` by passing
  `PREFIX=/usr` to `make`.

* Added support for PowerPC (tested on ppc64le Debian). Requires [SIMDe] to be
  installed to the system include path.

* Removed the dependency on the Firebase SDK. This may fix some build/runtime
  errors.

* Fixed miscellaneous errors during the LV2 build process, and improved the
  build process so that files aren’t regenerated when running `make
  install_lv2` if `make lv2` has just been run.

* Other changes not described here: see the [commit log].

[ca78]: https://github.com/taylordotfish/vital/commit/ca788b9ab25377d54d9a15b2cc47aebf344e21e8
[e95a]: https://github.com/taylordotfish/vital/commit/e95a25a1b3f351fd12b1aeadd52402136d42f211
[SIMDe]: https://github.com/simd-everywhere/simde
[commit log]: https://github.com/taylordotfish/vital/commits/master

License
-------

Vital, which this unofficial fork is based on, is licensed under version 3 or
later of the GNU General Public License. All modifications in this fork are
released under the same license. See [LICENSE](LICENSE).
