# Debugging


If something goes wrong while using the Python CLI client, the
first place to check for more information so that you can [file a quality bug
report](https://github.com/dandi/dandi-cli/issues) is the logs.  Every command records a copy of its logs in a logfile, the location of which is
reported to the user when the command finishes running.  The location of the
logs varies by platform, e.g.:

- Linux: `~/.cache/dandi-cli/log` or `$XDG_CACHE_HOME/dandi-cli/log`
- macOS: `~/Library/Logs/dandi-cli`

Logs are named with a combination of the time at which the `dandi` command
started running and the process ID of the command.

Recent versions of the client include all possible debugging information in the
logs, but if you're using an older version, only log messages that were printed
to the user when the command ran are recorded.  As a result, in order to get
complete debugging information, you may have to rerun the problematic command,
this time increasing the logging level by passing `-l DEBUG` or `--log-level
DEBUG` on the command line.  Note that this option goes between the main
`dandi` command and the name of the subcommand:

    # Right:
    dandi -l DEBUG upload

    # Wrong:
    dandi upload -l DEBUG

In addition, many commands can be put into a developer-specific mode for
showing raw progress information instead of fancy progress bars.  For the
`delete`, `organize`, `upload`, and `validate` commands, this can be done by
setting the `DANDI_DEVEL` environment variable and passing `--devel-debug` to
the command:

    DANDI_DEVEL=1 dandi upload --devel-debug

For the `download` command, the equivalent is the `-f debug`/`--format debug`
option:

    dandi download -f debug

More advanced users who are familiar with [the Python
debugger](https://docs.python.org/3/library/pdb.html) can instruct the client to
automatically open the debugger if any errors occur by supplying the `--pdb`
option to the command.  Like the `-l`/`--log-level` option, the `--pdb` option
must be placed between `dandi` and the name of the subcommand.
