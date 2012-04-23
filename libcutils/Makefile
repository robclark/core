
targetSmpFlag := -DANDROID_SMP=1

commonSources := \
	array.c \
	hashmap.c \
	atomic.c \
	native_handle.c \
	buffer.c \
	socket_inaddr_any_server.c \
	socket_local_client.c \
	socket_local_server.c \
	socket_loopback_client.c \
	socket_loopback_server.c \
	socket_network_client.c \
	sockets.c \
	config_utils.c \
	cpu_info.c \
	load_file.c \
	list.c \
	open_memstream.c \
	strdup16to8.c \
	strdup8to16.c \
	record_stream.c \
	process_name.c \
	properties.c \
	threads.c \
	sched_policy.c \
	iosched_policy.c \
	str_parms.c \
        abort_socket.c \
        selector.c \
        tztime.c \
#        zygote.c


# Shared and static library for target
# ========================================================
LOCAL_MODULE := libcutils.a
LOCAL_SRC_FILES := $(commonSources) \
#	ashmem-dev.c \
	mq.c \
	android_reboot.c \
	partition_utils.c \
	uevent.c \
	qtaguid.c \
	klog.c
LOCAL_SRC_FILES += memory.c

LOCAL_C_INCLUDES := $(KERNEL_HEADERS)
LOCAL_STATIC_LIBRARIES := liblog
LOCAL_CFLAGS += $(targetSmpFlag)

################################

OBJS = $(LOCAL_SRC_FILES:.c=.o)
CFLAGS = -marm $(LOCAL_CFLAGS) -I../include -I. -DHAVE_PTHREADS=1

%.o: %.c
	gcc -g -c -fPIC $(CFLAGS) $(LFLAGS) $< -o $@

$(LOCAL_MODULE): $(OBJS)
	ar rcs $@ $<
	ranlib $@

clean:
	rm -f $(LOCAL_MODULES) *.o

