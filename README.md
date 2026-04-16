Projeto que simula um leilão

Para configurar as variáveis de ambiente modifique em: /cmd/auction/.env as seguintes variáveis:

BATCH_INSERT_INTERVA
MAX_BATCH_SIZE
AUCTION_INTERVAL
AUCTION_DURATION

Para rodar o projeto suba o docker compose com o mongo DB e o servidor do leilão
> docker compose up -d

E acesse as rotas para:
GET  localhost:8080/auction                    -> ver os leilões existentes
GET  localhost:8080/auction/:auctionId         -> encontrar um leilão por um id
POST localhost:8080/auction                    -> criar um leilão
GET  localhost:8080/auction/winner/:auctionId  -> encontrar o lance vencedor de um leilão pelo auctionId
POST localhost:8080/bid                        -> criar um lance
GET  localhost:8080/bid/:auctionId             -> encontrar o lance de um auctionId
GET  localhost:8080/user/:userId               -> encontrar um user pelo userId

Exemplo para criar um leilão:
> curl -X POST http://localhost:8080/auction \
  -H "Content-Type: application/json" \
  -d '{
    "product_name": "Notebook Gamer",
    "category": "Eletronicos",
    "description": "Notebook potente com placa RTX, ótimo para jogos",
    "condition": 1
  }'

Exemplo para ver os leilões abertos:
> curl "http://localhost:8080/auction?status=0"

Exemplo para ver os leilões fechados:
> curl "http://localhost:8080/auction?status=1"

Exemplo para criar um lance:
> curl -X POST http://localhost:8080/bid \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "auction_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "amount": 1500
  }'

Exemplo para ver o lance de um leilão pelo id:
> curl http://localhost:8080/bid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
