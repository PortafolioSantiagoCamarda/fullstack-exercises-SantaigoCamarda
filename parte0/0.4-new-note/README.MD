sequenceDiagram
participant browser
participant server


Note right of browser: El usuario escribe la nota y hace clic en "Save"


%% 1) ENVÍO DEL FORMULARIO
browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
activate server
Note left of server: Guarda la nota y decide redirigir (patrón PRG)
server-->>browser: 302 Found (Location: /exampleapp/notes)
deactivate server


%% 2) REDIRECCIÓN (PRG)
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
activate server
server-->>browser: HTML document
deactivate server


%% 3) ASSETS
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
server-->>browser: the css file


browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
server-->>browser: the JavaScript file


%% 4) DATA + RENDER
Note right of browser: El JS se ejecuta y solicita los datos
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: [ { "content": "...", "date": "..." }, ... ]
deactivate server


Note right of browser: El callback renderiza la lista de notas (incluye la nueva)