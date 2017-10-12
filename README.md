How to compile on a Windows Machine:

1. Download link https://sourcery.mentor.com/public/gnu_toolchain/arm-none-eabi/arm-2008q1-126-arm-none-eabi-i686-mingw32.tar.bz2
- I used 7zip to unzip the bz2, then must use Winrar (7zip made some .exe 0 size) to unzip the tar to C:\arm-2008q1\

2. Add C:\arm-2008q1\bin to system path

3. Next click the green [Clone or download] button on github, then [Download zip]
- Unzip the dso203-master.zip 
- Open a new Command Prompt and CD into dso203-master directory with all the source files.

4. Test the compiler, type: arm-none-eabi-gcc.exe -v
- output:
- Using built-in specs.
- Target: arm-none-eabi
- Configured with: /scratch/sandra/lite/src/gcc-4.2/configure --build=i686-pc-linux-gnu --host=i686-mingw32 --target=arm-none-eabi --enable-threads --disable-libmudflap --disable-libssp --disable-libgomp --disable-libstdcxx-pch --with-gnu-as --with-gnu-ld --enable-languages=c,c++ -
- -disable-shared --with-newlib --with-pkgversion=Sourcery G++ Lite 2008q1-126 --with-bugurl=https://support.codesourcery.com/GNUToolchain/ --disable-nls --prefix=/opt/codesourcery --with-headers=yes --with-sysroot=/opt/codesourcery/arm-none-eabi --with-build-sysroot=/scratch/sandr
- a/lite/eabi/install/host-i686-mingw32/arm-none-eabi --with-libiconv-prefix=/scratch/sandra/lite/eabi/obj/host-libs-2008q1-126-arm-none-eabi-i686-mingw32/usr --enable-poison-system-directories --with-build-time-tools=/scratch/sandra/lite/eabi/obj/tools-i686-pc-linux-gnu-2008q1-126
- -arm-none-eabi-i686-mingw32/arm-none-eabi/bin --with-build-time-tools=/scratch/sandra/lite/eabi/obj/tools-i686-pc-linux-gnu-2008q1-126-arm-none-eabi-i686-mingw32/arm-none-eabi/bin
- Thread model: single
- gcc version 4.2.3 (Sourcery G++ Lite 2008q1-126)

5. Lets build by typing: cs-make
- output:
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Calibrat.o Calibrat.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Draw.o Draw.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Files.o Files.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Function.o Function.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Interrupt.o Interrupt.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Main.o Main.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Menu.o Menu.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Process.o Process.c
- arm-none-eabi-gcc -mcpu=cortex-m3 -mthumb  -c -o BIOS.o BIOS.S
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o startup.o startup.c
- arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o stm32f10x_nvic.o stm32f10x_nvic.c
- arm-none-eabi-as   -o cortexm3_macro.o cortexm3_macro.s
- arm-none-eabi-gcc -o app1.elf Calibrat.o Draw.o Files.o Function.o Interrupt.o Main.o Menu.o Process.o BIOS.o startup.o stm32f10x_nvic.o cortexm3_macro.o -mcpu=cortex-m3 -lc -mthumb -march=armv7 -mfix-cortex-m3-ldrd -msoft-float -nostartfiles -Wl,-Map,app1.map -T app1.lds
- arm-none-eabi-objcopy -O ihex app1.elf app1.hex
- rm app1.elf

6. You should find the compiled firmware file app1.hex (423,697 bytes)
- Put your DS203 into DFU mode (press and hold >|| button and power on) and copy the app1.hex to drive.
