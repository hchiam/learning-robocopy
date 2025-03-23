# Learning robocopy

Just one of the things I'm learning. <https://github.com/hchiam/learning>

- buit into windows, not on mac
- CLI command (vs a UI like [Total Commander](https://www.youtube.com/watch?v=_txtc5EjbXI))
- TL;DR:

  - ```sh
    # for windows:
    
    # diffs before actually do:
    robocopy C:\source\folder C:\destination\folder /MIR /L
    
    # actually copy over diffs:
    robocopy C:\source\folder C:\destination\folder /MIR
    ```

  - ```sh
    # for windows:

    # diffs before actually do:
    rbcd() {
        source_folder="$1"
        dest_folder="$2"
        
        if [[ -z "$source_folder" || -z "$dest_folder" ]]; then
            echo "Usage: rbcd <source_folder> <dest_folder>"
            return 1
        fi

        robocopy "$source_folder" "$dest_folder" /MIR /L
    }

    # actually copy over diffs:
    rbc() {
        source_folder="$1"
        dest_folder="$2"
        
        if [[ -z "$source_folder" || -z "$dest_folder" ]]; then
            echo "Usage: rbc <source_folder> <dest_folder>"
            return 1
        fi

        robocopy "$source_folder" "$dest_folder" /MIR
    }
    ```

## Main Notes

- from <https://www.youtube.com/watch?v=-vl3pNVr_8Q>

- `robocopy C:\source\folder C:\destination\folder /r:3 /w:2 /MIR /SEC`
  - `/r:3` = retry 3 times, (e.g. if file still open)
  - `/w:2` = wait for 2 seconds until retry
  - `/MIR` = mirror _differences_ (minimally update destination with deletions/additions/edits)
  - `/SEC` = copy over security permissions

- you can `robocopy` from a remote receiving destination server:
  - `robocopy \\remotesourceservername\c$\source\folder C:\destination\folder /r:3 /w:2 /MIR /SEC`
    - `c$` is the `C:` drive on the remote source server

- `robocopy /?` = help, like to see other options like `/E` or `/PURGE`

## More info, like if you don't currently have access to a Windows machine

<https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy>

<https://www.pdq.com/blog/hitchhikers-guide-to-robocopy/>

- `/L` = only list the files, don't copy, delete, or time stamp = show what will happen but don't actually do it
  - example: `robocopy C:\source\folder C:\destination\folder /r:3 /w:2 /MIR /SEC /L`
  - you might want to combine it with `/LOG` to save to log file, not just show results to CLI output

- `/NFL` = don't show file names
- `/NDL` = don't show directory (folder) names
- `/NP` = don't show progress (file/directory count) of copy operation
