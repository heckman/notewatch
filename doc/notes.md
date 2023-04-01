| NEW | EXISTS | File is... |
| ---- | ---- | ---- |
| True | True | created, or moved to here |
|   False  |  True  | modified, or moved to here overwriting extant file |
|   True   | False | deleted, or moved from here (happens when created, then deleted very quickly) |
|  False  | False | deleted, or moved from here |

(moved out of scope is the same as deleted)



#### Converting Watchman output to internal commands

Output from watchman includes: inode, is_new, does_exist, filename

```
for each line outputted from watchman:
	if does_exist:
		add to 'existing' hash-table as inode: filename
		if 'is_new' add to 'isNew' hash-table as inode: True
	else
		add to 'non-existing' hash-table as inode: filename
for each inode in 'non-existing' hash-table keys:
	if inode is in 'existing' hash-table keys:
		add inode to 'renamed' hash-table
		output rename non-existing[inode] existing[inode] isNew[inode]
	else:
		output remove function(non-existing[inode])
for each inode in existing hash-table keys:
	if inode is a key in 'renamed' hash-table: continue
	if inode is a key in 'new' hash-table:
		output remove function(existing[inode])
	else:
		output remove function(existing[inode])
```





#### To batch stdin in bash

Runs `handler` for every batch in pipe, collected when pipe is idle for `timeout` seconds

```
# Read stdin and pipe to specified command a batch at a time,
# where batches are delineated when stdin is idle for `timeout` seconds.
# Each batch invokes a new instance of the command. A timeout <500ns is not advised.
function batchify() { local timeout="${1:-0.000001}" # remaining args are command
    while read -r line; do {
        echo "$line"
        while read -rt "$timeout" line; do
            echo "$line"
        done
    } | "${@:2:$#-1}"; done
}
```



