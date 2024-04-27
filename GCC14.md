# Grub 2.12 GCC 14 compilation issues
## All
### Problem 1:
```
../../grub-core/tests/strtoull_test.c: In function ‘strtoull_testcase’:
../../grub-core/tests/strtoull_test.c:31:32: error: passing argument 2 of ‘grub_strtoull’ from incompatible pointer type [-Wincompatible-pointer-types]
   31 |   value = grub_strtoull(input, &output, base);
      |                                ^~~~~~~
      |                                |
      |                                char **
In file included from ../../include/grub/dl.h:29,
                 from ../../include/grub/test.h:22,
                 from ../../grub-core/tests/strtoull_test.c:19:
../../include/grub/misc.h:296:104: note: expected ‘const char ** const restrict’ but argument is of type ‘char **’
```
#### Solution:
- Build with `-fpermissive`

## riscv64
### Problem 2:
```
+ ././grub-mkimage -O riscv64-efi -o grubriscv64.efi.orig -d grub-core --sbat ././sbat.csv -m memdisk.squashfs -p /EFI/fedora all_video boot blscfg btrfs cat configfile cryptodisk echo ext2 f2fs fat font gcry_rijndael gcry_rsa gcry_serpent gcry_sha256 gcry_twofish gcry_whirlpool gfxmenu gfxterm gzio halt hfsplus http iso9660 jpeg loadenv loopback linux lvm luks luks2 memdisk mdraid09 mdraid1x minicmd net normal part_apple part_msdos part_gpt password_pbkdf2 pgp png reboot regexp search search_fs_uuid search_fs_file search_label serial sleep squash4 syslinuxcfg test tftp video xfs zstd efifwsetup efinet lsefi lsefimmap
././grub-mkimage: error: relocation 0x2b is not implemented yet.
```
#### Solution:
- Build with `-fPIC`

### Problem 3:
```
cc1: sorry, unimplemented: code model ‘large’ with ‘-fPIC’
gcc -DHAVE_CONFIG_H -I. -I../../grub-core -I..  -I/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12 -Wall -W  -DGRUB_MACHINE_EFI=1 -DGRUB_MACHINE=RISCV64_EFI -nostdinc -isystem /usr/lib/gcc/riscv64-redhat-linux/14/include -I../../include -I../include -DGRUB_FILE=\"commands/lsacpi.c\" -I. -I../../grub-core -I.. -I../.. -I../../include -I../include -I../../grub-core/lib/libgcrypt-grub/src/    -D_FILE_OFFSET_BITS=64 -std=gnu99 -fno-common -fno-strict-aliasing -g -grecord-gcc-switches -pipe -Wall -Werror=format-security -Wp,-D_GLIBCXX_ASSERTIONS -fno-omit-frame-pointer -Wall -W -Wshadow -Wpointer-arith -Wundef -Wchar-subscripts -Wcomment -Wdeprecated-declarations -Wdisabled-optimization -Wdiv-by-zero -Wfloat-equal -Wformat-extra-args -Wformat-security -Wformat-y2k -Wimplicit -Wimplicit-function-declaration -Wimplicit-int -Wmain -Wmissing-braces -Wmissing-format-attribute -Wmultichar -Wparentheses -Wreturn-type -Wsequence-point -Wshadow -Wsign-compare -Wswitch -Wtrigraphs -Wunknown-pragmas -Wunused -Wunused-function -Wunused-label -Wunused-parameter -Wunused-value  -Wunused-variable -Wwrite-strings -Wnested-externs -Wstrict-prototypes -g -Wredundant-decls -Wmissing-prototypes -Wmissing-declarations -Wcast-align  -Wextra -Wattributes -Wendif-labels -Winit-self -Wint-to-pointer-cast -Winvalid-pch -Wmissing-field-initializers -Wnonnull -Woverflow -Wvla -Wpointer-to-int-cast -Wstrict-aliasing -Wvariadic-macros -Wvolatile-register-var -Wpointer-sign -Wmissing-include-dirs -Wmissing-prototypes -Wmissing-declarations -Wformat=2 -freg-struct-return -march=rv64imac_zicsr_zifencei -mabi=lp64 -fno-omit-frame-pointer -fno-dwarf2-cfi-asm -fno-asynchronous-unwind-tables -fno-unwind-tables -fno-ident -mcmodel=large -fno-stack-protector -Wtrampolines    -ffreestanding  -fPIC -fpermissive -c -o commands/lsacpi_module-lsacpi.o `test -f 'commands/lsacpi.c' || echo '../../grub-core/'`commands/lsacpi.c
make[3]: *** [Makefile:43998: trig_module-trigtables.o] Error 1
make[3]: *** Waiting for unfinished jobs....
cc1: sorry, unimplemented: code model ‘large’ with ‘-fPIC’
cc1: sorry, unimplemented: code model ‘large’ with ‘-fPIC’
make[3]: *** [Makefile:35262: commands/acpi_module-acpi.o] Error 1
make[3]: *** [Makefile:40778: commands/lsacpi_module-lsacpi.o] Error 1
make[3]: Leaving directory '/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12/grub-core'
make[2]: *** [Makefile:29104: all] Error 2
make[2]: Leaving directory '/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12/grub-core'
make[1]: *** [Makefile:12320: all-recursive] Error 1
make[1]: Leaving directory '/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12'
make: *** [Makefile:4021: all] Error 2
error: Bad exit status from /var/tmp/rpm-tmp.TYdSZC (%build)
```
#### Solution:
- Build with `-mcmodel=medany`

