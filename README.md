## Gonicefmt is a Most useful and readable code linter and formatter
This is **not an ultimate truth** **but our (M. Ushakov as `Wissance` CEO) own view** how go code must 
be formatted (see our `editorconfig` in REPO too):

### 1. Which linters could be replaced `gonicefmt` 

You could find linters related to formatting [here](https://github.com/golangci/awesome-go-linters)

There are following linters related to code formatting:
* `dedupimport` - Fix duplicate imports that have the same import path but different import names.
* `gofmt` - Gofmt formats Go programs.
* `gofumpt` - The tool is a modified fork of gofmt, enforcing a stricter format than gofmt.
* `goimports` - Goimports does everything that gofmt does. Additionally it checks unused imports.
* `unindent` - Report code that is unnecessarily indented

Some of these linters must be replaced due to they worse code readability and raise unnecessary errors
***i.e. empty line raise an error, nonsense!***

### 2. More elegant code formatting

1. People just thinking that if we got long literal string as `func` argument it should start from a new
   line, for us it seems useless function vertical spread:
   ```go
      func ProcessText(text string)
      
      // calling it
      ProcessText(
                 "This occurs because passing literal string is too long for zoomers to keep attention on it")
   ```
   
   This function call MUST be converted to more concise:
   ```go
   ProcessText("This occurs because passing literal string is too long for zoomers to keep attention on it")
   ```
   that is how it looks for the mentally healthy human.
2. **Arguments x-mas tree**, consider we deal with function that has many arguments, i.e. 10, and many people
   make vertical align for them in a following manner:
   ```go
   func Interact (hostName string, 
                  domain string,
                  userName string,
                  password string,
                  useTls bool,
                  tlsCerts *TlsCfg,
                  encoding string,
                  protocol string,
                  version string,
                  timeout int)
   // and call ...
   Interact("localhost",
            "admin",
            "admin",
            false,
            nil,
            "utf-8",
            "grpc",
            "1.1",
            "2500")
   ```
   Wow!!!! How ***it waste my time to scroll***, in fucking 2023 we have wide displays with aspect ratio 16:9 (16 - width, 9 - height)
   how this simple code is vertically spread, it awfully awesome. Therefore we must transform it to 
   something like this:
   ```go
   func Interact (hostName string, domain string, userName string, password string,
                  useTls bool, tlsCerts *TlsCfg, encoding string, protocol string, 
                  version string, timeout int)
   
   // and call:
   Interact("localhost", "admin", "admin", false, nil, "utf-8", "grpc", "1.1", "2500")
   
   ```
   
   This one looks pretty compact (but maybe not for a zoomer?)
3. **Function arguments alignment**. The following example i suppose is bad too:
   ```go
   myFunc("1111", myFunc2("localhost", "admin", "admin", 
       9990, 5678))
   ```
   it should be aligned as follows:
      ```go
   myFunc("1111", myFunc2("localhost", "admin", "admin", 
                          9990, 5678))
   ```
4. **Optional formatting style**. I discovered following issues:
  * empty lines, it is NOT an error;
  * space after commentary `/`, `//This is comment` is not an error and putting space after last `/`
    must not be required