### File Description

The `Apricot file format` stores data for 3 primary cases:

    - Data
    - Indices
    - Free pages

This file implements the `N-ary Storage Model`. A record has its tuples stored contiguously. The tuples are stored in a `page` of `16KB`; this is the default page size that is configurable. Each file starts with  a `file header` that contains the following:

    - [ ] Magic Number (4 bytes) -  unique identifier that identifies the file as an Apricot file
    - [ ] Version number (4 bytes) - indicates the format version of the file
    - [ ] Relation object id - object identifier of the relation associated with the file
    - [ ] Maximum tuple size (4 bytes) - maximum tuple size allowed
    - [ ] Free space map (16 bytes) - pointer to the free space map within the file which keeps track of free blocks
    - [ ] Flags (4 bytes) - indicates properties such as:
      - [ ] Is it a temporary file
      - [ ] Is it a frozen file
      - [ ] Is it a deleted file
      - [ ] Is it an active file
    - [ ] Addition fields:
      - [ ] Creation time
      - [ ] Last modification time
      - [ ] Checksum
      - [ ] Compression information if file is compressed; algorithm & level
      - [ ] Security-related information - access control & encryption
      - [ ] Extra features


The `page` design depends on it's contents; for example, the page structure of the `data` file differs from the `index` file. The page structure is implemented as a `slotted page` where pointers are used as a form of indirection. This is a common pattern employed in implementing a page in relational databases. The page has 3 primary parts to it:

    - [ ] Page header
    - [ ] Line pointers
    - [ ] Tuples

At the page level, each `tuple` has a maximum size of `2KB`. The storage of each attribute of each tuple is in the page as is by default. Based on the type of attribute, some attributes may be compressed before being persisted. This information is stored in the header. The <compression_algorithm, attribute> pairs are stored as part of the page header. For attributes that are very large, a <pointer, size> pair is stored instead. The pointer refers to the position or offset in the extended storage file where the data/bytes compressed or not are stored.

The extended storage file stores data that's too large to fit into the regular page. The data is still fit into pages. The page structure is different from the data page structure. It contains a header with details such as the page number/id, the size of the data, a flag showing if the data stored is fully stored in the page or if it's partial, a pointer to the next/prev page, an optional bit indicating if this is the last page (if it is from a previous page), compression algorithm & ratio etc. 

`NULLs` are represented in a special way.


