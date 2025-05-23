# imgproxy-go

NOTE:  A clone of the unitedwardrobe library to test the base64 URL-safe encoding method (base64.RawURLEncoding).
The current version failed with encoding the path "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2F3M1nb8b_wuN94uxrdJ88eacQtp3d8KEB1OZ68DA13Z9iQzKSaif84Y&s"
as example.

A Go client library to generate urls for imgproxy services.

Based on https://docs.imgproxy.net/

**Note:** This library is not feature complete.

## Usage

```go
  package main

  import (
    "fmt"

    "github.com/unitedwardrobe/imgproxy-go"
  )

  func main() {
    ip, err := imgproxy.NewImgproxy(imgproxy.Config{
      BaseURL:       "http://localhost",
      SignatureSize: 15,
      Key:           hex.EncodeToString([]byte("key")),
      Salt:          hex.EncodeToString([]byte("salt")),
      EncodePath:    false,
    })
    if err != nil {
      panic(err)
    }

    url, err := ip.
      Builder().
      Resize(imgproxy.ResizingTypeFill, 123, 456, true, false).
      DPR(10).
      Format("png").
      Generate("path/to/my/image.jpg")
    if err != nil {
      panic(err)
    }

    fmt.Println(url) // http://localhost/448bHumukUmn0qpKBY2z/dpr:10/f:png/rs:fill:123:456:1:0/plain/path/to/my/image.jpg
  }
```

## Tests

```bash
  $ go test
```

## License

This project is licensed under the [MIT License](LICENSE.md).
