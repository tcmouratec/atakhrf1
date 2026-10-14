# atakhrf1

**Plugin ATAK que transforma um HackRF One ligado ao celular ou tablet Android em analisador de espectro portátil, ferramenta de detecção de drones/RF e localizador por RSSI, enviando informações ao mapa do ATAK via Cursor-on-Target (CoT).**

*English: [README.md](README.md)*

> Projeto independente da comunidade. Sem vínculo ou endosso do TAK Product Center, da Great Scott Gadgets ou de fabricantes.
> Somente recepção. Cumprir a legislação de rádio e privacidade do seu país é responsabilidade sua.

## Download

Baixe o plugin assinado em **[Releases](../../releases)**. Escolha o APK da versão do seu ATAK (o plugin só carrega na versão do ATAK para a qual foi compilado):

| Seu ATAK-CIV | Download |
|---|---|
| **5.7** | [v1.16.2](../../releases/tag/v1.16.2) |
| **5.6** | [v1.16.1](../../releases/tag/v1.16.1) |

Os APKs são assinados pelo Third Party Pipeline do TAK.gov, então carregam no **ATAK-CIV da Play Store**.

## O que faz

O painel tem quatro abas: **Scan | Caça | IA | Catálogo**. Funciona em tablet e celular.

### Scan
- Espectro e waterfall ao vivo, limiar ajustável, HackRF reconhecido e operado só pelo plugin.
- Quatro categorias de interesse, cada uma só com as ferramentas compatíveis: **Drones, Celular, Rádios, ISM**.
- Faixas pré-definidas por categoria com perfis de análise: celular (uplink/downlink, operadora por faixa), planos de canais de rádio (FRS/GMRS, PMR446, UHF/VHF, marítimo, aeronáutico), Wi-Fi 2,4 GHz, FPV 5,8 GHz, ISM genérico.
- Modos: **análise da faixa**, **espectro livre** (picos genéricos), **scan geral de drones** (7 faixas) e **scan burst** (janelas estreitas, burst do DroneID).
- Banco de assinaturas de drones (44 entradas com fonte) e casamento de canais FPV de 433 MHz a 5,8 GHz, incluindo FPV analógico de 900 MHz a 1,3 GHz e links de controle de longo alcance.
- Detecções ficam destacadas no espectro com cores por idade, e os alertas do scan de drones ficam retidos em um aviso até serem limpos.
- **Ouvir**: demodulação FM/AM com squelch e escuta automática.
- **Inspecionar**: janela de 1 MHz (cerca de 1 kHz de resolução) com espectro e waterfall, usando receptor I/Q próprio.
- **Gravar I/Q**: 5 segundos a 2 Msps em `.cs8` + `.json` (frequência, ganhos, posição, hora), com limite de armazenamento configurável. Nunca apaga sozinho.

### Caça
- Localização por RSSI de links de drone em frequência fixa (Wi-Fi 2,4 GHz, FPV analógico 5,8 GHz): girando antena direcional com a bússola ou caminhando com GPS.
- Mapa ao vivo no ATAK: trilha das medições, linha de marcação, fonte estimada e círculo de incerteza. A linha mostra só a direção; o círculo é incerteza, não garantia.

### IA (opcional, só online)
- Segunda opinião de um LLM sobre picos e candidatos. Offline, o plugin segue normal e nunca espera por ela.
- Anthropic e qualquer endpoint compatível com OpenAI (OpenRouter, Ollama, endpoint compatível do Gemini...). Tem botão **Testar IA**.
- Vereditos honestos: Provável (70%+), Possível (40-69%), Inconclusivo (<40%), Desconhecido. Vale o nível mais cauteloso. Nunca identifica pessoa nem transmissor.

### Catálogo
- Catálogo persistente de frequências (Observações, Capturas, Alertas) com filtros e exportação CSV.
- Envie uma entrada ao mapa por CoT. A posição é onde o sinal foi recebido mais forte, **não** a posição da fonte, e o texto do marcador avisa isso.
- **Limpar** remove os marcadores do plugin direto do mapa do ATAK.

### Mapa e diagnóstico
- CoT com UID estável (`a-u-A` para candidatos a drone, `a-u-G` nos demais). Sem fix de GPS, nenhuma posição é publicada.
- Registros periódicos de diagnóstico (bateria, memória, temperatura, modo em execução).
- As versões são cumulativas: um teste de regressão falha se alguma função de versão anterior deixar de ser alcançável.

## Limitações
- Detecção é triagem por energia. Não identifica modelo nem número de série do drone (isso é função do Remote ID).
- Um HackRF atende um aplicativo por vez.
- A chave da API de IA fica em texto simples nas preferências do plugin, no aparelho. Use chave gratuita ou restrita.
- Houve reinícios inexplicados de um Galaxy Tab A7 Lite durante scans; a causa não foi confirmada e há diagnóstico embutido para investigar.
- A Caça só funciona em links de frequência fixa; links com salto de frequência (OcuSync, ELRS) não são suportados.

## Requisitos
- ATAK-CIV 5.6 no Android, HackRF One, USB OTG.

## Apoie o projeto

Se o atakhrf1 for útil para você, pode apoiar o desenvolvimento com uma doação por Pix:

[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-donate-FFDD00?logo=buymeacoffee&logoColor=black)](https://buymeacoffee.com/tiagoufbao)

**Chave Pix (e-mail):** `tiagoufba@gmail.com`

## Termos de uso
O plugin é distribuído gratuitamente, somente em formato binário. O código-fonte não é publicado. Você pode usá-lo, mas não pode redistribuir, modificar nem revender sem autorização. Fornecido "como está", sem garantia. O ATAK e seu SDK têm termos próprios.

## Software de terceiros
O plugin inclui **libusb** (LGPL-2.1, https://github.com/libusb/libusb) e **libhackrf** (BSD-3-Clause, https://github.com/greatscottgadgets/hackrf). O código-fonte delas está disponível nesses links.
