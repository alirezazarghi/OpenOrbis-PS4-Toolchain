# Changelog



## Beta

**v0.1.1 - May 13th, 2020**

- Added MiraLib C# library on Continuous Integration (CI).

**v0.1.1 - May 12th, 2020**

- Fixed an issue where samples would fail to build on clang 10+ due to a sneaky change in LLVM where it no longer defines `__GNUC__`.
- Fixed an issue where Makefiles would not automatically create directories for intermediate files, causing them to fail on systems where the directories didn't already exist (ie. Visual Studio didn't create them).
- Fixed script line endings in `/extra` scripts from CRLF to LF for release.

**v0.1.0 - May 11th, 2020**

- Public release.
- Put create-eboot/create-lib on Continuous Integration (CI).



## Alpha

*Note: Some changes that didn't go anywhere / were deadends were left out as they were irrelevant, and a lot of the dead time spaces in the earlier versions were reversing periods where CrazyVoid and Specter were reversing the OELF format.*

**v0.0.54 - May 11th, 2020**

- Prepared for release, initiated basic CI for create-eboot.

**v0.0.53 - May 6th, 2020**

- Add new C# MiraLib library.

**v0.0.52 - May 2nd, 2020**

- Added linux build script for crt1 and crtlib.

**v0.0.51 - March 7th, 2020**

- Added audio sample - znullptr.
- Fixed formatting issues in sample READMEs.
- Add wav decoding to audio-wav sample.
- Updated PS4 library headers to add more definitions.

**v0.0.50 - March 7th, 2020**

- Fixed an issue where the bss section was not being considered when generating data program headers.
- Removed a prototype that could cause issues in certain build situations from freetype proto header.
- Updated crt1 to `Need_sceLibc` is set to 1.

**v0.0.49 - March 6th, 2020**

- Added text wrapping to font sample.

**v0.0.48 - March 5th, 2020**

- Major PS4 library header update.
- Added PNG/JPEG decoding sample.
- Fixed an issue where the custom heap size was not being respected due to a bug in the CRT stub.

**v0.0.47 - March 5th, 2020**

- Added font sample.
- Added freetype lib.
- Updated graphics sample.
- Added STB freestanding header library.

**v0.0.46 - March 3rd, 2020**

- Added video sample which rendered graphics to the screen via CPU rendering.
- Added CrazyVoid's pthread sample.

**v0.0.45 - March 3rd, 2020**

- Added readelf tool.
- Updated source documentation.
- Removed redundant files from readelf.

**v0.0.44 - March 2nd, 2020**

- Added CrazyVoid's new headers.
- Fixed an issue where SSE instructions would trigger a SIGBUS crash due to the CRT stub not aligning the stack to a 16-byte boundary.

**v0.0.43 - February 1st, 2020**

- Added missing crtlib source.

**v0.0.42 - January 31st, 2020**

- Added PDF documentation.
- Removed deprecated documentation.
- Reworked samples into Visual Studio projects and makefiles.
- Fixed a nil dereference in create-lib when no .data.rel_ro section was present.

**v0.0.41 - January 30th, 2020**

- Added PS4 SELF Project and PS4 SPRX Project Visual Studio templates.
- Moved linker script to root directory.

**v0.0.40 - January 29th, 2020**

- Added crtlib stub
- Added ldflags and script to build create-eboot/create-lib cross-platform.
- Fixed an issue where if an input ELF contained no dynamic functions or globals, a crash would occur due to bad checking logic.
- Fixed an issue where create-lib would write the interpreter string at the top of .text when it shouldn't for libraries.
- Fixed an issue where sce_process_param was dereferenced in create-lib, when it should be dereferencing sce_module_param.

**v0.0.39 - January 28th, 2020**

- Added library sample.

**v0.0.38 - January 24th, 2020**

- Added make FSELF functionality into create-eboot, removing the need for flatz' script.

**v0.0.37 - January 23rd, 2020**

- Rebranded elf-to-oelf as create-eboot.
- Fixed an issue where the `Need_sceLibc` symbol entry was off by one.

**v0.0.36 - January 23rd, 2020**

