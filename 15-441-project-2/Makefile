TOP_DIR = .
INC_DIR = $(TOP_DIR)/inc
SRC_DIR = $(TOP_DIR)/src
BUILD_DIR = $(TOP_DIR)/build
CC=gcc
FLAGS = -pthread -fPIC -g -ggdb -Wall -DDEBUG -I$(INC_DIR)
OBJS = $(BUILD_DIR)/cmu_packet.o \
	$(BUILD_DIR)/cmu_tcp.o \
	$(BUILD_DIR)/backend.o

default:all
all: server client testing_server

$(BUILD_DIR)/%.o: $(SRC_DIR)/%.c
	$(CC) $(FLAGS) -c -o $@ $<

server: $(OBJS)
	$(CC) $(FLAGS) $(SRC_DIR)/server.c -o server $(OBJS)

client: $(OBJS)
	$(CC) $(FLAGS) $(SRC_DIR)/client.c -o client $(OBJS)

testing_server: $(OBJ)
	$(CC) $(FLAGS) tests/testing_server.c -o tests/testing_server $(OBJS)

format:
	clang-format -i src/backend.c
	clang-format -i src/cmu_tcp.c

test:
	sudo python3 tests/test_cp1.py
	# sudo python3 tests/test_cp2.py

clean:
	-rm -f $(BUILD_DIR)/*.o peer client server
	-rm tests/testing_server
