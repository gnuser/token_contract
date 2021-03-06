cmake_minimum_required(VERSION 2.8)

project(token_contract)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_BUILD_TYPE "Debug")
include_directories(./src)

set(contract_src src/contract/contractobject.cpp
            src/contract/txparse.cpp
            src/contract/designcontract.cpp
            src/contract/contract.cpp)

set(contract_machine_src src/contract_machine/contractparse.cpp
            src/contract_machine/actionobject.cpp
            src/contract_machine/machinestack.cpp
            src/contract_machine/action.cpp)

set(data_src src/data/db_mysql.cpp)

set(transaction_src src/transaction/txobject.cpp
                    src/transaction/tx.cpp)

set(interactive_src src/interactive/tokeninteractive.cpp
                    src/interactive/interactive.cpp)


set(tokend_src ${contract_src}
            ${contract_machine_src}
            ${data_src}
            ${transaction_src}
            ${interactive_src}
            src/consumer.cpp
            src/consumer_handler.cpp
            src/producer.cpp
            src/init.cpp
            src/httpserver.cpp
            src/parsetx.cpp
            src/logic.cpp
            src/logicparsetx.cpp
            src/logickafka.cpp
            src/tokend.cpp)

set(scanblock_src ${contract_src}
            ${contract_machine_src}
            ${data_src}
            ${transaction_src}
            ${interactive_src}
            src/logic.cpp
            src/logicparsetx.cpp
            src/logickafka.cpp
            src/consumer.cpp
            src/consumer_handler.cpp
            src/producer.cpp
            src/init.cpp
            src/parsetx.cpp
            src/scanblock.cpp)

set(tokencli_src ${contract_src}
            ${contract_machine_src}
            ${data_src}
            ${transaction_src}
            ${interactive_src}
            src/consumer.cpp
            src/consumer_handler.cpp
            src/producer.cpp
            src/init.cpp
            src/httpserver.cpp
            src/parsetx.cpp
            src/logic.cpp
            src/logicparsetx.cpp
            src/logickafka.cpp
			src/logiccli.cpp
            src/tokencli.cpp)

#
#set(lib_src ${transation_src}
#            ${contract_src}
#            ${contract_machine_src}
#            ${data_src}
#            ${interactive_src}
#            src/init.cpp)

#set(test_src src/init.cpp)

#ADD_LIBRARY (token_contract STATIC ${lib_src})
#target_link_libraries(token_contract c rt  curl  pthread event  mysqlclient boost_system boost_program_options glog bitcoin)

add_executable(tokend ${tokend_src})
target_link_libraries(tokend c rt  curl  pthread event  mysqlclient boost_system boost_program_options glog bitcoin rdkafka rdkafka++)

add_executable(scanblock ${scanblock_src})
target_link_libraries(scanblock c rt  curl  pthread event  mysqlclient boost_system boost_program_options glog bitcoin rdkafka rdkafka++)

add_executable(tokencli ${tokencli_src})
target_link_libraries(tokencli c rt  curl  pthread event  mysqlclient boost_system boost_program_options glog bitcoin rdkafka rdkafka++)

#add_executable(test_logic ${scanblock_src})
#target_link_libraries(scanblock c rt  curl  pthread event  mysqlclient boost_system boost_program_options glog bitcoin rdkafka rdkafka++)

#MESSAGE(STATUS "Project Directory: ${CMAKE_CURRENT_BINARY_DIR}")

#set(LIB_TOKEN_CONTRACT_PATH ${CMAKE_CURRENT_BINARY_DIR})

#add_subdirectory(src/test)
#add_subdirectory(src/token_daemon)

