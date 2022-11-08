# Challenge 21

## We test our API

I added testing of some controllers using **Jest**, generated the Requests with **axios**.

```console
test
└── controllers
    ├── other.test.js
    └── product.test.js
```

To run the tests you can execute the following commands _(the server must be up)_

### `npm run test`

This command will display the results by terminal.


### `npm run testReport`

It will show the results by terminal and will also save a file with the results in the folder **_testresults_**, the file is identified with the date it was run.

For example, on July 13, 2022 I ran the tests, **`TestResults_2022-07-13.txt`** was generated in the `testresults` folder

```console
cat testresults/TestResults_2022-07-13.txt
                                                       
PASS test/controllers/other.test.js
PASS test/controllers/product.test.js

Test Suites: 2 passed, 2 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        0.794 s, estimated 1 s
Ran all test suites.
```