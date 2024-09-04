sequenceDiagram
    participant User
    participant Browser
    participant Server
    
    User->>Browser: Writes note and clicks "Save"
    
    note right of Browser: Browser captures the input and triggers JavaScript event listener

    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note with note data
    activate Server
    
    note right of Server: Server processes the incoming data and stores the new note
    
    Server-->>Browser: HTTP 302 Redirect to /exampleapp/notes
    deactivate Server
    
    note right of Browser: Browser follows the redirect
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: HTML document
    deactivate Server
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: Updated JSON with the new note included
    deactivate Server
    
    note right of Browser: Browser updates the DOM to display the new note
