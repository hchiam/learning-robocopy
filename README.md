# Learning robocopy

Just one of the things I'm learning. <https://github.com/hchiam/learning>

- windows, not on mac

Notes from <https://www.youtube.com/watch?v=-vl3pNVr_8Q>

- `robocopy C:\source\folder C:\destination\folder /r:3 /w:2 /MIR /SEC`
  - `/r:3` = retry 3 times, (e.g. if file still open)
  - `/w:2` = wait for 2 seconds until retry
  - `/MIR` = mirror _differences_ (minimally update destination with deletions/additions/edits)
  - `/SEC` = copy over security permissions

- you can `robocopy` from a remote receiving destination server:
  - `robocopy \\remotesourceservername\c$\source\folder C:\destination\folder /r:3 /w:2 /MIR /SEC`
    - `c$` is the `C:` drive on the remote source server

- `robocopy /?` = help, like to see other options like `/E` or `/PURGE`
