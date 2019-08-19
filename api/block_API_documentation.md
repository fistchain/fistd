
## APIs

The fistchain block explorer is exposed by two APIs: a fistchain implementation of
the [Insight API](https://github.com/bitpay/insight-api), and its
own JSON HTTP API. The Insight API uses the path prefix `/insight/api`. The
fistchain API uses the path prefix `/api`.
File downloads are served from the `/download` path.

### Insight API

The [Insight API](https://github.com/bitpay/insight-api) is accessible via HTTP
via REST or WebSocket.

See the [Insight API documentation](api/Insight_API_documentation.md) for
further details.

### fistchain API

The fistchain API is a REST API accessible via HTTP. To call the fistchain API, use
the `/api` path prefix.

#### Endpoint List

| Best block           | Path                                | Type                                  |
| -------------------- | ----------------------------------- | ------------------------------------- |
| Summary              | `/block/best?txtotals=[true|false]` | `types.BlockDataBasic`                |
| Stake info           | `/block/best/pos`                   | `types.StakeInfoExtended`             |
| Header               | `/block/best/header`                | `dcrjson.GetBlockHeaderVerboseResult` |
| Raw Header (hex)     | `/block/best/header/raw`            | `string`                              |
| Hash                 | `/block/best/hash`                  | `string`                              |
| Height               | `/block/best/height`                | `int`                                 |
| Raw Block (hex)      | `/block/best/raw`                   | `string`                              |
| Size                 | `/block/best/size`                  | `int32`                               |
| Subsidy              | `/block/best/subsidy`               | `types.BlockSubsidies`                |
| Transactions         | `/block/best/tx`                    | `types.BlockTransactions`             |
| Transactions Count   | `/block/best/tx/count`              | `types.BlockTransactionCounts`        |
| Verbose block result | `/block/best/verbose`               | `dcrjson.GetBlockVerboseResult`       |

| Block X (block index) | Path                  | Type                                  |
| --------------------- | --------------------- | ------------------------------------- |
| Summary               | `/block/X`            | `types.BlockDataBasic`                |
| Stake info            | `/block/X/pos`        | `types.StakeInfoExtended`             |
| Header                | `/block/X/header`     | `dcrjson.GetBlockHeaderVerboseResult` |
| Raw Header (hex)      | `/block/X/header/raw` | `string`                              |
| Hash                  | `/block/X/hash`       | `string`                              |
| Raw Block (hex)       | `/block/X/raw`        | `string`                              |
| Size                  | `/block/X/size`       | `int32`                               |
| Subsidy               | `/block/best/subsidy` | `types.BlockSubsidies`                |
| Transactions          | `/block/X/tx`         | `types.BlockTransactions`             |
| Transactions Count    | `/block/X/tx/count`   | `types.BlockTransactionCounts`        |
| Verbose block result  | `/block/X/verbose`    | `dcrjson.GetBlockVerboseResult`       |

| Block H (block hash) | Path                       | Type                                  |
| -------------------- | -------------------------- | ------------------------------------- |
| Summary              | `/block/hash/H`            | `types.BlockDataBasic`                |
| Stake info           | `/block/hash/H/pos`        | `types.StakeInfoExtended`             |
| Header               | `/block/hash/H/header`     | `dcrjson.GetBlockHeaderVerboseResult` |
| Raw Header (hex)     | `/block/hash/H/header/raw` | `string`                              |
| Height               | `/block/hash/H/height`     | `int`                                 |
| Raw Block (hex)      | `/block/hash/H/raw`        | `string`                              |
| Size                 | `/block/hash/H/size`       | `int32`                               |
| Subsidy              | `/block/best/subsidy`      | `types.BlockSubsidies`                |
| Transactions         | `/block/hash/H/tx`         | `types.BlockTransactions`             |
| Transactions count   | `/block/hash/H/tx/count`   | `types.BlockTransactionCounts`        |
| Verbose block result | `/block/hash/H/verbose`    | `dcrjson.GetBlockVerboseResult`       |

| Block range (X < Y)                     | Path                      | Type                     |
| --------------------------------------- | ------------------------- | ------------------------ |
| Summary array for blocks on `[X,Y]`     | `/block/range/X/Y`        | `[]types.BlockDataBasic` |
| Summary array with block index step `S` | `/block/range/X/Y/S`      | `[]types.BlockDataBasic` |
| Size (bytes) array                      | `/block/range/X/Y/size`   | `[]int32`                |
| Size array with step `S`                | `/block/range/X/Y/S/size` | `[]int32`                |

| Transaction T (transaction id)       | Path                         | Type               |
| ------------------------------------ | ---------------------------- | ------------------ |
| Transaction details                  | `/tx/T?spends=[true\|false]` | `types.Tx`         |
| Transaction details w/o block info   | `/tx/trimmed/T`              | `types.TrimmedTx`  |
| Inputs                               | `/tx/T/in`                   | `[]types.TxIn`     |
| Details for input at index `X`       | `/tx/T/in/X`                 | `types.TxIn`       |
| Outputs                              | `/tx/T/out`                  | `[]types.TxOut`    |
| Details for output at index `X`      | `/tx/T/out/X`                | `types.TxOut`      |
| Vote info (ssgen transactions only)  | `/tx/T/vinfo`                | `types.VoteInfo`   |
| Ticket info (sstx transactions only) | `/tx/T/tinfo`                | `types.TicketInfo` |
| Serialized bytes of the transaction  | `/tx/hex/T`                  | `string`           |
| Same as `/tx/trimmed/T`              | `/tx/decoded/T`              | `types.TrimmedTx`  |

| Transactions (batch)                                    | Path                        | Type                |
| ------------------------------------------------------- | --------------------------- | ------------------- |
| Transaction details (POST body is JSON of `types.Txns`) | `/txs?spends=[true\|false]` | `[]types.Tx`        |
| Transaction details w/o block info                      | `/txs/trimmed`              | `[]types.TrimmedTx` |

| Address A                                                               | Path                            | Type                  |
| ----------------------------------------------------------------------- | ------------------------------- | --------------------- |
| Summary of last 10 transactions                                         | `/address/A`                    | `types.Address`       |
| Number and value of spent and unspent outputs                           | `/address/A/totals`             | `types.AddressTotals` |
| Verbose transaction result for last <br> 10 transactions                | `/address/A/raw`                | `types.AddressTxRaw`  |
| Summary of last `N` transactions                                        | `/address/A/count/N`            | `types.Address`       |
| Verbose transaction result for last <br> `N` transactions               | `/address/A/count/N/raw`        | `types.AddressTxRaw`  |
| Summary of last `N` transactions, skipping `M`                          | `/address/A/count/N/skip/M`     | `types.Address`       |
| Verbose transaction result for last <br> `N` transactions, skipping `M` | `/address/A/count/N/skip/M/raw` | `types.AddressTxRaw`  |
| Transaction inputs and outputs as a CSV formatted file.                 | `/download/address/io/A`        | CSV file              |

The full ticket pool endpoints accept the URL query `?sort=[true\|false]` for
requesting the tickets array in lexicographical order. If a sorted list or list
with deterministic order is _not_ required, using `sort=false` will reduce
server load and latency. However, be aware that the ticket order will be random,
and will change each time the tickets are requested.

<sup>\*</sup>For the pool info block range endpoint that accepts the `arrays`
url query, a value of `true` will put all pool values and pool sizes into
separate arrays, rather than having a single array of pool info JSON objects.
This may make parsing more efficient for the client.


All JSON endpoints accept the URL query `indent=[true|false]`. For example,
`/stake/diff?indent=true`. By default, indentation is off. The characters to use
for indentation may be specified with the `indentjson` string configuration
option.
