fil4.lv2 - Parametric Equalizer
===============================

fil4.lv2 is a 4 band parametric equalizer with additional low+high shelf
filters and a (optional) custom GUI displaying the transfer function.

Usage
-----

The parameters can be set by moving the nodes in the graph or directly 
via control knobs:

*   Shift + click: reset to default
*   right-click: toggle current value with default, 2nd click restore.

The Ctrl key allows for fine grained control when dragging or
using the mouse-wheel on a knob.

Mouse-wheel granularity:
*   Gain: 1dB (fine: 0.2dB)
*   Frequency: 1/6 octave (fine: 1/24 octave)
*   Bandwidth: 1/3 octave (fine: 15 steps for a ratio 1:2)

All switches and controls are internally smoothed, so they can be
used 'live' without any clicks or zipper noises. This should make
this plugin a good candidate for use in systems that allow automation
of plugin control ports, such as Ardour, or for stage use.

Install
-------

Compiling these plugin requires the LV2 SDK, gnu-make, a c-compiler,
libpango, libcairo and openGL (sometimes called: glu, glx, mesa).

```bash
  git clone git://github.com/x42/fil4.lv2.git
  cd fil4.lv2
  make submodules
  make
  sudo make install PREFIX=/usr
```

Optionally compile a standalone jack app (not covered by `make install`)
```bash
  make jackapps
  ./x42/x42-fil
```

Note to packagers: The Makefile honors `PREFIX` and `DESTDIR` variables as well
as `CPPFLAGS`, `CFLAGS`, `CXXFLAGS`, `LDFLAGS`.
Additionally there is `OPTIMIZATIONS` (custom additions to both `CFLAGS` and `CXXFLAGS`).


Screenshots
-----------

![screenshot](https://raw.github.com/x42/fil4.lv2/master/img/fil4_v2.png "Fil4 GUI")

Details
-------

Fil4 is based on fil-pluins LADSPA.

Fil4 consists of four 2nd order resonant filters using a Mitra-Regalia
style lattice filter, which has the nice property of being stable
even while parameters are being changed.

The high/low-shelf filters are standard 2nd order biquad/IIR filters.
The DC-offset filter has a fixed roll-off of -12dB/oct with -3dB at 20Hz.
