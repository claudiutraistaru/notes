
# [Protobuf](https://developers.google.com/protocol-buffers/)

- Message encoding more concise and quick than XML.
- The client need to use protobuf code generation tool to utilize this library.
- protobuf's unique numbered tag looks confusing. But it actually is quick useful. It is used for future extention of message definition.

    ```proto
    message SearchRequest {
    required string query = 1;
    optional int32 page_number = 2;
    optional int32 result_per_page = 3;
    }
    // later extended to
    message SearchRequest {
    required string query = 1;
    optional int32 page_number = 2;
    optional int32 result_per_page = 3;
    optional int32 new_data = 4;
    }
    ```

    snippet copied from [here](https://stackoverflow.com/a/26826460/6759854)

    Another example in libp2p's kad-dht Go implementation is [here](https://github.com/libp2p/go-libp2p-kad-dht/blob/master/pb/dht.proto). Some of the field IDs were skipped for future use reservation.

- protobuf encoding is fascinating. 6 predefined __wire types__. Base 128 varint is a non-fixed-size integer. [Here is a great stackoverflow answer explains pro and cons of varint](https://stackoverflow.com/a/24642169/6759854).