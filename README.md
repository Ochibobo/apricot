### Apricot

Row oriented storage format (N-Ary) that is proprietary to the Opslag storage engine.


### API Design
- [ ] Consider Apache Thrift or ProtoBuf.
- [ ] Implementation is either in:
  - [ ] C
  - [ ] Rust
  - [ ] Java
- [ ] Semantics:
  - [ ] open
  - [ ] close
  - [ ] read
  - [ ] write
  - [ ] seek
  - [ ] size

### File types
- [ ] Database table files
  - [ ] Magic number
  - [ ] Version information
  - [ ] Header information
    - [ ] Block size
    - [ ] Page layout information
    - [ ] Data structure definition
  - [ ] Actual data
  - [ ] In postgres:
    - [ ] 8 KB pages are used
    - [ ] Page header is 24 bytes
    - [ ] Rows written from down to up in the page
    - [ ] There's a special space; used for index file pages.
    - [ ] 2 pointers:
      - [ ] Lower & Upper
      - [ ] They grow towards each other
    - [ ] Data rows at the tail
    - [ ] At the beginning, we have as many line pointers as rows that correspond to rows and point to them
      - [ ] Have fixed width.
      - [ ] Rows may move outside when other rows grow or shrink
      - [ ] Indirection gives freedom to re-organize space
      - [ ] Then slot number is just the line pointer number
      - [ ] The `ctid` is in the format <page_number, line_pointer_number>
      - [ ] The `page header` contains:
        - [ ] lsn
        - [ ] checksum
        - [ ] flags
        - [ ] lower - pointer
        - [ ] upper - pointer
          - [ ] upper - lower = free space.
        - [ ] special - where the special space start
        - [ ] pagesize
        - [ ] version
        - [ ] prune_xid
    - [ ] `pageinspect` extension to peek inside the page
      - [ ] Access page headers
      - [ ] Access line pointers
    - [ ] There us a `free space management file`
      - [ ] `FSM` trees.
    - [ ]  
- [ ] Index files
- [ ] Write Ahead Log
- [ ] Toast files
- [ ] Configuration files
- [ ] Log files
- [ ] System catalog
- [ ] Maximum size per table
- [ ]  


### Other concerns
- [ ] Versioning
- [ ] `ALTER TABLE ADD COLUMM` effect
