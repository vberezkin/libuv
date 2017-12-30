cmake_minimum_required(VERSION 2.8)

include_directories(include src)

set(SRC
	src/fs-poll.c
	src/heap-inl.h
	src/inet.c
	src/queue.h
	src/threadpool.c
	src/uv-common.c
	src/uv-common.h
	src/version.c

	src/unix/async.c
	src/unix/atomic-ops.h
	src/unix/core.c
	src/unix/dl.c
	src/unix/fs.c
	src/unix/getaddrinfo.c
	src/unix/getnameinfo.c
	src/unix/internal.h
	src/unix/loop-watcher.c
	src/unix/loop.c
	src/unix/no-proctitle.c
	src/unix/pipe.c
	src/unix/poll.c
	src/unix/process.c
	src/unix/proctitle.c
	src/unix/pthread-fixes.c
	src/unix/signal.c
	src/unix/spinlock.h
	src/unix/stream.c
	src/unix/tcp.c
	src/unix/thread.c
	src/unix/timer.c
	src/unix/tty.c
	src/unix/udp.c

	include/pthread-barrier.h
	include/tree.h
	include/uv-version.h
	include/uv-errno.h
	include/uv-os390.h
	include/uv-threadpool.h
	include/uv.h
)

if (CMAKE_SYSTEM_NAME MATCHES "Android")
	set(SRC ${SRC}
		src/unix/android-ifaddrs.c
		src/unix/cygwin.c
		src/unix/linux-core.c
		src/unix/linux-inotify.c
		src/unix/linux-syscalls.c
		src/unix/linux-syscalls.h
		src/unix/procfs-exepath.c
		src/unix/sysinfo-loadavg.c
		src/unix/sysinfo-memory.c
		include/android-ifaddrs.h
		include/uv-linux.h
	)
elseif (APPLE)
	set(SRC ${SRC}
		src/unix/bsd-ifaddrs.c
		src/unix/darwin.c
		src/unix/fs.c
		src/unix/fsevents.c
		src/unix/kqueue.c
	)
endif()

add_library(uv STATIC ${SRC})
