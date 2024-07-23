---
title: Table Driven Tests
date: 07-22-2024
---
- https://go.dev/wiki/TableDrivenTests
- Mentioned in Learn Go with tests [here](https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/structs-methods-and-interfaces#further-refactoring)
```go
var flagtests = []struct {
    in  string
    out string
}{
    {"%a", "[%a]"},
    {"%-a", "[%-a]"},
    {"%+a", "[%+a]"},
    {"%#a", "[%#a]"},
    {"% a", "[% a]"},
    {"%0a", "[%0a]"},
    {"%1.2a", "[%1.2a]"},
    {"%-1.2a", "[%-1.2a]"},
    {"%+1.2a", "[%+1.2a]"},
    {"%-+1.2a", "[%+-1.2a]"},
    {"%-+1.2abc", "[%+-1.2a]bc"},
    {"%-1.2abc", "[%-1.2a]bc"},
}
func TestFlagParser(t *testing.T) {
    var flagprinter flagPrinter
    for _, tt := range flagtests {
        t.Run(tt.in, func(t *testing.T) {
            s := Sprintf(tt.in, &flagprinter)
            if s != tt.out {
                t.Errorf("got %q, want %q", s, tt.out)
            }
        })
    }
}
```

Defining test input and output and looping through each case as part of a test. a.k.a. TDT.