### Problem 4:
```
+ ././grub-mkimage -O riscv64-efi -o grubriscv64.efi.orig -d grub-core --sbat ././sbat.csv -m memdisk.squashfs -p /EFI/fedora all_video boot blscfg btrfs cat configfile cryptodisk echo ext2 f2fs fat font gcry_rijndael gcry_rsa gcry_serpent gcry_sha256 gcry_twofish gcry_whirlpool gfxmenu gfxterm gzio halt hfsplus http iso9660 jpeg loadenv loopback linux lvm luks luks2 memdisk mdraid09 mdraid1x minicmd net normal part_apple part_msdos part_gpt password_pbkdf2 pgp png reboot regexp search search_fs_uuid search_fs_file search_label serial sleep squash4 syslinuxcfg test tftp video xfs zstd efifwsetup efinet lsefi lsefimmap
././grub-mkimage: error: relocation 0x14 is not implemented yet.
error: Bad exit status from /var/tmp/rpm-tmp.srVjDB (%build)

RPM build errors:
    Bad exit status from /var/tmp/rpm-tmp.srVjDB (%build)
```
#### Solution:
- Build without `-fPIE` and with `-fno-PIE`

### Problem 5:
```
gcc -fPIC -mcmodel=medany -fno-PIE -Wl,-z,noexecstack -Wl,--no-warn-rwx-segments -std=gnu99 -fno-common -fno-strict-aliasing -g -grecord-gcc-switches -pipe -Wall -Werror=format-security -Wp,-D_GLIBCXX_ASSERTIONS -fno-omit-frame-pointer -specs=/usr/lib/rpm/redhat/redhat-hardened-cc1 -fstack-protector-strong -Wall -W -Wshadow -Wpointer-arith -Wundef -Wchar-subscripts -Wcomment -Wdeprecated-declarations -Wdisabled-optimization -Wdiv-by-zero -Wfloat-equal -Wformat-extra-args -Wformat-security -Wformat-y2k -Wimplicit -Wimplicit-function-declaration -Wimplicit-int -Wmain -Wmissing-braces -Wmissing-format-attribute -Wmultichar -Wparentheses -Wreturn-type -Wsequence-point -Wshadow -Wsign-compare -Wswitch -Wtrigraphs -Wunknown-pragmas -Wunused -Wunused-function -Wunused-label -Wunused-parameter -Wunused-value  -Wunused-variable -Wwrite-strings -Wnested-externs -Wstrict-prototypes -Wcast-align  -Wextra -Wattributes -Wendif-labels -Winit-self -Wint-to-pointer-cast -Winvalid-pch -Wmissing-field-initializers -Wnonnull -Woverflow -Wvla -Wpointer-to-int-cast -Wstrict-aliasing -Wvariadic-macros -Wvolatile-register-var -Wpointer-sign -Wmissing-include-dirs -Wmissing-prototypes -Wmissing-declarations -Wformat=2 -Wno-undef -Wno-sign-compare -Wno-unused -Wno-unused-parameter -Wno-redundant-decls -Wno-unreachable-code -Wno-conversion -Wno-error=attributes  -fPIC -mcmodel=medany -fno-PIE -fpermissive -fPIC -mcmodel=medany -fno-PIE -Wl,-z,relro -Wl,--as-needed -Wl,--build-id=sha1 -Wl,-z,now -specs=/usr/lib/rpm/redhat/redhat-hardened-ld-errors -specs=/usr/lib/rpm/redhat/redhat-hardened-ld   -Wl,-z,relro -Wl,--as-needed    -specs=/usr/lib/rpm/redhat/redhat-annobin-cc1  -Wl,--build-id=sha1   -o grub-script-check grub-core/kern/emu/grub_script_check-argp_common.o grub-core/osdep/grub_script_check-init.o util/grub_script_check-grub-script-check.o  libgrubmods.a libgrubgcry.a libgrubkern.a grub-core/lib/gnulib/libgnu.a  -ldevmapper     
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_short_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
collect2: error: ld returned 1 exit status
make[2]: *** [Makefile:5584: grub-script-check] Error 1
make[2]: *** Waiting for unfinished jobs....
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_short_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
collect2: error: ld returned 1 exit status
make[2]: *** [Makefile:5373: grub-mkrelpath] Error 1
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_short_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `program_invocation_name@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
/usr/bin/ld: unresolvable R_RISCV_PCREL_HI20 relocation against symbol `stderr@@GLIBC_2.27'
collect2: error: ld returned 1 exit status
make[2]: *** [Makefile:5280: grub-mkimage] Error 1
make[2]: Leaving directory '/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12'
make[1]: *** [Makefile:12320: all-recursive] Error 1
make[1]: Leaving directory '/home/jason/rpmbuild/BUILD/grub-2.12/grub-riscv64-efi-2.12'
make: *** [Makefile:4021: all] Error 2
error: Bad exit status from /var/tmp/rpm-tmp.xbqVXw (%build)

RPM build errors:
    Bad exit status from /var/tmp/rpm-tmp.xbqVXw (%build)
```
#### Solution:
- Build without `%{?_hardening_cflags}` and `%{?_hardening_ldflags}`

## x86_64
### Problem 6:
```
/usr/bin/ld: relocatable linking with relocations from format elf64-x86-64 (lib/i386/relocator_module-relocator16.o) to format elf32-i386 (relocator.module) is not supported
```
#### Workaround:
- Comment out `%global alt_efi_arch ia32`

### Problem 7:
```
./../include/grub/misc.h:36:56: error: duplicate case value
```
#### Workaround:
- Set `%global with_legacy_arch 0`
