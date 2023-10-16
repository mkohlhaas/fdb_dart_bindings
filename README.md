```shell
dart run ffigen
```

StateMachine (?): Or does FDB returns appropriate error messages?
  - APIVersion must be called first
  - Setting network options must be called before calling SetupNetwork().
  - Calling runNetwork() must be called after SetupNetwork().
  - ...

Singleton:
  - final fdbc = FDBC(DynamicLibrary.open('libfdb_c.so'));
  - from https://github.com/apple/foundationdb/blob/main/bindings/ruby/lib/fdbimpl.rb
    Use this package to find architecture: x86_64, ARM64, ...
    - https://pub.dev/packages/system_info2

      import 'dart:io' show Platform;
      var so = switch(Platform.operatingSystem) {
          case 'linux': 'libfdb_c.so';
          case 'macos': 'libfdb_c.dylib';
          case 'windows': 'fdb_c.dll';
        }


Classes:
  - FDB (fdb.go; "global" functions)
    - APIVersion()
    - OpenDatabase()
    - StartNetwork()
    - ...
  - Database (database.go)
    - Close()
    - CreateTransaction()
    - Transact()
    - OpenTenant() (see Tenant class)
    - SetOptions:
      - see FDBTransactionOption
        - SetLocationCacheSize
        - SetMaxWatches
        - ...
    - ...
  - Tenant
    - Destroy()
    - CreateTransaction()
  - Transaction
    - Transact()
    - GetRange()
    - SetOptions:
      - SetLocalAddress()
      - SetClusterFile()
    - ...
  - Network (generated.go)
    - SetupNetwork()
    - StartNetwork()
    - RunNetwork()
    - StopNetwork()
    - SetOptions:
      - see FDBNetworkOption
        - SetLocalAddress()
        - SetClusterFile()
        - ...
    - ...
  - FDBException
    - toString()
  - Future
    - BlockUntilReady()
    - IsReady()
    - ...
  - Tuples
  - Directory
  - Subspace
