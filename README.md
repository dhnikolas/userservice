#Generate gRPC client and server
protoc --go-grpc_out=. --go_out=. *.proto 

#Generate http reverse proxy gateway
protoc --grpc-gateway_out ./gateway \
 --grpc-gateway_opt logtostderr=true \
 --grpc-gateway_opt paths=source_relative \
 --grpc-gateway_opt generate_unbound_methods=true *.proto

#Generate gateway swagger
protoc -I . --openapiv2_out ./gateway --openapiv2_opt logtostderr=true *.proto