################################################################
#
# $Id:$
#
# $Log:$
#



ifeq ($(ROOT),)
    $(error Please, do first : source get_cross_env.sh)
else
    export $(ROOT)
endif

# Speedup compilation (choose 1~2 x number of CPU/Core)
export JOBS=-j6

BUSYBOX_VER=1.22.1

export LOGS=$(ROOT)/logs
export SOURCES=$(ROOT)/src
export INITRAMFS_ROOT=$(ROOT)/initramfs
export ARM_ROOT=arm-sysroot
export ARM_SYSROOT=$(ROOT)/$(ARM_ROOT)
export ARM_APPROOT=$(ARM_SYSROOT)/usr
export CONFIGS=$(ROOT)/configs
export TOMDIST=$(ROOT)/opentom_dist
export DOWNLOADS=Downloads

export ARMGCC=gcc-3.3.4_glibc-2.3.2
export CROSS=$(ROOT)/$(ARMGCC)
export T_ARCH=arm-linux
PREFIX=$(CROSS)/arm-linux/sys-root
export CFLAGS=-mlittle-endian -march=armv5te -mtune=arm9tdmi -mshort-load-bytes -fno-omit-frame-pointer -fno-optimize-sibling-calls -mno-thumb-interwork -O2 -I$(ARM_SYSROOT)/usr/include -L$(ARM_SYSROOT)/usr/lib
export CPPFLAGS=-march=armv5te -mtune=arm9tdmi -I$(PREFIX)/include -I$(PREFIX)/usr/include
LDFLAGS=-L$(PREFIX)/lib -L$(ARM_SYSROOT)/usr/lib 
COMPILO=$(CROSS)/bin/$(T_ARCH)

export CC=$(T_ARCH)-gcc
export CXX=$(T_ARCH)-g++
export LD=$(T_ARCH)-ld
export NM=$(T_ARCH)-nm -B
export AR=$(T_ARCH)-ar
export AS=$(T_ARCH)-as
export RANLIB=$(T_ARCH)-ranlib
export STRIP=$(T_ARCH)-strip
export OBJCOPY=$(T_ARCH)-objcopy

export CROSS_COMPILE=$(T_ARCH)-
export ARCH=arm


 # gcc or g++
CFLAGS+=-ggdb3 -Os
LDFLAGS+=-Wl,--gc-sections 
CFLAGS+=-ggdb3 -Wall -DNORMALUNIX -DLINUX -DSNDSERV -D_DEFAULT_SOURCE # -DUSEASM
LIBS+=-lm -lc -lX11

# subdirectory for objects
OBJDIR=tomtomdoom
OUTPUT=doom

SRC_DOOM = dummy.o am_map.o doomdef.o doomstat.o dstrings.o d_event.o d_items.o d_iwad.o d_loop.o d_main.o d_mode.o d_net.o f_finale.o f_wipe.o g_game.o hu_lib.o hu_stuff.o info.o i_cdmus.o i_endoom.o i_joystick.o i_scale.o i_sound.o i_system.o i_timer.o memio.o m_argv.o m_bbox.o m_cheat.o m_config.o m_controls.o m_fixed.o m_menu.o m_misc.o m_random.o p_ceilng.o p_doors.o p_enemy.o p_floor.o p_inter.o p_lights.o p_map.o p_maputl.o p_mobj.o p_plats.o p_pspr.o p_saveg.o p_setup.o p_sight.o p_spec.o p_switch.o p_telept.o p_tick.o p_user.o r_bsp.o r_data.o r_draw.o r_main.o r_plane.o r_segs.o r_sky.o r_things.o sha1.o sounds.o statdump.o st_lib.o st_stuff.o s_sound.o tables.o v_video.o wi_stuff.o w_checksum.o w_file.o w_main.o w_wad.o z_zone.o w_file_stdc.o i_input.o i_video.o doomgeneric.o doomgeneric_xlib.o
OBJS += $(addprefix $(OBJDIR)/, $(SRC_DOOM))

all:	 $(OUTPUT)

clean:
	rm -rf $(OBJDIR)
	rm -f $(OUTPUT)
	rm -f $(OUTPUT).gdb
	rm -f $(OUTPUT).map

$(OUTPUT):	$(OBJS)
	@echo [Linking $@]
	$(VB)$(CC) $(CFLAGS) $(LDFLAGS) $(OBJS) \
	-o $(OUTPUT) $(LIBS) -Wl,-Map,$(OUTPUT).map
	@echo [Size]
	-$(CROSS_COMPILE)size $(OUTPUT)

$(OBJS): | $(OBJDIR)

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(OBJDIR)/%.o:	%.c
	@echo [Compiling $<]
	$(VB)$(CC) $(CFLAGS) -c $< -o $@

print:
	@echo OBJS: $(OBJS)
