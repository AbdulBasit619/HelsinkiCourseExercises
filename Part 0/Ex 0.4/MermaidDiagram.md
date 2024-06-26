# 0.4: New note diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

 Note right of browser: The user enters the new note and clicks the save button
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/new_note

    activate server
 Note right of browser: The server received the request and performs whole page reload
server->>browser: 
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: The HTML document
    deactivate server

 Note right of browser: The JS file is called first to process the additon and rendering of new note
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js


    activate server
    server-->>browser: The JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json

    activate server
    server-->>browser: [ {"content": "np", "date": "2024-06-25T19:53:18.239Z"}, ... ]
    deactivate server

    activate server
    Note right of browser: At the same time the browser calls the CSS file to start rendering the styles
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css

    server-->>browser: The CSS file
    deactivate server

    Note right of browser: The browser finally executes the callback function that renders the notes in addition to the new note
```