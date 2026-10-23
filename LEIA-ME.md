# Metrônomo Fit3 para Android

Uma página só (`index.html`) que roda no **Chrome do celular** e fala com a pulseira por Web Bluetooth.
Ela aproveita o pareamento que o celular já tem com a pulseira, então não precisa resetar nada.

O Chrome só libera Bluetooth para páginas em **https** ou em endereços que você liberar manualmente.
Abaixo estão duas formas de abrir a página.

## Opção A: servir do PC na rede de casa (5 minutos)

1. No PC, abra o Prompt de Comando **na pasta do `index.html`** e rode:
   ```
   python -m http.server 8000
   ```
   Se o Firewall do Windows perguntar, permita em **redes privadas**.
2. Descubra o IP do PC com `ipconfig` (linha "Endereço IPv4", algo como `192.168.0.15`).
3. No celular, abra o Chrome e acesse `chrome://flags`. Procure **"Insecure origins treated as secure"**,
   coloque `http://192.168.0.15:8000` (com o seu IP), mude para **Enabled** e toque em **Relaunch**.
4. Acesse `http://192.168.0.15:8000` no Chrome do celular.

O celular e o PC precisam estar no mesmo Wi-Fi. Quando terminar os testes, volte essa flag para Default.

## Opção B: endereço https permanente

Publique o `index.html` em qualquer hospedagem estática (GitHub Pages, Netlify, Cloudflare Pages).
Assim você abre direto pelo celular, sem PC e sem flags. Dá até para adicionar à tela inicial como atalho.

## Usando

1. **Libere a pulseira do app da Samsung**: em Configurações > Apps, toque em **Forçar parada** no
   **Galaxy Wearable** e no **Galaxy Fit3 Plugin**. Os dois não podem falar com a pulseira ao mesmo tempo.
2. Na página, toque em **Conectar à pulseira** e escolha o **Galaxy Fit3** na lista.
3. Ajuste o BPM e toque em **Iniciar**.
4. Deixe a **tela do celular ligada** com a página aberta. O Chrome atrasa os timers quando ela vai para segundo plano.
5. Para voltar ao normal, desconecte na página e abra o Galaxy Wearable. Ele reconecta sozinho.

O painel de estatísticas mostra o atraso até a pulseira **receber** cada batida e a variação desse atraso.
Para medir a vibração em si, use o `analisar_gravacao.py` da versão para PC.

## Se der problema

- **A pulseira não aparece na lista:** o app da Samsung ainda está conectado. Force a parada dos dois apps
  de novo ou desligue e religue o Bluetooth do celular.
- **"Bluetooth bloqueado"**: a página não está em https e a flag do passo 3 não está ativa.
- **Conecta mas para no handshake:** desconecte, espere 10 segundos e tente de novo. Abra o
  **Registro técnico** no fim da página e me mande o conteúdo.

Licença: GPL-3.0-only. O protocolo vem dos projetos yuriyurin/Fit3-App e GokulArumugam/Fit3Bridge.
O projeto não tem relação com a Samsung.
