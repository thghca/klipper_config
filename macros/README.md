# General
* Macros starting with an underscore are not intended to be directly called by the user during normal printer use
* Macros starting with double underscore are not intended to be directly called by the user at all (except debug)
* Klipper merge sections in all included config files, so it possible to define macro gcode in one file and extra variables in another

# `__ON_STARTUP.cfg`
Initialisations when printer starts
* `[delayed_gcode ON_STARTUP]` - timer, runs asap after start
* `[gcode_macro __ON_STARTUP]` - executes it's own variables prefixed with `run_` as gcode commands.
* Extra `run_*` variables can be defined in another files.

# `_CONFIG.cfg`

* `[gcode_macro _CONFIG]` - Holds config values for other macros
* Extra variables can be defined in another files.

# `_GPUSH_GPOP.cfg`
Easy save/load gcode states with stack (kind of).
* `[gcode_macro _GPUSH]` - Put current gcode state on top of stack. Call that before macro moves.
* `[gcode_macro _GPOP]` - Restore current gcode state from top of stack. Call that after macro moves. Pass params, so `MOVE=1` if restore position needed.
* `[gcode_macro _GCLEAR]` - Reset current stack index. Usually not needed, but no harm to reset after sd print.
* Always call gpop after gpush in same macro. Stack head should be 0 after exiting outer script.
