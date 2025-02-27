
# go-SuperFastScan

A very simple and fast port scanner written in Go.

## Features

-   Scans all 65,535 ports quickly using Goroutines.
-   Simple and minimalistic code.
-   Easily customizable IP address.
-   Good for CTF


## Usage

Modify the target IP address inside the source code before running the scanner:

```go
ip := "127.0.0.1" // Change this to the IP you want to scan
```

Run the scanner with:

```sh
$ go run superFastScan.go
```

Alternatively, you can build an executable and run it:

```sh
$ go build -o scanner superFastScan.go
$ ./scanner
```

## Code Example

```go
package main

import (
	"fmt"
	"net"
	"sync"
)
func main() {
	var wg sync.WaitGroup
	for i := 1; i <= 65535; i++ {
		wg.Add(1)
		go func(j int) {
			defer wg.Done()
			ip := "127.0.0.1" // Change this to the IP you want to scan
			address := fmt.Sprintf("%s:%d", ip, j)
			conn, err := net.Dial("tcp", address)
			if err != nil {
				return
			}
			conn.Close()
			fmt.Printf("Port %d is open\n", j)
		}(i)
	}
	wg.Wait()
}
```

## Notes

-   Ensure you have permission to scan the target system.
-   Scanning networks without authorization may be illegal in some jurisdictions.
-   Modify the IP before use to avoid scanning localhost unintentionally.

## License

This project is licensed under the MIT License. Feel free to modify and distribute it.

----------

Happy scanning! 🚀
