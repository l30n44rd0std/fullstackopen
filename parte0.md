# Exercício 0.4

sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document (da página SPA)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: o arquivo css
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: o arquivo JavaScript (spa.js)
    deactivate server

    Note right of browser: O navegador começa a executar o código JavaScript (spa.js)<br>que busca os dados JSON iniciais do servidor.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "..." }, ...]
    deactivate server

    Note right of browser: O navegador executa a função de callback que<br>renderiza as notas iniciais na página.

# Exercício 0.5

sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document (da página SPA)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: o arquivo css
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: o arquivo JavaScript (spa.js)
    deactivate server

    Note right of browser: O navegador começa a executar o código JavaScript (spa.js)<br>que busca os dados JSON iniciais do servidor.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "..." }, ...]
    deactivate server

    Note right of browser: O navegador executa a função de callback que<br>renderiza as notas iniciais na página.

# Exercício 0.6

sequenceDiagram
    participant browser
    participant server

    Note left of browser: Usuário está na página SPA (/spa).<br>Ele digita texto no campo<br>e clica no botão "Save".

    Note right of browser: O JavaScript (spa.js) intercepta o evento de submit do formulário.<br>Ele previne o comportamento padrão do navegador (preventDefault()).<br>Cria um objeto de nota (ex: {content: "Nova nota SPA", date: new Date()}).

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    Note over browser,server: Corpo da requisição contém a nova nota como JSON.<br>Cabeçalho Content-Type é 'application/json'.
    activate server

    Note right of server: Servidor recebe os dados JSON,<br>processa a nova nota e a armazena.

    server-->>browser: HTTP 201 Created
    Note over browser,server: Resposta não contém HTML para redirecionamento.<br>Pode conter a nota criada como JSON no corpo (opcional).
    deactivate server

    Note right of browser: O JavaScript (spa.js) recebe a confirmação 201.<br>Ele atualiza a interface do usuário (DOM)<br>adicionando a nova nota à lista visível na página.<br>NENHUM RECARREGAMENTO DE PÁGINA OCORRE.