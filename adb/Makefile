# makefile to build adbd natively for ubuntu:

LOCAL_SRC_FILES := \
	adb.c \
	backup_service.c \
	fdevent.c \
	transport.c \
	transport_local.c \
	transport_usb.c \
	sockets.c \
	services.c \
	file_sync_service.c \
	jdwp_service.c \
	framebuffer_service.c \
	remount_service.c \
	usb_linux_client.c \
	log_service.c \
	utils.c

LOCAL_CFLAGS := -O2 -g -DADB_HOST=0 -Wall -Wno-unused-parameter
LOCAL_CFLAGS += -D_XOPEN_SOURCE -D_GNU_SOURCE

# TODO: This should probably be board specific, whether or not the kernel has
# the gadget driver; rather than relying on the architecture type.
#ifeq ($(TARGET_ARCH),arm)
LOCAL_CFLAGS += -DANDROID_GADGET=1
#endif

LOCAL_MODULE := adbd

LOCAL_FORCE_STATIC_EXECUTABLE := true
LOCAL_MODULE_PATH := $(TARGET_ROOT_OUT_SBIN)
LOCAL_UNSTRIPPED_PATH := $(TARGET_ROOT_OUT_SBIN_UNSTRIPPED)

LOCAL_STATIC_LIBRARIES := libcutils libc

################################

OBJS = $(LOCAL_SRC_FILES:.c=.o)
CFLAGS = -marm $(LOCAL_CFLAGS) -I../include -I. -DHAVE_PTHREADS=1

%.o: %.c
	gcc -g -c -fPIC $(CFLAGS) $(LFLAGS) $< -o $@

$(LOCAL_MODULE): $(OBJS)
	gcc -fPIC -static $^ -L ../libcutils/*.o -lpthread -o $@

clean:
	rm -f $(LOCAL_MODULES) *.o

