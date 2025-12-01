
# Cardápio de Doces - Pacote com exemplos de integração de pagamento

Conteúdo do pacote:
- index.html -> site (front-end)
- server/mercadopago_server.js -> exemplo de criação de preferência (Mercado Pago Checkout Pro)
- server/stripe_server.js -> exemplo de criação de Checkout Session (Stripe Checkout)
- package.json, .env.example, README.md

**Como usar (rápido)**
1. Copie `.env.example` para `.env` e preencha as chaves: `MP_ACCESS_TOKEN` e/ou `STRIPE_SECRET_KEY`.
2. Instale dependências: `npm install express cors dotenv mercadopago stripe` (dependendo de qual server for usado).
3. Inicie o servidor desejado:
   - Mercado Pago: `npm run start:mp`
   - Stripe: `npm run start:stripe`
4. No front-end (`index.html`) configure a URL do backend para chamar `/create_preference` (Mercado Pago) ou `/create-checkout-session` (Stripe) com os itens do carrinho.
5. Consulte a documentação oficial para obter instruções avançadas e credenciais de produção.

Documentação útil (incluída aqui para referência):
- Mercado Pago: criar preferência / Checkout Pro docs.
- Stripe: Checkout Sessions quickstart docs.
