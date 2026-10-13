# Prova prática stemOS

Prova online para assistente administrativo/comercial. Inclui e-mail do pedido 345349, atendimento simulado e pesquisa no site stemOS.

- Prova: https://gheslaghesla.github.io/stemos-prova-pratica/
- Painel: https://gheslaghesla.github.io/stemos-prova-pratica/painel.html
- API e versão independente: https://stemos-prova-pratica.gheslaghesla.workers.dev/

As respostas são persistidas na Cloudflare D1 (banco stemos-provas), além do TXT disponível ao candidato. O painel exige a variável secreta ADMIN_KEY configurada na Cloudflare, fora do repositório. Sem essa variável, o painel nega acesso.

O tempo é contado no servidor do início à conclusão, incluindo pausas e pesquisa. Cada tentativa possui seu próprio protocolo. O mesmo candidato pode realizar novas tentativas; reenvios do mesmo protocolo não duplicam o registro.

## Arquivos

index.html e painel.html usam a API hospedada. worker.js implementa a aplicação e a API. schema.sql descreve a tabela já criada na Cloudflare. wrangler.jsonc contém o binding DB.

## Deploy

Com Node.js e acesso à conta Cloudflare: npm install; npx wrangler login; npx wrangler secret put ADMIN_KEY; npm run deploy. Não execute schema.sql outra vez no banco existente. Novas instalações precisam da tabela records antes do primeiro uso.

## Simulação

O cliente fictício responde por reconhecimento de palavras, sem conexão com WhatsApp real ou IA. A avaliação do candidato é humana.

## Verificação

Testados: contagem no servidor, resistência a timestamp alterado no cliente, tentativas separadas, reenvio idempotente, proteção do painel e sintaxe do frontend/Worker.
