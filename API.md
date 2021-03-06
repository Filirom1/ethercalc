FORMAT: 1A
HOST: https://www.ethercalc.org/

# EtherCalc

API for real-time collaborative spreadsheets.

* Overview: http://ethercalc.net/
* 中文版: http://ethercalc.tw/

# Index [/_]

## Create Page [POST]

Takes a JSON structure with `room` and `snapshot` fields.

Replaces the page with a serialization in Socialtext save format.
If `room` is not specified, returns a new page.

+ Request (application/json)

    ```json
    { "room": "test"
    , "snapshot": "..."
    }
    ```

+ Response 201
    + Headers

        ```
        Location: /_/test
        ```

## Create from CSV [POST]

Takes a CSV structure that contains the new spreadsheet's content.

+ Request (text/csv)
+ Response 201

## Create from SocialCalc [POST]

Takes a SocialCalc serialization format that contains the new spreadsheet's content.

+ Request (text/x-socialcalc)
+ Response 201

# Page [/_/{id}]

## Page Content [GET]

Fetch the page as a serialization in SocialCalc save format.

+ Response 200 (text/x-socialcalc)

## Overwrite with CSV [PUT]

Replace the page with a serialization in CSV format.

+ Request (text/csv)
+ Response 200

## Overwrite with SocialCalc [PUT]

Replace the page with a serialization in SocialCalc save format.

+ Request (text/x-socialcalc)
+ Response 200

## Post Commands [POST]

Takes a JSON structure with a `command` field (either as a string
or an array of strings), or a plain-text command string.

Runs one or more commands specified in the `command` field.

To find out which command corresponds to which spreadsheet actions,
perform the actions on the web interface and check the _Audit_ tab
for the recorded commands.

+ Request (application/json)
+ Response 202

    ```json
    {"command": "..."}
    ```

## Append Rows [POST]

Takes a CSV structure that contains fields to be appended to the first column after the last row.

+ Parameters
    + row (optional, integer) ... If specified, insert and paste on the specified row instead of the last.
+ Request (text/csv)
+ Response 200

# Page Cells [/_/{id}/cells]

## GET

Returns a JSON representation of all defined cells in the page.

+ Response 200 (application/json)

# Cell Value [/_/{id}/cells/{coord}]

## GET

Returns a JSON representation of a single cell in the page.

+ Response 200 (application/json)

# HTML Export [/_/{id}.html]

## GET

Returns a HTML rendering of the page. (GET `/_/{id}/html` also works.)

+ Response 200 (text/html)

# CSV Export [/_/{id}.csv]

## GET

Returns a CSV rendering of the page. (GET `/_/{id}/csv` also works.)

+ Response 200 (text/csv)
