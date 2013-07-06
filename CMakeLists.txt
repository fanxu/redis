project(redis C)
cmake_minimum_required(VERSION 2.8)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -pedantic -Wall")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -gdwarf-3")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DUSE_JEMALLOC")

include_directories(${CMAKE_SOURCE_DIR}/deps/jemalloc/include)
link_directories(${CMAKE_SOURCE_DIR}/deps/jemalloc/lib)
include_directories(${CMAKE_SOURCE_DIR}/deps/hiredis)
link_directories(${CMAKE_SOURCE_DIR}/deps/hiredis)
include_directories(${CMAKE_SOURCE_DIR}/deps/linenoise)
include_directories(${CMAKE_SOURCE_DIR}/deps/lua/src)
link_directories(${CMAKE_SOURCE_DIR}/deps/lua/src)

# redis-server
set(REDIS_SERVER_SRC_LIST
    src/adlist.c
    src/ae.c
    src/anet.c
    src/dict.c
    src/redis.c
    src/sds.c
    src/zmalloc.c
    src/lzf_c.c
    src/lzf_d.c
    src/pqsort.c
    src/zipmap.c
    src/sha1.c
    src/ziplist.c
    src/release.c
    src/networking.c
    src/util.c
    src/object.c
    src/db.c
    src/replication.c
    src/rdb.c
    src/t_string.c
    src/t_list.c
    src/t_set.c
    src/t_zset.c
    src/t_hash.c
    src/config.c
    src/aof.c
    src/pubsub.c
    src/multi.c
    src/debug.c
    src/sort.c
    src/intset.c
    src/syncio.c
    src/migrate.c
    src/endianconv.c
    src/slowlog.c
    src/scripting.c
    src/bio.c
    src/rio.c
    src/rand.c
    src/memtest.c
    src/crc64.c
    src/bitops.c
    src/sentinel.c
)
add_executable(redis-server ${REDIS_SERVER_SRC_LIST})
target_link_libraries(redis-server debug hiredis lua m pthread)
target_link_libraries(redis-server optimized hiredis lua jemalloc dl m pthread)
