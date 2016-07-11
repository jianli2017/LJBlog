---
layout: post
title:  sdfdfdfsdfqfsdfdfdfs
category: mach-o 文件结构
tags:KSCrash
comments: true
---


# 第一首

~~~
/Users/gome/Desktop/GomeEShop:
Mach header
      magic cputype cpusubtype  caps    filetype ncmds sizeofcmds      flags
MH_MAGIC_64   ARM64        ALL  0x00     EXECUTE    59       6648   NOUNDEFS DYLDLINK TWOLEVEL WEAK_DEFINES BINDS_TO_WEAK PIE
~~~


~~~
bogon:~ LiJian$ otool -h  /Users/gome/Desktop/GomeEShop 
/Users/gome/Desktop/GomeEShop:
Mach header
      magic cputype cpusubtype  caps    filetype ncmds sizeofcmds      flags
 0xfeedfacf 16777228          0  0x00           2    59       6648 0x00218085
 ~~~
 
 ~~~
  otool -l  /Users/gome/Desktop/GomeEShop 
/Users/gome/Desktop/GomeEShop:
Load command 0
      cmd LC_SEGMENT_64
  cmdsize 72
  segname __PAGEZERO
   vmaddr 0x0000000000000000
   vmsize 0x0000000100000000
  fileoff 0
 filesize 0
  maxprot 0x00000000
 initprot 0x00000000
   nsects 0
    flags 0x0
~~~


segment_command_64

~~~    
Load command 1
      cmd LC_SEGMENT_64
  cmdsize 952
  segname __TEXT
   vmaddr 0x0000000100000000
   vmsize 0x000000000229c000
  fileoff 0
 filesize 36290560
  maxprot 0x00000005
 initprot 0x00000005
   nsects 11
    flags 0x0
Section
  sectname __text
   segname __TEXT
      addr 0x0000000100004b64
      size 0x0000000001e9b9e8
    offset 19300
     align 2^2 (4)
    reloff 0
    nreloc 0
     flags 0x80000400
 reserved1 0
 reserved2 0

Load command 4
            cmd LC_DYLD_INFO_ONLY
        cmdsize 48
     rebase_off 41893888
    rebase_size 141304
       bind_off 42035192
      bind_size 34824
  weak_bind_off 42070016
 weak_bind_size 184
  lazy_bind_off 42070200
 lazy_bind_size 31424
     export_off 42101624
    export_size 474384
Load command 5
     cmd LC_SYMTAB
 cmdsize 24
  symoff 42717648
   nsyms 520197
  stroff 51055968
 strsize 11094644
 

Load command 6
            cmd LC_DYSYMTAB
        cmdsize 80
      ilocalsym 0
      nlocalsym 500741
     iextdefsym 500741
     nextdefsym 17674
      iundefsym 518415
      nundefsym 1782
         tocoff 0
           ntoc 0
      modtaboff 0
        nmodtab 0
   extrefsymoff 0
    nextrefsyms 0
 indirectsymoff 51040800
  nindirectsyms 3792
      extreloff 0
        nextrel 0
      locreloff 0
        nlocrel 0
Load command 7
          cmd LC_LOAD_DYLINKER
      cmdsize 32
         name /usr/lib/dyld (offset 12)
Load command 8
     cmd LC_UUID
 cmdsize 24
    uuid C86C5BF4-9C5F-3A25-818F-9FE1684096C3
Load command 9
      cmd LC_VERSION_MIN_IPHONEOS
  cmdsize 16
  version 7.0
      sdk 9.2
Load command 10
      cmd LC_SOURCE_VERSION
  cmdsize 16
  version 0.0
Load command 11
       cmd LC_MAIN
   cmdsize 24
  entryoff 627752
 stacksize 0
Load command 12
          cmd LC_ENCRYPTION_INFO_64
      cmdsize 24
     cryptoff 16384
    cryptsize 36274176
      cryptid 0
          pad 0
Load command 13
          cmd LC_LOAD_DYLIB
      cmdsize 48
         name /usr/lib/libc++.1.dylib (offset 24)
   time stamp 2 Thu Jan  1 08:00:02 1970
      current version 237.2.0
compatibility version 1.0.0
         
Load command 56
      cmd LC_FUNCTION_STARTS
  cmdsize 16
  dataoff 42576008
 datasize 141640
Load command 57
      cmd LC_DATA_IN_CODE
  cmdsize 16
  dataoff 42717648
 datasize 0
Load command 58
      cmd LC_CODE_SIGNATURE
  cmdsize 16
  dataoff 62150624
 datasize 313552
 ~~~