# Note Watch (NW)

mardown cross-link manager

Where `link-index` is a text file where each line is `note-F`->`note-T`, where -> is some delimiter separating the filenames of two notes where there is at least one link from `note-F` to `note-T`.



- When `note-P` note is renamed `note-R`

  1. update archive (pre-rename-handler)

  2. for each `note-F`->`note-T` entry in `link-index`:

        1. if `note-F` = `note-P`:

              1. change entry in `link-index` to `note-R`->`note-T`

        2. if `note-T` = `note-P`:

              1. update `note-F` file:[^change files that  link to note]<br>change all links to `note-P` into links to `note-R`<br>(including backlinks)

              2. change entry in `link-index` to `note-F`->`note-R`
  3. update archive (post-rename-handler)
  
  
  
- When `note-P` note is created or changed:<br>Check linked files

  1. update archive (pre-change-handler)
  2. make a list of all links other than backlinks `note-P` as `notes-L`
  3. for each `note-F`->`note-T` entry in `link-index`:<br>where  `note-F` = `note-P`:
     1. if the link is still there—`note-T` is in `notes-L`:
        1. remove `note-T` from `notes-L`
     2. otherwise—the link has been removed from the file:
        1. remove `note-P`->`note-T` entry from `link-index`
        2. update `note-T`:[^change files that note has a new link to]<br>remove backlick to `note-P`
  4. for links that are new—each `note-L` remaining in `notes-L`:
     1. add `note-P`->`note-T` entry to `link-index`
     2. if `note-T` noes not exists:
        1. create new file for `note-T`
     3. update `note-T`:<br>add backlick to `note-P`