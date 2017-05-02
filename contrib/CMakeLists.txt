project(contrib)

file(GLOB libevent_src libevent/*.c)

ADD_CUSTOM_TARGET(libevent ALL 
	COMMAND echo -n
	DEPENDS libevent-bin/Makefile ${CMAKE_BUILD_DIR}/lib/libevent.a
	)

ADD_CUSTOM_COMMAND(OUTPUT libevent-bin/Makefile
	COMMAND mkdir -p libevent-bin && cd libevent-bin && ${CMAKE_SOURCE_DIR}/contrib/libevent/configure
	)

ADD_CUSTOM_COMMAND(OUTPUT ${CMAKE_BUILD_DIR}/lib/libevent.a
	COMMAND cd libevent-bin && make libevent.la && cp .libs/libevent.a ${CMAKE_BUILD_DIR}/lib
	DEPENDS libevent-bin/Makefile ${libevent_src} 
	)

