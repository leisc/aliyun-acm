# Aliyun ACM

*maintainer: CJK <regan.cjk@gmail.com>*

## Usage

```go
import "gitlab.xinghuolive.com/golang/aliyun-acm"

var client acm.Client

func init() {
    // Setup once.
	client = acm.Setup(
		"EndPoint",
		"Tenant", // Use tenant to separate deployment environment.
		"AccessKey",
		"SecretKey",
	)

    // Get static config.
    value := client.GetConfig("DEFAULT_GROUP", "dataID")
    // Note that value has been decoded from GBK to UTF-8.
    fmt.Println(value)

    // Listen on dynamic config in goroutine
	go client.Listen("DEFAULT_GROUP", "dataID", func(newValue string) {
        // Do something with new config value while update.
		fmt.Println(newValue)
	})
}
```
