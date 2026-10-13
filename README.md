# Prova prática stemOS

Três atividades para assistente administrativo/comercial: e-mail sobre o pedido 345349 enviado com prazo de 5 dias úteis, atendimento simulado sobre motores de robótica e pesquisa do site https://stemos.com.br/.

## Versão sem servidor — GitHub Pages

`index.html` funciona em um navegador e permite baixar as respostas e a conversa em `.txt` para envio por e-mail. Os rascunhos ficam no navegador. Não existe recebimento centralizado nem painel nesta versão.

Para publicar: no repositório, abra Settings → Pages e selecione a branch main, pasta / (root), caso esse recurso esteja disponível no plano e na visibilidade escolhidos.

## Versão completa — painel protegido

`worker.js` roda em Cloudflare Workers. As respostas são persistidas em R2 e o painel fica em `/avaliador`, com chave de acesso verificada no servidor. O GitHub armazena o código; GitHub Pages não executa o painel nem o armazenamento R2.

Com Node.js instalado e uma conta Cloudflare:

```sh
npm install
npx wrangler login
npx wrangler r2 bucket create stemos-provas
npx wrangler secret put ADMIN_KEY
npm run check
npm run deploy
```

No comando de segredo, informe uma chave longa e aleatória e guarde-a para acessar o painel. Nunca a coloque no repositório. A configuração de R2 está em `wrangler.jsonc`.

Envie aos candidatos a URL raiz publicada pelo Workers. Acesse `/avaliador` e informe a chave para consultar as respostas. Ao concluir a prova, o candidato também pode baixar um `.txt` e anexá-lo a um e-mail.

## Como funciona a simulação

O cliente fictício responde por regras de reconhecimento de palavras em português, sem integração com WhatsApp real ou modelo de IA. O cenário é fixo para todos: Mariana, professora do Colégio Horizonte, em Campinas, com uma equipe iniciante de FTC. As informações são reveladas conforme as perguntas. A simulação pode não compreender todas as formulações; a avaliação do atendimento deve ser humana.

Não há cronômetro, pontuação automática ou decisões automáticas de contratação. O candidato pode escolher livremente o formato do e-mail. Nome e e-mail identificam a prova. O candidato recebe informação sobre o registro de suas respostas.

## Verificação realizada

Sintaxe do Worker e do JavaScript da página; respostas da simulação; proteção do endpoint de avaliação; validação do envio; gravação e leitura com armazenamento em memória e prevenção de duplicidade para o mesmo protocolo. Deploy real de Workers/R2 e revisão visual em navegador ainda precisam ser verificados.