- Fixed an issue where certain relocations were not ported due to a missing PIE (position independent executable) flag.
- Fixed build scripts to use elf-to-oelf.
- Added dictionary definitions for module to lib in elf-to-oelf.

**v0.0.35 - January 22nd, 2020**

- Added system example.
- Added executables into the repo for testing (to be removed later).

**v0.0.34 - January 22nd, 2020**

- Added networking sample.
- Added documentation.

**v0.0.33 - January 22nd, 2020**

- Added BSD libc library headers.
- Deprecated PS4 Assistant payload in favor of Mira.

**v0.0.32 - January 21st, 2020**

- Added controller input sample.

**v0.0.31 - January 21st, 2020**

- Added hello_world sample.
- Removed deprecated test/usleep sample.
- Fixed an issue where `stdio.h` was using a type that was not valid on linux.
- Fixed an issue where the prototype for `sceKernelUsleep` and `rename` was not correct.

**v0.0.30 - January 20th, 2020**

- Added comment documentation to elf-to-oelf.
- Added information to OELF specification documentation.

**v0.0.29 - January 20th, 2020**

- Finished elf-to-oelf v0.1.
  - Added support for need_sceLibc object.
  - Added globals to keep track of the need_sceLibc object as well as the number of entries for the hash table.
  - Added rela table entries for .data.rel.ro entries sceLibcMallocReplace, sceLibcNewReplace, Need_sceLibc, sceLibcMallocReplaceForTls.
  - Added rela table entries for .sce_process_param entries sceLibcParam, sceKernelMemParam, sceKernelFsParam.
  - Added sorting for program headers to ensure a standard order is followed.
  - Added support for PT_GNU_EH_FRAME / exception handler frames.
  - Added a helper function to write relative rela entries.
  - Added a helper function to write object rela entries.
  - Added a helper function to get a symbol value by name from the input ELF.
  - Fixed an issue where OrbisElf.ProgramHeaders was of type []elf.ProgHeader - it is now of type []elf.Prog64.
  - Fixed an issue where libkernel was not the first library included.
  - Fixed an issue where the size of NID entries was incorrect and caused calculation issues in building the symbol table.
  - Fixed an issue where the nchain field of the hash table and by extension the number of entries in the hash table itself were incorrect due to not factoring in non-external symbols.
  - Fixed an issue where DT_FLAGS was incorrect and used a deprecated value.
  - Fixed an issue where DT_SCE_MODULE_INFO was incorrect because it used the size of the module table when it should have been using the offset.
  - Fixed an issue where PT_DYNAMIC's memory size was null, which caused the PS4's ELF loader to fail.
  - Fixed other various offset miscalculations in the program header table generator.
  - Fixed an issue where the program header count 'Phnum' was sometimes incorrect in the ELF header.

**v0.0.28 - January 15th, 2020**

- Added program header rewriting.
- Added alignment between the string table and the symbol table in dynlib data.
- Fixed an issue where the relocation / rela table size was incorrect as it did not account for the size of the jump table.

**v0.0.27 - January 14th, 2020**

- Added program header generators for PT_SCE_DYNLIB_DATA, PT_DYNAMIC.
- Added code to commit the write of the generated dynlib data segment to the output file.
- Added code to record the file offset of the dynlib data segment.
- Fixed an issue where the file offset and size of the dynamic table were not recorded.

**v0.0.26 - January 11th, 2020**

- Added program header generators for PT_INTERP, PT_TLS, PT_LOAD (text), PT_GNU_EH_FRAME, PT_SCE_RELRO, PT_LOAD (data), and PT_SCE_PROC_PARAM.
- Added a helper function to get program headers by type and flag.
- Fixed `OrbisElf.ProgramHeaders` type to `[]elf.ProgHeader` instead of `[]elf.Prog`.

**v0.0.25 - January 9th, 2020**

- Add program header table generator (elf-to-oelf).
- Removed redundant `[]byte()` cast from the `writeFingerprint()` function in the dynlib data generator (elf-to-oelf).

**v0.0.24 - January 7th, 2020**

- Added relocation table generator (elf-to-oelf).
- Added symbol hash table generator (elf-to-oelf).
- Added helper function to get a dynamic tag value that isn't string-related.

