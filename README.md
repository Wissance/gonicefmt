## gonicefmt is a Most useful and readable code linter and formatter
This is **not an ultimate truth** **but our (M. Ushakov as `Wissance` CEO) own view** how go code must 
be formatted:

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
2. Arguments x-mas tree, consider we deal with function that has many arguments, i.e. 10, and many people
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
   Wow!!!! How it waste my time to scroll, in fucking 2023 we have wide displays with aspect ratio 16:9 (16 - width, 9 - height)
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


