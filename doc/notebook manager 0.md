# Oik

Monitors a directory tree for changes and updates the affected references in (at the moment only markdown) notes within.



#### When a markdown (or image) file is renamed (or moved):

-  in managed files, update links (including backlinks) that are pointed at the renamed file
  - filename might have changed
  - relative path might have changed
- in the renamed/moved file, if it's a markdown file, update relative links
  - relative path might have changed

#### When a markdown file is updated (or created)

- convert wiki links to regular links (optional)
- add backlinks in files that have new links to them from the updated file

- delete backlinks in files that no longer have links to them in the updated file
  - prune empty files devoid of backlinks (optional)

- create new files for new links that point to non-existent files
  - limit creation to within managed directory tree


#### When a markdown file is deleted:

- delete backlinks that pointed at the file
  - prune empty files devoid of backlinks (optional)
- update links everywhere that point at the file (maybe)
  - mark links as broken—¿how do they become unbroken?