**v0.0.23 - January 4th, 2020**

- Added refactored dynlib data generator to elf-to-oelf.
- Added helper function to check if a given library file contains an external symbol, which will be needed for relocation table generation.
- Fixed an issue where `OrderedMap.Set()` would not take into account if a key was already created and would add duplicate key entries.

**v0.0.22 - January 3rd, 2020**

- Fixed `program_headers.py` so that it now displays the virtual address and physical address of the segment.
- Fixed `rela_entries.py` so that it now displays all entries instead of just some of them.

**v0.0.21 - January 3rd, 2020**

- Switched static library stubs to dynamic libraries so we can put more of the workload on the LLVM linker and less on elf-to-oelf.
- Fixed an issue where a bad typedef in `stdio.h` caused compilation issues (`wchar_t`).

**v0.0.20 - November 21st, 2019**

- Added relinker, which goes which goes back through the .text segment and rewrites the stubs to create jumps that dereference the Procedure Linkage Table (PLT) (elf-to-oelf).
- Added program header entries for the interpreter and TLS.
- Reworked the way `writeOriginalText()` worked so that stubs are also written, where they weren't before due to an oversight.
- Fixed R_AMD64_RELATIVE constant to the proper name, being R_AMD64_JUMP_SLOT for the 0x7 RELA type.
- Fixed `writeStrTable()` off-by-one error when calculating the size of the table.
- Fixed an issue where `writeRelaTable()` would write the entries r_info backwards. Now the symbol index is stored in the upper 32-bits, and the type in the lower to properly adhere to ELF standards.
- Fixed `rela_entries.py` script so that it properly calculates the number of RELA entries.
- Removed redundant integer cast in `writeSectionPadding()`.

**v0.0.19 - November 16th, 2019**

- Added dynamic table building to SCE_Dynlib_Data segment builder (elf-to-oelf).
- Fixed `.sce_proc_param` to align to a 0x10 byte boundary.
- 

**v0.0.18 - November 13th, 2019**

- Added hash table building to SCE_Dynlib_Data segment builder (elf-to-oelf).
- Added section padding before NID, symbol, rela, and hash table to align to a 0x10 byte boundary.
- Added section padding before dynamic table to align to a 0x10 byte boundary.

**v0.0.17 - November 12th, 2019**

- Refactored elf-to-oelf (complete overhaul).

**v0.0.16 - October 29th, 2019**

- Added base RELA table building to SCE_Dynlib_Data segment builder (elf-to-oelf).
- Fixed relro segment header to use proper virtual and physical addresses.
- Fixed the `rela_entries.py` script to more accurately reflect the `r_sym` field as "symbol" rather than "info".

**v0.0.15 - October 23rd, 2019**

- Added symbol table building to SCE_Dynlib_Data segment builder (elf-to-oelf).
- Refactored how structs are written via binary serialization (elf-to-oelf).

**v0.0.14 - October 22nd, 2019**

- Added script to read symbol table entries.

**v0.0.13 - October 21st, 2019**

- Added initial SCE_Dynlib_Data segment builder (elf-to-oelf).

**v0.0.8 - July 29th, 2019**

- Fixed various script bugs due to improperly reading RELA information.

**v0.0.7 - July 28th, 2019**

- Added data segment builder (elf-to-oelf).

**v0.0.6 - July 26th, 2019**

- Switched elf-to-oelf to Golang codebase.
- Added EH frame builder (elf-to-oelf).

**v0.0.5 - March 28th, 2019**

- Added preliminary orbisLibGen.
- Added flatz' make_fself.py script.
- Added initial PS4 library headers (reversing).

**v0.0.4 - March 27th, 2019**

- Added elf-to-oelf segment builders (C++).

**v0.0.3 - March 26th, 2019**

- Added additional OELF documentation (reversing).
- Added script to print out dynamic entries of OELFs.
- Added script to print out program headers of OELFs.
- Added script to print out RELA entries of OELFs.

**v0.0.2 - March 5th, 2019**

- Added initial elf-to-oelf implementation (C++).
- Added preliminary OELF documentation (reversing).

**v0.0.1 - Feb. 26th, 2019**

- Added README, LICENSE, and BSD libc header files.