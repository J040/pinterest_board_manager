# Personal Board Manager

Baixe as imagens de boards do Pinterest que você possui (ou que foram compartilhadas com você) em máxima qualidade, usando a API oficial do Pinterest (v5).

`Importante: este projeto só funciona com boards acessíveis à sua conta.`

### Recursos

Lista automaticamente os seus boards.

Faz paginação completa dos pins.

Escolhe a maior variante de imagem disponível; tenta a versão “originals” quando possível.

Recomeça downloads interrompidos e cria pastas automaticamente.

### Requisitos

`Python 3.9+`

`pip install requests tqdm`

Um token de acesso OAuth do Pinterest com escopos: boards:read e pins:read.

### Como funciona (resumo)

Você autoriza o app a ler seus boards/pins.

O script chama `GET /boards/{board_id}/pins` paginando com bookmark.

Para cada pin, escolhe a maior imagem e faz o download para a pasta indicada.

### Instalação
```
git clone https://j040.github.io/pinterest_board_manager/
cd pinterest_board_manager
pip install -r requirements.txt  
```
`# (ou) pip install requests tqdm`

### Como obter seu token

Converta ou crie uma conta Business no Pinterest.

No "Developer Portal", crie um app para obter um Token.

Escopos: boards:read, pins:read.

Rode o fluxo OAuth do seu app e copie o Access Token gerado.

(Opcional) Guarde o token em uma variável de ambiente:

`export PINTEREST_ACCESS_TOKEN="SEU_TOKEN"`

## Uso

### Liste os seus boards (para ver os IDs):

`python pinterest_board_dl.py --access-token "$PINTEREST_ACCESS_TOKEN" --list-boards`

### Baixe todas as imagens de um board:

python pinterest_board_dl.py --access-token "$PINTEREST_ACCESS_TOKEN" --board-id 123456789 --out ./downloads/meu_board

### Saída esperada:

Your boards:
```
{"id":"123456789","name":"Viagens","privacy":"PUBLIC"}
{"id":"987654321","name":"Referências","privacy":"SECRET"}
Done. Saved 42 image(s); skipped 1.
```

### Perguntas frequentes

Posso baixar de qualquer board público?
Não. A API oficial só permite ler boards que a sua conta pode acessar (seus ou compartilhados).

Dá para pegar a imagem em “qualidade original”?
O script escolhe a maior variante exposta pela API e tenta a rota “originals” quando disponível. Em alguns pins, a versão original pode não existir.

O token expira?
Tokens podem expirar ou ser revogados. Se algo der 401/403, gere um novo token ou revise escopos/permissões.

##### Privacidade

Este projeto é local: o token e os arquivos ficam no seu computador.
Veja a Política de Privacidade para detalhes.

##### Licença: MIT

##### Contato
João Victor Ribeiro – joao.v.ribeiro@outlook.com
