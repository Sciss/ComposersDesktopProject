SUBDIRS=man

lib_LTLIBRARIES = libaaio.la

libaaio_la_SOURCES =  aaio.c

include_HEADERS = aaio.h

EXTRA_DIST=aaio2.c aaio1.c README

CFLAGS=-Wall -pedantic -std=c99

libaaio_la_LDFLAGS = -version-info 1:1:1

# Current is the version of the interface the library
# 	implements. Whenever a new function is added, or its name
# 	changed, or the number or type of its parameters (the
# 	prototype -- in libraries we call this the function
# 	signature), this number goes up. And it goes up exactly by
# 	one. 

# Revision is the revision of the implementation of this interface,
# 	 i.e., when you change the library by only modifying code
# 	 inside the functions (fixing bugs, optimizing internal
# 	 behavior, or adding/removing/changing signatures of functions
# 	 that are private to the library -- used only internally) you
# 	 raise the revision number only. 

# Age is the difference between the newest and oldest interface the
#     library currently implements. Let's say you had 8 versions of your
#     library's interface, 0 through 7. You are now on the 4th revision
#     of the 8th interface, that is, 7:3:X (remember we start counting
#     on zero). And when you had to make choices for what old interfaces
#     you would keep support -- for backward compatibility purposes, you
#     chose to keep support for interfaces 5, 6 and (obviously) the
#     current, 7. The libtool version of your library would be 7:3:2 ,
#     because the Age is 7-5 = 2.  
