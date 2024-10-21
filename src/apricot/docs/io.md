### Apricot IO API definition document.
- Write API:
  - [ ] Create a file for a schema
  - [ ] Create a file for an index
    - [ ] BTree
    - [ ] Hash
    - [ ] Trie
    - [ ] Vector
  - [ ] Create a file for extended schema content
    - [ ] Content the either couldn't fit in the page or was specified to be stored in the extended file
    - [ ] Specification is done at the attribute level
    - [ ] Some types are stored in the extened file by default
  - [ ] Write a page to a schema file:
    - [ ] Sequentially
    - [ ] At a particular offset.
  - [ ] Write a page to the index file
  - [ ] Write a page to the extended file
  - [ ] Write Options:
    - [ ] Compression algorithm
      - [ ] Schema-wide
      - [ ] Row-wide
      - [ ] Attribute-specific
      - [ ] Should we include this in the file API or in the storage engine itself?
    - [ ] Column-specific details:
      - [ ] On the main file
      - [ ] On the extended file
      - [ ] Can be based on the column type
      - [ ] Compressed
  - [ ] Flush
  - [ ] Write to memory
  - [ ] Write stats
    - [ ] Number of writes
      - [ ] Pages
      - [ ] Records
    - [ ] Time taken per write
    - [ ] Stats file
  - [ ] Updates
  - [ ] How to handle foreign keys
    - [ ] Cascades
    - [ ] Check against the index file
  - [ ] Write Ahead Log
    - [ ] A journal file

- Read API:
  - [ ] Read pages:
    - [ ] Sequentially page by page
    - [ ] A particular page
    - [ ] A specified page range
    - [ ] A set of random pages
  - [ ] Pagination
    - [ ] Specifying the number of records per read
    - [ ] Specifying number of pages per read
  - [ ] Search will be specified in the storage engine, not here
    - [ ] The engine uses an index to improve reads.
  - [ ] Read Options:
    - [ ] Decompress on read; default.
    - [ ] Read from memory exclusive.
    - [ ] Read from memory/disk -> default.
  - [ ] Read stats
    - [ ] Number of pages
    - [ ] Number of records
    - [ ] Stats file
  - [ ] `JOINS` are not handled here.


- Delete API:
  - [ ] Delete specific record
  - [ ] Delete multiple records
    - [ ] Write a bit to the page header to mark a page as deleted and perform `clean-ups` later.
    - [ ] Deletion involved re-organizing pages
  - [ ] Delete Options:
    - [ ] Delete Immediately
    - [ ] Postpone deletes to compaction


- Compaction API:
  - [ ] Re-organize pages to free make tuples contiguous & avail free pages.
  - [ ] Entire file system is locked


- File management API:
  - [ ] Determine the `base` directory where all files will be stored
  - [ ] Open file
    - [ ] Keep track of open files too.
  - [ ] Close file


- Free Storage management API:
  - [ ] Keep a record of pages with free entries
    - [ ] Not sure as deleted files will be persisted up until compaction if the option is not immediate.
      - [ ] Explore this vs immediate deletes.


